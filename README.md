# Machine-Learning-na-Pratica-no-Azure-ML
Resolução do Desafio Machine Learning na Prática no Azure ML

O Desafio consiste em criação de um modelo de previsão com seus pontos de extremidades configurados.
Abaixo teremos o passo a passo para a criação do modelo no Azure ML:

# Criação do Workspace no Azure ML

1. Entrar no portal do azure : https://portal.azure.com com suas credenciais.
   Obs: Caso ainda não tenha uma conta você irá precisar criar uma conta.
2. Após entrar no portal clique no "Create a resource"
3. Você será direcionado ao Marketplace do Azure, insira no campo de pesquisa "Azure Machine Learning" e clique em "create".
4. Configure seu recurso da seguinte forma:
   Subscription: Deixe o nome padrão que aparece.
   Resource group: Crie um resource group caso não tenha ou selecione um caso tenha.
   Name: Insira um nome único para o seu recurso.
   Region: Selecione a região mais próxima a você.
   Storage account: Mantenha a conta padrão criada.
   Key vault: Mantenha o padrão criado.
   Application insights: Mantenha o padrão criado.
   Container registry: None
5. Selecione "Review + Create" e depois "Create". Espere alguns minutos para a criação do seu workspace e depois vá para "deploy resource"
6. Selecione "Launch studio" e sign in no seu Azure Machine Learning studio com a sua conta Microsoft
7. No Azure Machine Learning studio crie um novo workspace

# Configurando seu recurso

1. Clique em "ML Automatizado" e clicar em novo ML automatizado com as seguintes configurações:
   Basic settings:

Job name: mslearn-bike-automl
New experiment name: mslearn-bike-rental
Description: Automated machine learning for bike rental prediction
Tags: none
Task type & data:

Select task type: Regression
Select dataset: Create a new dataset with the following settings:
Data type:
Name: bike-rentals
Description: Historic bike rental data
Type: Tabular
Data source:
Select From web files
Web URL:
Web URL: https://aka.ms/bike-rentals
Skip data validation: do not select
Settings:
File format: Delimited
Delimiter: Comma
Encoding: UTF-8
Column headers: Only first file has headers
Skip rows: None
Dataset contains multi-line data: do not select
Schema:
Include all columns other than Path
Review the automatically detected types
Select Create. After the dataset is created, select the bike-rentals dataset to continue to submit the Automated ML job.

Task settings:

Task type: Regression
Dataset: bike-rentals
Target column: Rentals (integer)
Additional configuration settings:
Primary metric: Normalized root mean squared error
Explain best model: Unselected
Use all supported models: Unselected. You’ll restrict the job to try only a few specific algorithms.
Allowed models: Select only RandomForest and LightGBM — normally you’d want to try as many as possible, but each model added increases the time it takes to run the job.
Limits: Expand this section
Max trials: 3
Max concurrent trials: 3
Max nodes: 3
Metric score threshold: 0.085 (so that if a model achieves a normalized root mean squared error metric score of 0.085 or less, the job ends.)
Timeout: 15
Iteration timeout: 15
Enable early termination: Selected
Validation and test:
Validation type: Train-validation split
Percentage of validation data: 10
Test dataset: None
Compute:

Select compute type: Serverless
Virtual machine type: CPU
Virtual machine tier: Dedicated
Virtual machine size: Standard_DS3_V2*
Number of instances: 1
* If your subscription restricts the VM sizes available to you, choose any available size.

2. Clique em "enviar trabalho de treinamento" e espere pela finalização que pode demorar alguns minutos.

# Revisando o melhor modelo e finalizando

1. Quando finalizar (o status deve estar como concluído), clique no melhor resumo de modelo, o link abaixo do nome do algorítmo (caso tenha mais de um escolha o que ache melhor)
2. Assim, após aparecer a tela do modelo, clique em implantar no "Serviço Web"
3. Acrescente os seguintes dados e clique em implantar

Name: predict-rentals
Description: Predict cycle rentals
Compute type: Azure Container Instance
Enable authentication: Selected

4. Assim que terminar tudo (o status ao lado do nome do modelo estiver como concluído e o implantar status estiver como êxito), clique no link do implantar status
5. Entrando assim no pontos de extremidade, clique em testar e utilize um código semelhante ao descrito abaixo e pronto, seu desenvolvimento de um componente nessa parte está pronto!

{

"Inputs": {

"data": [

{

"day": 1,

"mnth": 1,

"year": 2022,

"season": 2,

"holiday": 0,

"weekday": 1,

"workingday": 1,

"weathersit": 2,

"temp": 0.3,

"atemp": 0.3,

"hum": 0.3,

"windspeed": 0.3

}

]

},

"GlobalParameters": 1.0

}

# Não esqueça de deletar o recurso
1. Antes de tudo, você deve estar na tela inicial do Portal do Azure, procurar pelo nome grupo de recursos na pesquisa ou em alguma das barras e clicar no Grupo de Recursos em que seu recurso está (normalmente a própria tela de início vai estar disponibilizado isso, como abaixo, mas caso não esteja, essa alternativa anterior também funciona)
2. Entre nesse seu grupo de recurso e clique em Delete resource group ou remover grupo de recurso
3. Por último, confirme o nome do grupo de recursos e remova
