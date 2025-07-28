# 🤖 Machine Learning no Azure

<div align="center">

![Azure ML](https://img.shields.io/badge/Azure_Machine_Learning-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)

</div>

## 📋 O que é Machine Learning?

**Machine Learning (ML)** é um subcampo da Inteligência Artificial que permite aos computadores aprenderem e melhorarem automaticamente com a experiência, sem serem explicitamente programados para cada tarefa.

> 💡 **Conceito Simples**: Em vez de escrever regras específicas, damos exemplos ao computador e ele aprende padrões sozinho.

### **Tipos de Machine Learning**

#### **1. Aprendizado Supervisionado** 👨‍🏫
- **Definição**: O modelo aprende com dados que já têm respostas corretas
- **Exemplo**: Classificar emails como spam ou não spam
- **Técnicas**: Classificação, Regressão

#### **2. Aprendizado Não Supervisionado** 🔍
- **Definição**: O modelo encontra padrões em dados sem respostas pré-definidas
- **Exemplo**: Agrupar clientes por comportamento de compra
- **Técnicas**: Clustering, Redução de Dimensionalidade

#### **3. Aprendizado por Reforço** 🎮
- **Definição**: O modelo aprende através de tentativa e erro
- **Exemplo**: Jogos de computador, carros autônomos
- **Técnicas**: Q-Learning, Deep Q-Networks

---

## 🚀 Azure Machine Learning

### **O que é o Azure ML?**

**Azure Machine Learning** é uma plataforma em nuvem que simplifica todo o processo de desenvolvimento de modelos de ML, desde a preparação de dados até o deploy em produção.

### **Principais Vantagens**

✅ **Escalabilidade**: Processamento de grandes volumes de dados  
✅ **Facilidade de Uso**: Interface visual e notebooks Jupyter  
✅ **Integração**: Conecta-se facilmente com outros serviços Azure  
✅ **Segurança**: Controle de acesso e criptografia de dados  
✅ **Monitoramento**: Acompanhamento de performance em tempo real  

---

## 🛠️ Componentes do Azure ML

### **1. Workspace** 🏢

**Definição**: É o recurso de nível superior que contém todos os artefatos do Azure ML.

**O que inclui**:
- Experimentos de ML
- Datasets
- Modelos treinados
- Pipelines de ML
- Recursos de computação

### **2. Datasets** 📊

**Definição**: Representam os dados que você usa para treinar seus modelos.

**Tipos Suportados**:
- **Tabular**: Dados estruturados (CSV, Excel, etc.)
- **File**: Arquivos de imagem, áudio, vídeo
- **Text**: Documentos de texto

**Exemplo de Dataset**:
```python
# Criando um dataset no Azure ML
from azureml.core import Dataset

dataset = Dataset.Tabular.from_delimited_files(
    path='https://dados-exemplo.com/clientes.csv'
)
```

### **3. Compute Resources** 💻

**Definição**: Recursos de computação para treinar modelos.

**Tipos Disponíveis**:
- **Compute Instances**: Para desenvolvimento e experimentação
- **Compute Clusters**: Para treinamento distribuído
- **Inference Clusters**: Para servir modelos em produção

### **4. Experiments** 🧪

**Definição**: Organizam e rastreiam suas execuções de treinamento.

**Funcionalidades**:
- Log de métricas
- Comparação de modelos
- Versionamento de código
- Reproduzibilidade

---

## 🎯 Casos de Uso Práticos

### **1. Previsão de Vendas** 📈

**Problema**: Uma empresa quer prever as vendas do próximo mês.

**Solução com Azure ML**:
1. **Coleta de Dados**: Histórico de vendas, promoções, feriados
2. **Preparação**: Limpeza e transformação dos dados
3. **Treinamento**: Modelo de regressão (ex: Random Forest)
4. **Avaliação**: Métricas como RMSE, MAE
5. **Deploy**: API para previsões em tempo real

### **2. Detecção de Fraude** 🕵️

**Problema**: Identificar transações fraudulentas em tempo real.

**Solução com Azure ML**:
1. **Dados**: Histórico de transações (legítimas e fraudulentas)
2. **Modelo**: Classificação binária (Logistic Regression, Random Forest)
3. **Features**: Valor, localização, horário, padrões de comportamento
4. **Deploy**: Pipeline em tempo real para análise de novas transações

### **3. Análise de Sentimento** 😊

**Problema**: Analisar comentários de clientes automaticamente.

**Solução com Azure ML**:
1. **Dados**: Comentários de clientes com classificação manual
2. **Processamento**: Limpeza de texto, tokenização
3. **Modelo**: Classificação (positivo, neutro, negativo)
4. **Integração**: Conecta com Azure Cognitive Services

---

## 🔧 Ferramentas e Frameworks

### **Azure ML Studio** 🎨

**Interface Visual** para desenvolvimento de ML sem código:

**Funcionalidades**:
- **Designer**: Arrastar e soltar componentes
- **AutoML**: Treinamento automático de modelos
- **Notebooks**: Desenvolvimento com Python/R
- **Pipelines**: Orquestração de workflows

### **SDK do Azure ML** 📚

**Biblioteca Python** para desenvolvimento programático:

```python
# Exemplo básico de treinamento
from azureml.core import Workspace, Experiment
from azureml.core.compute import ComputeTarget

# Conectar ao workspace
ws = Workspace.from_config()

# Criar experimento
experiment = Experiment(workspace=ws, name='meu-experimento')

# Treinar modelo
run = experiment.submit(config)
run.wait_for_completion(show_output=True)
```

### **AutoML** 🤖

**Treinamento Automático** de modelos:

**Vantagens**:
- Seleção automática do melhor algoritmo
- Otimização de hiperparâmetros
- Feature engineering automático
- Comparação de modelos

---

## 📊 Fluxo de Trabalho Típico

### **1. Preparação dos Dados** 📋

```python
# Exemplo de preparação
import pandas as pd
from sklearn.preprocessing import StandardScaler

# Carregar dados
df = pd.read_csv('dados.csv')

# Limpeza
df = df.dropna()
df = df.drop_duplicates()

# Feature engineering
df['idade'] = 2024 - df['ano_nascimento']

# Normalização
scaler = StandardScaler()
df[['idade', 'renda']] = scaler.fit_transform(df[['idade', 'renda']])
```

### **2. Treinamento do Modelo** 🎯

```python
# Exemplo de treinamento
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split

# Dividir dados
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Treinar modelo
model = RandomForestClassifier(n_estimators=100)
model.fit(X_train, y_train)

# Avaliar
accuracy = model.score(X_test, y_test)
print(f'Acurácia: {accuracy:.2f}')
```

### **3. Deploy do Modelo** 🚀

```python
# Exemplo de deploy
from azureml.core.model import Model
from azureml.core.webservice import AciWebservice

# Registrar modelo
model = Model.register(workspace=ws, model_path='modelo.pkl')

# Criar serviço web
deployment_config = AciWebservice.deploy_configuration(
    cpu_cores=1, memory_gb=1
)

service = Model.deploy(
    ws, "meu-servico", [model], deployment_config
)
service.wait_for_deployment(show_output=True)
```

---

## 📈 Métricas e Avaliação

### **Métricas Comuns**

#### **Para Classificação**:
- **Acurácia**: Proporção de predições corretas
- **Precisão**: Proporção de predições positivas corretas
- **Recall**: Proporção de casos positivos identificados
- **F1-Score**: Média harmônica entre precisão e recall

#### **Para Regressão**:
- **RMSE**: Raiz do erro quadrático médio
- **MAE**: Erro absoluto médio
- **R²**: Coeficiente de determinação

### **Exemplo de Avaliação**:

```python
from sklearn.metrics import classification_report, confusion_matrix

# Predições
y_pred = model.predict(X_test)

# Relatório detalhado
print(classification_report(y_test, y_pred))

# Matriz de confusão
print(confusion_matrix(y_test, y_pred))
```

---

## 🔒 Segurança e Boas Práticas

### **Segurança de Dados**
- **Criptografia**: Dados em repouso e em trânsito
- **Controle de Acesso**: RBAC (Role-Based Access Control)
- **Auditoria**: Logs de todas as operações
- **Conformidade**: LGPD, GDPR, HIPAA

### **Boas Práticas**
- **Versionamento**: Controle de versão para código e dados
- **Documentação**: Explicar decisões e processos
- **Testes**: Validação rigorosa antes do deploy
- **Monitoramento**: Acompanhar performance em produção
- **Retreinamento**: Atualizar modelos periodicamente

---

## 🎓 Recursos de Aprendizado

### **Documentação Oficial**
- [Azure Machine Learning Documentation](https://docs.microsoft.com/azure/machine-learning/)
- [Azure ML Python SDK](https://docs.microsoft.com/python/api/overview/azure/ml/)
- [Azure ML Studio](https://ml.azure.com/)

### **Cursos e Tutoriais**
- [Microsoft Learn - Azure ML](https://docs.microsoft.com/learn/paths/build-ai-solutions-with-azure-ml/)
- [Azure ML Quickstart](https://docs.microsoft.com/azure/machine-learning/quickstart-create-resources)
- [MLOps com Azure](https://docs.microsoft.com/azure/machine-learning/concept-model-management-and-deployment)

### **Exemplos Práticos**
- [Azure ML Samples](https://github.com/Azure/MachineLearningNotebooks)
- [Azure ML Designer](https://docs.microsoft.com/azure/machine-learning/tutorial-designer-automobile-price-train-score)

---

<div align="center">

*"Machine Learning não é mágica, é matemática aplicada com dados."*

</div> 