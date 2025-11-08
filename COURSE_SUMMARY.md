# Resumo do Curso: Introdução ao Ciclo de Vida de Modelos

## Visão Geral
Este repositório contém exercícios práticos completos para o curso de Introdução ao Ciclo de Vida de Modelos de Machine Learning, utilizando Python, Jupyter Notebooks e MLFlow.

## Estrutura do Curso

### Aula 2: Experimentação e MVP de Modelos
**Arquivo:** `aula_02_experimentacao_mvp/exercicio_experimentacao_mvp.ipynb`

**O que você aprenderá:**
- Configurar MLFlow para rastreamento de experimentos
- Treinar múltiplos modelos (Logistic Regression, Decision Tree, Random Forest)
- Comparar resultados e selecionar o melhor modelo
- Usar o MLFlow UI para visualização

**Dataset:** Wine Classification (sklearn)

### Aula 3: Desenvolvimento e Engenharia de Modelos
**Arquivo:** `aula_03_desenvolvimento_engenharia/exercicio_engenharia_modelos.ipynb`

**O que você aprenderá:**
- Criar features engineered (razões, produtos, polinomiais)
- Seleção de features com SelectKBest
- Pipelines de ML com StandardScaler
- Grid Search para otimização de hiperparâmetros
- Análise de feature importance

**Dataset:** Breast Cancer (sklearn)

### Aula 4: Implantação de Modelos (Deployment)
**Arquivo:** `aula_04_implantacao/exercicio_deployment.ipynb`

**O que você aprenderá:**
- Registrar modelos no MLFlow Model Registry
- Promover modelos entre stages (Staging, Production)
- Criar serviço de inferência
- Versionamento de modelos
- Estratégias de deployment (Blue-Green, Canary, Shadow)

**Dataset:** Iris (sklearn)

### Aula 5: Monitoramento e Manutenção
**Arquivo:** `aula_05_monitoramento_manutencao/exercicio_monitoramento.ipynb`

**O que você aprenderá:**
- Monitorar métricas de performance ao longo do tempo
- Detectar degradação de modelo
- Análise de data drift com testes estatísticos
- Implementar alertas automáticos
- Estratégias de retreinamento

**Dataset:** Breast Cancer (sklearn)

### Aula 6: CI/CD e Automação de Pipelines
**Arquivo:** `aula_06_cicd_automacao/exercicio_cicd_pipelines.ipynb`

**O que você aprenderá:**
- Criar Data Pipeline automatizado
- Training Pipeline com validação
- Test Pipeline com testes automatizados
- Deployment Pipeline com validações
- Orquestração completa de pipelines
- Exemplo de GitHub Actions workflow

**Dataset:** California Housing (sklearn)

### Aula 7: Governança e Ciclo de Feedbacks
**Arquivo:** `aula_07_governanca_feedback/exercicio_governanca.ipynb`

**O que você aprenderá:**
- Criar Model Card completo
- Sistema de auditoria e logs
- Sistema de coleta de feedback
- Rastreamento de linhagem (Data Lineage)
- Verificações de compliance e GDPR

**Dataset:** Iris (sklearn)

### Aula 8: Projeto Final - Ciclo Completo de ML
**Arquivo:** `aula_08_projeto_final/projeto_final_completo.ipynb`

**O que você aprenderá:**
- Integrar todos os conceitos das aulas anteriores
- Implementar pipeline end-to-end completo
- Criar sistema de predição de preços de imóveis
- Gerar relatórios profissionais
- Documentação completa com Model Card

**Dataset:** California Housing (sklearn)
**Meta:** RMSE < 0.7, R² > 0.70

## Tecnologias Utilizadas

### Core
- **Python 3.8+**
- **Jupyter Notebooks** - Ambiente interativo
- **MLFlow 2.10+** - Tracking, Registry, Deployment

### Machine Learning
- **scikit-learn 1.3+** - Algoritmos e pipelines
- **numpy 1.24+** - Computação numérica
- **pandas 2.0+** - Manipulação de dados

### Visualização
- **matplotlib 3.7+** - Gráficos básicos
- **seaborn 0.12+** - Gráficos estatísticos

### Monitoramento
- **evidently 0.4+** - Detecção de drift

## Como Começar

