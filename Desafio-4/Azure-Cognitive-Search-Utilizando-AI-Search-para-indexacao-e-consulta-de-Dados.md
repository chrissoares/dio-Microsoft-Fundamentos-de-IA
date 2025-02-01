# Laboratório
# Azure Cognitive Search: Utilizando AI Search para indexação e consulta de Dados

## Criando o Serviço AI Search

No Portal do Azure, ir na opção Criar um recurso.

Pesquise porAzure AI Search

Normalmente o primeiro resultado será Azure AI services, clique nele.

Plano: Azure AI Search.

Clique em Criar

Selecione a assinatura, e o grupo de recursos.

Dê um nome para o serviço que esta sendo criado.

Escolha o local, deve ser o mesmo do recurso de Azure AI Services. (Fora dos Estados Unidos é mais caro)

Em camada de preços, clique me Alterar o Tipo de Preço.

Escolha o Básico.

Verifique as outras opções de configuração, se desejar, como Escala, Em Rede, Rótulos.

Clique em Revisar + criar e/ou Criar.

## Criando o Azure AI Services

De volta ao Portal do Azure, ir na opção Criar um recurso.

Pesquise por: Azure AI services

Normalmente o primeiro resultado será Azure AI services, clique nele.

Em plano escolha: Azure AI services

Clique em Criar

Selecione a assinatura, e o grupo de recursos.

Escolha o local (Fora dos Estados Unidos é mais caro)

Dê um nome para o serviço que esta sendo criado.

Tipo de preço: Standard S0

Marque a caixa confirmando que leu os termos abaixo. Leia os termos

Verifique as outras opções de configuração, se desejar, como Escala, Em Rede, Rótulos.

Clique em Revisar + criar e/ou Criar.

## Criando e Configurando a Conta de Armazenamento

De volta ao Portal do Azure, ir na opção Criar um recurso.

Categoria: **Armazenamento**

Localize e acesse: **Conta de armazenamento**

Selecione a assinatura, e o grupo de recursos.

Dê um nome para o serviço que esta sendo criado.

Escolha o local (Fora dos Estados Unidos é mais caro)

Serviço Primario: Armazenamento de Blobs do Azure ou Azure Data Lake Storage Gen 2

Desempenho: Standard

Redundância: LRS

Verifique as outras opções de configuração, se desejar, como: Avançado, Rede, Proteção de dados, Criptografia e Marcas.

Clique em Revisar + criar e/ou Criar

Aguarde finalizar a criação do Storage Account e acesse ele.

Depois que foi criado, é necessário (para o laboratório) liberar o acesso anônimo ao Storage Account.

Dentro do recurso de Storage Account criado.

Acesse Configurações, Configuração.

Localize a opção, Permitir acesso anônimo ao Blob, e habilite ela.

Vamos precisar colocar alguns arquivos em um container.

Localize a opção Armazenamento de dados

Acesse Contêineres

Clique na opção + Contêiner na parte superior do quadro a direita da página.

Defina um nome para ele, ex: coffer-reviews

Nível de acesso anônimo: Contêiner (acesso de leitura anônimo para contêineres e blobs)

Enquanto ocorre a criação do container, podemos adiantar e baixar os arquivos que serão utilizados. pelo link: https://aka.ms/mslearn-coffee-reviews

Será baixado um arquivo compactado chamado reviews.zip, descompacte em um local de sua preferência.

Volte ao seu Storage Account.

Acesse o contêiner criado.

Vá na opção carregar.

Carregue todos os arquivos que foram descompactados. (review-1.docx até review-9.docx)

Eles apareceram dentro do seu Contêiner criado.

## Configuração da Pesquisa

Acesse o serviço de pesquisa.

Entre na opção Importar dados

Fonte de dados: Armazenamento do Blob do Azure

Notem da fonte de dados: coffee-customer-data

Dados para extrair: Conteúdo e metadados

Modo de análise: Padrão

Assinatura: Escolha sua assinatura

Cadeia de conexão: Clique me Escolher uma conexão existente.

Escolha o recurso de Storage Account criado anteriormente.

Escolha o contêiner criado.

Clique em Selecionar.

Autenticação de identidade gerenciada: Nenhum

Nome do contêiner: Já vai ser preenchido depois de escolher a conexão.

