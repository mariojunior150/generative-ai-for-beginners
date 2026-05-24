# Construindo Aplicativos de Busca

[![Introdução a IA Generativa e Modelos de Linguagem](./images/08-lesson-banner.png?WT.mc_id=academic-105485-koreyst)](https://youtu.be/W0-nzXjOjr0?si=GcsqiTTvd7RKbo7V)

> _(Clique na imagem acima para assistir ao vídeo desta lição)_

LLMs vão além de chatbots e geração de texto — também é possível construir aplicativos de busca usando Embeddings. Embeddings são representações numéricas de dados (também chamadas vetores) e podem ser usadas para busca semântica sobre conteúdo.

Nesta lição, você vai construir um aplicativo de busca para nossa startup educacional. Nossa startup é uma organização sem fins lucrativos que fornece educação gratuita a estudantes em países em desenvolvimento. Temos muitos vídeos no YouTube que os estudantes podem usar para aprender sobre IA. Queremos criar um aplicativo de busca que permita aos estudantes procurar um vídeo do YouTube digitando uma pergunta.

Por exemplo, um estudante pode digitar “O que são Jupyter Notebooks?” ou “O que é Azure ML” e o aplicativo de busca retornará uma lista de vídeos relevantes — e, melhor ainda, um link para o ponto exato do vídeo onde a resposta é abordada.

## Introdução

Nesta lição, cobriremos:

- Busca semântica vs busca por palavras-chave.
- O que são Embeddings de texto.
- Como criar um índice de Embeddings de texto.
- Como buscar em um índice de Embeddings de texto.

## Objetivos de Aprendizagem

Ao concluir esta lição, você será capaz de:

- Diferenciar busca semântica de busca por palavra-chave.
- Explicar o que são Embeddings de texto.
- Criar uma aplicação que usa Embeddings para buscar dados.

## Por que construir um aplicativo de busca?

Construir um aplicativo de busca ajuda a entender como usar Embeddings para encontrar informação relevante. Você também aprenderá a criar um sistema que permita aos estudantes encontrar respostas rapidamente.

A lição inclui um índice de Embeddings dos transcripts do canal Microsoft [AI Show](https://www.youtube.com/playlist?list=PLlrxD0HtieHi0mwteKBOfEeOYf0LJU4O1). O índice contém os Embeddings dos transcripts até outubro de 2023. Você usará esse índice para montar o aplicativo de busca da nossa startup. O app retorna um link com timestamp para o trecho do vídeo onde a resposta aparece — uma forma prática de ajudar estudantes a encontrar o que precisam rapidamente.

O exemplo abaixo mostra uma consulta semântica para a pergunta 'can you use rstudio with azure ml?'. Observe a URL do YouTube; ela contém um timestamp que leva você até o ponto do vídeo onde a resposta para a pergunta é abordada.

![Consulta semântica para a pergunta "can you use rstudio with Azure ML"](./images/query-results.png?WT.mc_id=academic-105485-koreyst)

## O que é busca semântica?

Você pode estar se perguntando: o que é busca semântica? Busca semântica é uma técnica que usa o significado (semântica) das palavras em uma consulta para retornar resultados relevantes.

Por exemplo, se você procura por “meu carro dos sonhos”, a busca semântica entende que você não está sonhando sobre um carro, mas procurando seu carro `ideal`. Já a busca por palavra-chave faria uma busca literal por termos como “sonho” e “carro”, frequentemente retornando resultados irrelevantes.

## O que são Embeddings de Texto?

[Text embeddings](https://en.wikipedia.org/wiki/Word_embedding?WT.mc_id=academic-105485-koreyst) são uma técnica de representação de texto usada em [processamento de linguagem natural](https://en.wikipedia.org/wiki/Natural_language_processing?WT.mc_id=academic-105485-koreyst). Embeddings de texto são representações numéricas semânticas de texto. Eles são usados para representar dados de forma que seja fácil para uma máquina entender. Existem muitos modelos para gerar embeddings de texto; nesta lição, vamos nos concentrar em gerar embeddings usando o modelo de Embeddings do OpenAI.

Por exemplo, imagine o trecho abaixo em um transcript de um episódio do AI Show:

```text
Today we are going to learn about Azure Machine Learning.
```

Enviaríamos o texto para a API de Embeddings do OpenAI e ela retornaria o seguinte embedding composto por 1536 números, também chamado de vetor. Cada número no vetor representa um aspecto diferente do texto. Para simplificar, aqui estão os primeiros 10 números do vetor.

```python
[-0.006655829958617687, 0.0026128944009542465, 0.008792596869170666, -0.02446001023054123, -0.008540431968867779, 0.022071078419685364, -0.010703742504119873, 0.003311325330287218, -0.011632772162556648, -0.02187200076878071, ...]
```

## Como o índice de Embeddings foi criado?

O índice de Embeddings desta lição foi gerado por uma série de scripts Python. Você encontra os scripts e instruções no [README](./scripts/README.md?WT.mc_id=academic-105485-koreyst) na pasta `scripts` desta lição. Não é necessário executar esses scripts para completar a lição, pois o índice já está fornecido.

Os scripts executam as seguintes etapas:

1. A transcrição de cada vídeo do YouTube na playlist [AI Show](https://www.youtube.com/playlist?list=PLlrxD0HtieHi0mwteKBOfEeOYf0LJU4O1) é baixada.
2. Usando [OpenAI Functions](https://learn.microsoft.com/azure/ai-services/openai/how-to/function-calling?WT.mc_id=academic-105485-koreyst), é feita uma tentativa de extrair o nome do palestrante dos primeiros 3 minutos da transcrição do YouTube. O nome do palestrante de cada vídeo é armazenado no índice de embeddings chamado `embedding_index_3m.json`.
3. O texto da transcrição é então dividido em segmentos de texto de **3 minutos**. O segmento inclui cerca de 20 palavras de sobreposição com o próximo segmento para garantir que o Embedding do segmento não seja cortado e para fornecer melhor contexto de busca.
4. Cada segmento de texto é então enviado para a API de Chat do OpenAI para resumir o texto em 60 palavras. O resumo também é armazenado no índice de embeddings `embedding_index_3m.json`.
5. Finalmente, o texto do segmento é enviado para a API de Embeddings do OpenAI. A API de Embeddings retorna um vetor de 1536 números que representam o significado semântico do segmento. O segmento junto com o vetor de Embeddings do OpenAI é armazenado no índice de embeddings `embedding_index_3m.json`.

### Bancos de dados vetoriais

Para simplificar a lição, o índice de Embeddings é armazenado em um arquivo JSON chamado `embedding_index_3m.json` e carregado em um DataFrame do Pandas. No entanto, em produção, o índice de Embeddings seria armazenado em um banco de dados vetorial como [Azure Cognitive Search](https://learn.microsoft.com/training/modules/improve-search-results-vector-search?WT.mc_id=academic-105485-koreyst), [Redis](https://cookbook.openai.com/examples/vector_databases/redis/readme?WT.mc_id=academic-105485-koreyst), [Pinecone](https://cookbook.openai.com/examples/vector_databases/pinecone/readme?WT.mc_id=academic-105485-koreyst), [Weaviate](https://cookbook.openai.com/examples/vector_databases/weaviate/readme?WT.mc_id=academic-105485-koreyst), entre outros.

## Entendendo similaridade cosseno

Já aprendemos sobre embeddings de texto; o próximo passo é aprender como usar embeddings de texto para buscar dados e, em particular, encontrar os embeddings mais similares a uma determinada consulta usando similaridade cosseno.

### O que é similaridade cosseno?

A similaridade cosseno é uma medida de similaridade entre dois vetores; você também ouvirá isso referido como `busca por vizinhos mais próximos`. Para executar uma busca por similaridade cosseno, você precisa vetorizar o texto da consulta usando a API de Embeddings do OpenAI. Depois, calcule a similaridade cosseno entre o vetor da consulta e cada vetor no índice de Embeddings. Lembre-se de que o índice de Embeddings tem um vetor para cada segmento de texto da transcrição do YouTube. Finalmente, ordene os resultados pela similaridade cosseno e os segmentos de texto com maior similaridade cosseno serão os mais similares à consulta.

De uma perspectiva matemática, a similaridade cosseno mede o cosseno do ângulo entre dois vetores projetados em um espaço multidimensional. Essa medida é benéfica porque, se dois documentos estiverem distantes pela distância euclidiana devido ao tamanho, eles ainda podem ter um ângulo menor entre eles e, portanto, uma similaridade cosseno maior. Para mais informações sobre equações de similaridade cosseno, veja [Similaridade cosseno](https://en.wikipedia.org/wiki/Cosine_similarity?WT.mc_id=academic-105485-koreyst).

## Construindo seu primeiro aplicativo de busca

Agora, vamos aprender como construir um aplicativo de busca usando Embeddings. O aplicativo de busca permitirá que os estudantes pesquisem um vídeo digitando uma pergunta. O aplicativo de busca retornará uma lista de vídeos relevantes à pergunta. O aplicativo de busca também retornará um link para o ponto do vídeo onde a resposta para a pergunta está localizada.

Esta solução foi desenvolvida e testada no Windows 11, macOS e Ubuntu 22.04 usando Python 3.10 ou superior. Baixe Python em [python.org](https://www.python.org/downloads/?WT.mc_id=academic-105485-koreyst).

## Tarefa — construir um aplicativo de busca para estudantes

Apresentamos nossa startup no início desta lição. Agora é hora de permitir que os estudantes construam um aplicativo de busca para seus trabalhos avaliativos.

Neste exercício, você criará os Serviços Azure OpenAI que serão usados para construir o aplicativo de busca. Você criará os seguintes Serviços Azure OpenAI. Você precisará de uma assinatura do Azure para concluir este exercício.

### Inicie o Azure Cloud Shell

1. Faça login no [portal do Azure](https://portal.azure.com/?WT.mc_id=academic-105485-koreyst).
2. Selecione o ícone do Cloud Shell no canto superior direito do portal do Azure.
3. Selecione **Bash** como o tipo de ambiente.

#### Crie um grupo de recursos

> Para estas instruções, estamos usando o grupo de recursos chamado "semantic-video-search" em East US.
> Você pode alterar o nome do grupo de recursos, mas ao mudar a localização dos recursos,
> verifique a [tabela de disponibilidade de modelos](https://aka.ms/oai/models?WT.mc_id=academic-105485-koreyst).

```shell
az group create --name semantic-video-search --location eastus
```

#### Crie um recurso Azure OpenAI Service

No Cloud Shell, execute este comando para criar o recurso Azure OpenAI Service:

```shell
az cognitiveservices account create --name semantic-video-openai --resource-group semantic-video-search \
    --location eastus --kind OpenAI --sku s0
```

#### Obtenha endpoint e chaves para uso na aplicação

No Cloud Shell, execute os comandos abaixo para recuperar o endpoint e a chave do recurso:

```shell
az cognitiveservices account show --name semantic-video-openai \
   --resource-group  semantic-video-search | jq -r .properties.endpoint
az cognitiveservices account keys list --name semantic-video-openai \
   --resource-group semantic-video-search | jq -r .key1
```

#### Faça o deploy do modelo de Embeddings OpenAI

No Cloud Shell, execute este comando para implantar o modelo de Embeddings OpenAI:

```shell
az cognitiveservices account deployment create \
    --name semantic-video-openai \
    --resource-group  semantic-video-search \
    --deployment-name text-embedding-ada-002 \
    --model-name text-embedding-ada-002 \
    --model-version "2"  \
    --model-format OpenAI \
    --sku-capacity 100 --sku-name "Standard"
```

## Solução

Abra o [notebook de solução](./python/aoai-solution.ipynb?WT.mc_id=academic-105485-koreyst) no GitHub Codespaces e siga as instruções.

Quando você executar o notebook, será solicitado que insira uma consulta. A caixa de entrada se parecerá com isto:

![Caixa de entrada para o usuário inserir uma consulta](./images/notebook-search.png?WT.mc_id=academic-105485-koreyst)

## Excelente trabalho! Continue seu aprendizado

Após concluir esta lição, confira nossa [coleção de aprendizado de IA Generativa](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) para continuar evoluindo seu conhecimento em IA Generativa!

Vá para a Lição 9, onde veremos como [construir aplicativos de geração de imagens](../09-building-image-applications/README.md?WT.mc_id=academic-105485-koreyst)!