### 1. Instalação
```bash
# Clone o repositório
git clone https://github.com/lfbraz/introducao-ciclo-de-vida-de-modelos.git
cd introducao-ciclo-de-vida-de-modelos

# Crie ambiente virtual
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Instale dependências
pip install -r requirements.txt
```

### 2. Executar Notebooks
```bash
# Iniciar Jupyter
jupyter notebook

# Navegue até a pasta da aula desejada e abra o notebook
```

### 3. Usar MLFlow UI
```bash
# Em um terminal separado
mlflow ui

# Acesse http://localhost:5000
```

## Estrutura de Diretórios
```
.
├── README.md                           # Documentação principal
├── COURSE_SUMMARY.md                   # Este arquivo
├── requirements.txt                    # Dependências Python
├── .gitignore                          # Arquivos ignorados
├── data/                               # Diretório para datasets
├── aula_02_experimentacao_mvp/         # Aula 2
│   ├── README.md
│   └── exercicio_experimentacao_mvp.ipynb
├── aula_03_desenvolvimento_engenharia/ # Aula 3
│   ├── README.md
│   └── exercicio_engenharia_modelos.ipynb
├── aula_04_implantacao/                # Aula 4
│   ├── README.md
│   └── exercicio_deployment.ipynb
├── aula_05_monitoramento_manutencao/   # Aula 5
│   ├── README.md
│   └── exercicio_monitoramento.ipynb
├── aula_06_cicd_automacao/             # Aula 6
│   ├── README.md
│   └── exercicio_cicd_pipelines.ipynb
├── aula_07_governanca_feedback/        # Aula 7
│   ├── README.md
│   └── exercicio_governanca.ipynb
└── aula_08_projeto_final/              # Aula 8
    ├── README.md
    └── projeto_final_completo.ipynb
```

## Fluxo de Aprendizado Recomendado

1. **Semana 1-2:** Aulas 2 e 3
   - Experimentação básica
   - Feature engineering

2. **Semana 3-4:** Aulas 4 e 5
   - Deployment
   - Monitoramento

3. **Semana 5-6:** Aulas 6 e 7
   - Automação
   - Governança

4. **Semana 7-8:** Aula 8
   - Projeto final integrado

## Recursos Adicionais

### Documentação
- [MLFlow Documentation](https://mlflow.org/docs/latest/index.html)
- [Scikit-learn User Guide](https://scikit-learn.org/stable/user_guide.html)
- [Evidently Documentation](https://docs.evidentlyai.com/)

### Conceitos Importantes

#### Experimentação
- Registro de experimentos
- Comparação de modelos
- Seleção de MVP

#### Feature Engineering
- Criação de features
- Seleção de features
- Transformações

#### Deployment
- Model Registry
- Versionamento
- Estratégias de deployment

#### Monitoramento
- Data drift
- Concept drift
- Alertas automáticos

#### CI/CD
- Pipelines automatizados
- Testes automatizados
- Validação contínua

#### Governança
- Model Cards
- Auditoria
- Compliance

## Avaliação

### Critérios
- **Completude** (30%): Todas as tarefas completadas
- **Qualidade** (30%): Código limpo e bem documentado
- **Performance** (20%): Métricas dentro dos objetivos
- **Governança** (20%): Documentação e compliance

### Entregáveis Esperados
- Notebooks executados com resultados
- Modelos registrados no MLFlow
- Model Cards completos
- Relatórios de performance
- Código organizado e documentado

## Suporte

Para dúvidas:
1. Revise a documentação do notebook
2. Consulte os README de cada aula
3. Verifique a documentação oficial das bibliotecas
4. Entre em contato com o professor

## Próximos Passos

Após concluir o curso, considere:
1. Implementar um projeto real com seus próprios dados
2. Explorar MLFlow em ambientes cloud (AWS, Azure, GCP)
3. Estudar orquestradores como Airflow ou Kubeflow
4. Aprofundar em monitoring com Prometheus/Grafana
5. Explorar deployment em Kubernetes

## Conclusão

Este curso fornece uma base sólida em todas as etapas do ciclo de vida de modelos de ML, desde a experimentação inicial até o monitoramento em produção. Ao completar todos os exercícios, você terá experiência prática em ferramentas e técnicas essenciais para MLOps.

Bons estudos! 🚀📊🤖