Pasta de Blobs: deixar em branco.

Descrição: Descreva o que esta sendo importado, ex: Reviews for Fourth Coffee shops

Clique em Próximo: Adicionar habilidades cognitivas (opcional)

Em Anexar Serviços de IA, escolha o serviço que criou anteriormente.

Em Adicionar enriquecimentos

Nome do conjunto de habilidades: Dê um nome que descreva as skills, ex: **coffee-skillset**

Marque o Checkbox Habilitar OCR e mesclar todo o texto no campo merged_content

Campo de dados de origem: **merged_content**

Nível de granularidade do enriquecimento: Páginas (partes de caracteres 5000)

**Não** marque a caixa Habilitar o enriquecimento incremental.

Em “Os itens marcados abaixo exigem um nome de campo.” marque conforme a tabela abaixo:

| Habilidades Cognitivas de Texto | Nome do Campo |
| --- | --- |
| Extrair nomes de localização | locations |
| Extrair frases-chave | keyphrases |
| Detectar sentimento | sentiment |
| Gerar marcações de imagens | imageTags |
| Gerar legendas de imagens | imageCaption |

Em Salvar os enriquecimentos em um repositório de conhecimento

Selecione:

- Projeções de imagem
- Documentos
- Páginas
- Frases-chave
- Entidades
- Detalhes da imagem
- Referência de imagem

Será exibido um Alerta. Clique em Escolher uma conexão existente.

Escolha o Storage Account que criamos no início deste laboratório.

Clique em + Contêiner:

Defina um nome: **knowledge-store**

Deixe-o como privado

Escolha o contêiner: **knowledge-store**

Clique em Selecionar.

Clique em Próximo: Personalizar índice de destino

Nome do índice: **coffee-index**

Confira se me Chave, esta o nome **metadata_storage_path**

Nome do sugestor: Deixar em branco

Modo de busca: **autopopulated** (mas não tem esta opção disponível no momento, esta ficando como **analyzingInfixMatching**)

Na tabela seguinte, revise as configurações dos campos de índice. Marque a caixa Filtrável para todos os campos que já estão selecionados por padrão: content, locations, keyphrases, sentiment, merged_content, text, layoutText, imageTags, imageCaption

Clique me Próximo> Criar um indexador

Nome: **coffee-indexer**

Agenda: **Uma vez**

Descrição: É opcional, pode descrever o que se espera ao usar este recurso.

**Opções Avançadas:**

Garanta que o checkbox Chaves de Codificação de Base 64 está marcado.

Clique em enviar. Será criado o a fonte de dados, Conjunto de Habilidades, índice e o indexador

De volta a página do recurso Azure IA Search.

No painel a esquerda.

Localize Gerenciamento de Pesquisa

Selecione Indexadores.

Selecione o índice recém criado **coffee-indexer(**azureblob-indexer no meu caso)

Aguarde um instante e clique em Atualizar, até que o status apresente Êxito.

Clique no nome do índice para ver mais detalhes.

## Realizando Pesquisas

Na página do recurso, em Visão geral.

Clique em Explorador de pesquisa

Índice: **coffe-index**

Em Exibir, escolha Exibição JSON

Vai ser exibido o Editor de Consultas JSON.

Copie o código e cole nele:

```jsx
{
    "search": "*",
    "count": true
}
```

Será retornado todos os documentos do índice, incluindo o total de documentos no campo **@odata.count**.

Para localizar pela localização use:

```jsx
{
 "search": "locations:'Chicago'",
 "count": true
}
```

Será apresentado todos os documentos qual a localidade seja Chicago. **@odata.count** vai apresentar um valor de 3.

Para pesquisar pelo sentimento, vamos usar:

```jsx
{
 "search": "sentiment:'negative'",
 "count": true
}
```

Será apresentado todos os documentos que o sentimento quanto a review foi negativo.

## Insights

Uma aplicação que resgata os comentários a partir de:

- Postagens nas contas do instagram
- Postagens nas páginas do facebook
- Vídeos no Tiktok
- Empresas no Google Maps

Pode ser reunido essas informações periodicamente e através do bando de dados, realizar a integração com a pesquisa que vai retornar o sentimento sobre cada assunto postado além dos serviços e produtos vendidos.
