# Aula 4: Implantação de Modelos (Deployment)

## Descrição
Implante modelos em produção usando diferentes estratégias.

## Objetivos
- Registrar modelos no MLFlow Model Registry
- Versionar modelos adequadamente
- Servir modelos via API REST
- Implementar estratégias de deployment

## Exercício
Execute o notebook `exercicio_deployment.ipynb`

## API Flask de Predição (Opcional)
Além do notebook, você pode subir uma API simples em Flask para servir o modelo treinado na Aula 3.

### Pré-requisitos
- Ambiente Python do curso ativado
- Dependências instaladas: `pip install -r requirements.txt` (agora inclui Flask)
- Modelo salvo em `models/best_random_forest.joblib` (gerado na Aula 3)

### Executando localmente
No diretório raiz do repositório:

Linux/macOS/Git Bash:
```bash
export FLASK_APP=aula_04_implantacao/flask-app/app.py
python aula_04_implantacao/flask-app/app.py
```

Windows (PowerShell):
```powershell
$env:FLASK_APP = "aula_04_implantacao/flask-app/app.py"
python aula_04_implantacao/flask-app/app.py
```

> A variável `FLASK_APP` só é necessária se você usar `flask run`. Rodando `python .../app.py` diretamente, ela pode ser omitida.

Endpoints:
- `GET /` — Health check
- `POST /heart-disease-predict` — Recebe JSON e retorna predição

Formato de entrada:
- Você pode enviar já no formato pré-processado (colunas one-hot como `cp_atypical angina`, `restecg_normal`, etc.)
- OU enviar colunas brutas `cp`, `restecg`, `slope`, `thal`, `sex` que serão convertidas automaticamente.

Mapeamentos simples (valores inteiros → strings como na Aula 2):
- `sex`: 0 → Female, 1 → Male
- `cp`: 0 → typical angina, 1 → atypical angina, 2 → non-anginal, 3 → asymptomatic
- `restecg`: 0 → normal, 1 → st-t abnormality, 2 → left ventricular hypertrophy
- `slope`: 0 → upsloping, 1 → flat, 2 → downsloping
- `thal`: 0 → normal, 1 → fixed defect, 2 → reversable defect

Após mapear para strings, aplicamos **`pd.get_dummies(..., drop_first=True)` exatamente como na Aula 2** (veja notebook de experimentação). Assim as colunas geradas seguem o mesmo padrão do dataset pré-processado. Se alguma categoria não aparecer em um batch, a coluna correspondente é adicionada depois na etapa de alinhamento com valor 0.

Ordem das features: a API alinha automaticamente ao conjunto e ordem originais do treinamento (via `feature_names_in_`). Colunas extras são descartadas e faltantes adicionadas com 0.

### Exemplo de requisição

Windows (PowerShell) — `curl` é um alias de `Invoke-WebRequest` e não aceita a sintaxe abaixo; use `Invoke-RestMethod`:
```powershell
$body = @{
    age = 57; sex = 1; cp = 0; trestbps = 130; chol = 236; fbs = 0
    restecg = 1; thalch = 174; exang = 0; oldpeak = 0.0; slope = 1; ca = 1; thal = 2
} | ConvertTo-Json

Invoke-RestMethod -Uri http://localhost:5000/heart-disease-predict `
    -Method Post -ContentType "application/json" -Body $body
```
(Alternativa: `curl.exe` chama o curl real, mas as aspas do JSON precisam de escape.)

Linux/macOS/Git Bash:
```bash
curl -X POST http://localhost:5000/heart-disease-predict \
	-H "Content-Type: application/json" \
	-d '{
				"age": 57,
				"sex": 1,
				"cp": 0,
				"trestbps": 130,
				"chol": 236,
				"fbs": 0,
				"restecg": 1,
				"thalch": 174,
				"exang": 0,
				"oldpeak": 0.0,
				"slope": 1,
				"ca": 1,
				"thal": 2
			}'
```

Também suporta batch via `instances`:

```json
{
	"instances": [
		{ "age": 57, "sex": 1, "cp": 0, "trestbps": 130, "chol": 236, "fbs": 0, "restecg": 1, "thalch": 174, "exang": 0, "oldpeak": 0.0, "slope": 1, "ca": 1, "thal": 2 },
		{ "age": 62, "sex": 0, "cp": 2, "trestbps": 120, "chol": 281, "fbs": 0, "restecg": 1, "thalch": 103, "exang": 1, "oldpeak": 1.4, "slope": 2, "ca": 0, "thal": 3 }
	]
}
```

Observação: a API replica o feature engineering essencial da Aula 3 (ex.: `age_squared`, `bp_chol_ratio`, etc.) quando as colunas base são informadas. Caso você já envie essas colunas engenheiradas, elas serão respeitadas.

## Container Docker

Você pode executar a API em um container Docker para facilitar distribuição.

### Build da imagem (de dentro de `aula_04_implantacao`)
Execute os comandos abaixo estando dentro da pasta `aula_04_implantacao`.

```bash
docker build -t heart-api:latest -f Dockerfile ..
```

### Executar o container
```bash
docker run --rm -p 5000:5000 heart-api:latest
```

### Verificar
```bash
curl http://localhost:5000/
```

### Predição
```bash
curl -X POST http://localhost:5000/heart-disease-predict \
	-H "Content-Type: application/json" \
	-d '{"age":63,"sex":1,"cp":3,"trestbps":145,"chol":233,"fbs":1,"restecg":0,"thalch":150,"exang":0,"oldpeak":2.3,"slope":0,"ca":0,"thal":1}'
```

### Personalizações
- Variável `MODEL_PATH` pode ser sobrescrita: `docker run -e MODEL_PATH=/app/models/best_random_forest.joblib ...`
- Para uso de Gunicorn, instale `gunicorn` e ajuste `CMD` no Dockerfile para: `gunicorn -b 0.0.0.0:5000 app:app`

### .dockerignore
Arquivo `.dockerignore` criado para reduzir o tamanho da imagem (ignora `mlruns/`, `data/`, `venv/`, caches, etc.).

---
Esta seção demonstra para os alunos a equivalência entre o encoding da Aula 2 (strings + get_dummies(drop_first)) e o fluxo automatizado de produção dentro do container.
