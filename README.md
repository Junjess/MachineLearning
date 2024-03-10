# MachineLearning
Desafio de Projeto do bootcamp Microsoft Azure AI Fundamentals da empresa DIO. 

# Passos Iniciais
Para iniciar a utilizar o Microsoft Azure, é necessário possuir uma conta Microsoft. Acesse o link:(https://portal.azure.com). Ao entrar em sua conta, você deve clicar no botão "Create a Resource" no canto superior esquerdo da tela. 
Nesta próxima tela, pesquise por Machine Learning. Clique em Azure Machine Learning (geralmente é a primeira sugestão que aparece). Depois de selecionar, clique em "create".

# Preenchendo as Configurações
1. Inscrição(Subscription): Aqui você vai colocar a sua inscrição. Geralmente ela já vem preenchida.
2. Grupo de recursos(Resources Group): Você vai selecionar um criar um resource group. Para criar é só clicar em "crie um novo" e colocar o nome desejado para o seu grupo.
3. Nome(Name): Crie um nome para o seu espaço de trabalho.
4. Região(Region): Selecione a região mais próxima. (Recomendado o uso da East US ou Leste dos EUA).
5. Conta de armazenamento(Storage account): Vai ser criado automaticamente, não é necessário alterar.
6. Cofre de chaves(Key vault): Vai ser criado automaticamente, não é necessário alterar.
7. Informações sobre aplicativos(Application insights): Vai ser criado automaticamente, não é necessário alterar.
8. Registro de container(Container registry): Nenhum(none).
9. Clique em "Revise + crie" e depois clique em Criar.
10. Espere até finalizar a criação do workspace (pode levar alguns minutos).
11. Depois de finalizar, clique em "ir para recursos".
12. Clique em "launch studio", você vai ser direcionado para outra aba.

# Começando a criar a Machine Learning
1. Na página inicial, clique em "ML Automatizado".
2. Depois, clique em "novo trabalho de ML Automatizado".

## Configurações Básicas
1. Nome do trabalho: mslearn-bike-automl
2. Novo experimento nome: mslearn-bike-rental
3. Descrição: Automated machine learning for bike rental prediction
4. Marcas: nenhuma
5. Clique em "avançar"

## Tipo de tarefa e dados
1. Selecionar tipo de tarefa: Regressão.
2. Selecionar os dados: clique em criar.
### Criar ativos de dados
1. Nome: bike-rentals
2. Descrição: Historic bike rental data.
3. Tipo: Tabular.
4. Clica em avançar.
5. Selecione "De arquivo da WEB".
6. URL: https://aka.ms/bike-rentals
7. *Não* selecionar o campo selecionavel.
8. Clique em "Avançar"
9. Formato do arquivo: Delimitado
10. Delimitador: Vírgula
11. Codificação: UTF-8
12. Cabeçalhos de colunas: Somente o primeiro arquivo tem cabeçalho.
13. *Não* selecionar o campo selecionavel.
14. Avançar
15. Mantenha todas as linhas selecionadas, menos a linha Path.
16. Avance e clique em criar.

## Tipo de tarefa e dados
3. Tipo da tarefa: Regressão
4. Selecione o campo bike-rentals.
5. Avance.

## Configurações de tarefas
1. Coluna de destino: rentals(integer).
2. Clique em "exibir definições de configuração adicionais.
3. Métrica primária: Normalized root mean squared error
4. Desmarque todos os campos marcados.
5. Modelos bloqueados: RandomForest e LightGBM.
6. Clique em salvar.
7. Expanda a parte "Limites".
8. Máximo de avaliações: 3
9. Máximo de avaliações simultâneas:3
10. Máximo de nós: 3
11. Limite de pontuação da métrica: 0.085
12. Tempo limite do experimento (minutos): 15
13. Tempo limite de iteração (minutos): 15
14. Selecione "Habilitar encerramento adiantado".
15. Tipo de validação: Divisão de validação de treinamento.
16. Validação de percentual de dados: 10
17. Dados de testes: nenhum.
18. Avance.

## Computação
1. Sem servidor.
2. Tipo de máquina virtual: CPU
3. Tipo de máquina virtual: Dedicado
4. Tamanho: Standard_DS3_v2 (4 núcleo(s), 14GB de RAM, 28 GB de armazenamento, $0.29/hr)
5. Número de instâncias: 1
6. Clique em enviar trabalho de treinamento.
7. Espere até que o Status esteja como concluído.

# Revise os dados
1. Selecione o link embaixo do nome do algoritmo para ver os detalhes do modelo.

# Implantar e Testar o modelo
1. Na aba Modelo, selecione Implantar e use Serviços WEB.
2. Nome: predict-rentals
3. Descrição: Predict cycle rentals
4. Tipo de computação: Azure Container Instance (Instância de Contâiner da Azure)
5. Habilitar autenticação: Sim(selecione).
6. Espere até estar concluído.

# Testando a implantação do serviço
1. No menu a esquerda, clique em: Pontos de Extremidade.
2. Selecione predict-rentals
3. E vá para a aba Teste
4. No campo para json, digite  
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
5. Clique em Testar.  
6. Ao lado, irá aparecer os resultados do teste.
{1 item
"Results":[1 item
0:float361.39238595653825
]
}


