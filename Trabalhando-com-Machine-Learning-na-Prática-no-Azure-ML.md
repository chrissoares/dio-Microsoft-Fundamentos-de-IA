# Trabalhando com Machine Learning na Prática no Azure ML

## Laboratório

Acesse:

- https://aka.ms/ai900-auto-ml
- https://aka.ms/ai900-azure-ai-services

Acessar o Portal do Azure.

Criar um novo recurso de Machine Learning

No novo recurso de Machine Learning, acessar ML automatizado e criar um novo Trabalho de Ml automatizado.

Informar o Nome do trabalho, pode repetir o nome no Novo nome do experimento.

No tipo de Tarefa e dados, escolhemos regressão em Selecionar tipo de tarefa.

Em Selecionar os dados, vamos em Criar.

Damos um nome para o ativo de dados.

E colocamos uma descrição.

O tipo deve ficar Tabular.

Na fonte de dados, pode ser escolher desde um endereço web, quanto um arquivo local que será armazenado em nosso storage do azure, algum dado a partir do SQL, ou que já esteja armazenado no Azure.

Cada opção tem suas próprias etapas e são auto explicativas. Como exemplo, vamos escolher Local, pois o apresentado no curso, usando o endereço https://aka.ms/bike-rentals baixa um arquivo compactado.

Abra uma nova guia, sem fechar a página onde esta sendo configurado a fonte de dados.

Acesse o endereço https://aka.ms/bike-rentals, um arquivo compactado será baixado. 

Descompacte o arquivo no local de sua preferência, acesse a pasta bike-data, nela terá o arquivo daily-bike-share.csv. Este arquivo que será utilizado.

Voltando a configuração do da fonte de dados, escolha **De arquivos locais**. Clique em avançar.

Apareceram os armazenamentos disponíveis. Escolha um deles que preferir. Clique em avançar.

Clique no botão carregar arquivos ou pasta, escolha Carregar arquivos.

Navegue até o local onde esta o arquivo que daily-bike-share.csv e escolha ele. Clique em avançar.

Nas configurações, escolha o formato como Delimitado, Delimitador deixe Virgula, Codificação UTF-8, em Cabeçalho de coluna escolha Somente o primeiro arquivo tem cabeçalhos. Clique em avançar.

O esquema é onde são definido os tipos de cada coluna do arquivo, como inteiro, decimal, etc. Isto já é identificado automaticamente, pode conferir se todos estão corretos nos casos reais, para este exemplo pode apenas clicar em avançar.

Feito isto é hora de criar o Ativo de Dados. Clique em Criar. O processo seguinte pode demorar um pouco até ser finalizado.

Depois de termos nossos dados disponíveis, escolhemos e clique em avançar.

Nas configurações de tarefa, Coluna de destino vamos escolher rentals.

Clicar em Exibir definições de configuração adicional

Métrica primária: NormalizedRootMeanSquaredError

Desmarque todas as caixas de seleção.

Modelos permitidos: Escolha RandomForest e LightGBM.

Clique me Salvar.

Em Limites, para este exemplo, vamos configurar desta maneira:

Máximo de avaliações: 3

Máximo de avaliações simultâneas: 3

Máximo de nós: 3 

Limite de pontuação da métrica: 0,085

Tempo limite do experimento (minutos): 15

Tempo limite de iteração (minutos): 15

Tipo de validação coloque Divisão de validação de treinamento

Validação de percentual de dados: 10

Dados de teste: Nenhum

Clique em Avançar.

Em Computação, deixe:

Selecione o tipo de computação: Sem Servidor

Tipo de máquina virtual: CPU

Tipo de máquina virtual: Dedicado

Tamanho da máquina virtual, pode manter o que já vem configurado.

Número de instâncias: 1

Clique me Avançar

Agora, você pode rever todas as configurações anteriormente e então clicar em Enviar trabalho de treinamento.

Demora uns 10 minutos na média para concluir esta etapa.
