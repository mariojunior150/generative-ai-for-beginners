# Construindo Aplicações de Geração de Imagens

[![Construindo Aplicações de Geração de Imagens](./images/09-lesson-banner.png?WT.mc_id=academic-105485-koreyst)](https://youtu.be/B5VP0_J7cs8?si=5P3L5o7F_uS_QcG9)

Existe mais em LLMs do que geração de texto. Também é possível gerar imagens a partir de descrições em texto. Ter imagens como modalidade pode ser muito útil em diversas áreas, como MedTech, arquitetura, turismo, desenvolvimento de jogos e mais. Neste capítulo, vamos explorar os dois modelos de geração de imagem mais populares: DALL-E e Midjourney.

## Introdução

Nesta lição, vamos cobrir:

- Geração de imagens e por que ela é útil.
- O que são DALL-E e Midjourney e como funcionam.
- Como você construiria um aplicativo de geração de imagens.

## Objetivos de Aprendizagem

Ao concluir esta lição, você será capaz de:

- Construir uma aplicação de geração de imagens.
- Definir limites para sua aplicação com metaprompts.
- Trabalhar com DALL-E e Midjourney.

## Por que construir uma aplicação de geração de imagens?

Aplicações de geração de imagens são uma ótima maneira de explorar as capacidades da IA Generativa. Elas podem ser usadas, por exemplo, para:

- **Edição e síntese de imagens**. Você pode gerar imagens para vários casos de uso, como edição de imagem e síntese de imagem.

- **Aplicação em diversas indústrias**. Elas também podem ser usadas para gerar imagens para diferentes setores, como MedTech, Turismo, desenvolvimento de jogos e mais.

## Cenário: Edu4All

Como parte desta lição, continuaremos trabalhando com nossa startup Edu4All. Os estudantes criarão imagens para suas avaliações; exatamente quais imagens produzir é decisão dos próprios alunos, mas podem ser ilustrações para um conto de fadas, um novo personagem para sua história ou algo que ajude a visualizar ideias e conceitos.

Veja o que os estudantes da Edu4All poderiam gerar, por exemplo, se estiverem trabalhando em aula sobre monumentos:

![Edu4All startup, aula sobre monumentos, Torre Eiffel](./images/startup.png?WT.mc_id=academic-105485-koreyst)

usando um prompt como

> "Dog next to Eiffel Tower in early morning sunlight"

## O que são DALL-E e Midjourney?

[DALL-E](https://openai.com/dall-e-2?WT.mc_id=academic-105485-koreyst) e [Midjourney](https://www.midjourney.com/?WT.mc_id=academic-105485-koreyst) são dois dos modelos de geração de imagem mais populares; eles permitem usar prompts para gerar imagens.

### DALL-E

Vamos começar com o DALL-E, que é um modelo de IA Generativa que gera imagens a partir de descrições em texto.

> [DALL-E é uma combinação de dois modelos, CLIP e atenção difusa](https://towardsdatascience.com/openais-dall-e-and-clip-101-a-brief-introduction-3a4367280d4e?WT.mc_id=academic-105485-koreyst).

- **CLIP** é um modelo que gera embeddings — representações numéricas de dados — a partir de imagens e texto.

- **Atenção difusa** é um modelo que gera imagens a partir de embeddings. O DALL-E é treinado em um conjunto de dados de imagens e texto e pode ser usado para gerar imagens a partir de descrições de texto. Por exemplo, o DALL-E pode gerar imagens de um gato usando chapéu ou um cachorro com um moicano.

### Midjourney

O Midjourney funciona de maneira semelhante ao DALL-E: ele gera imagens a partir de prompts de texto. O Midjourney também pode ser usado para gerar imagens com prompts como “a cat in a hat” ou “a dog with a mohawk”.

![Imagem gerada por Midjourney, pombo mecânico](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8c/Rupert_Breheny_mechanical_dove_eca144e7-476d-4976-821d-a49c408e4f36.png/440px-Rupert_Breheny_mechanical_dove_eca144e7-476d-4976-821d-a49c408e4f36.png?WT.mc_id=academic-105485-koreyst)
_Crédito da imagem Wikipedia, imagem gerada por Midjourney_

## Como DALL-E e Midjourney funcionam

Primeiro, [DALL-E](https://arxiv.org/pdf/2102.12092.pdf?WT.mc_id=academic-105485-koreyst). O DALL-E é um modelo de IA Generativa baseado na arquitetura transformer com um _transformer autorregressivo_.

Um _transformer autorregressivo_ define como um modelo gera imagens a partir de descrições em texto: ele gera um pixel de cada vez e, em seguida, usa os pixels gerados para produzir o próximo pixel, passando por múltiplas camadas em uma rede neural, até que a imagem esteja completa.

Com esse processo, o DALL-E controla atributos, objetos, características e mais na imagem que gera. No entanto, o DALL-E 2 e o DALL-E 3 têm ainda mais controle sobre a imagem gerada.

## Construindo seu primeiro aplicativo de geração de imagens

Então, o que é preciso para construir uma aplicação de geração de imagens? Você precisa das seguintes bibliotecas:

- **python-dotenv** — é altamente recomendável usar essa biblioteca para manter seus segredos em um arquivo _.env_ separado do código.
- **openai** — essa biblioteca é o que você usará para interagir com a API da OpenAI.
- **pillow** — para trabalhar com imagens em Python.
- **requests** — para ajudar a fazer requisições HTTP.

## Criar e implantar um modelo Azure OpenAI

Se ainda não fez, siga as instruções na página do [Microsoft Learn](https://learn.microsoft.com/azure/ai-foundry/openai/how-to/create-resource?pivots=web-portal) para criar um recurso Azure OpenAI e um modelo. Selecione o DALL-E 3 como modelo.

## Crie o app

1. Crie um arquivo _.env_ com o seguinte conteúdo:

   ```text
   AZURE_OPENAI_ENDPOINT=<your endpoint>
   AZURE_OPENAI_API_KEY=<your key>
   AZURE_OPENAI_DEPLOYMENT="dall-e-3"
   ```

   Localize essas informações no Portal Azure OpenAI Foundry para o seu recurso, na seção "Deployments".

1. Liste as bibliotecas acima em um arquivo chamado _requirements.txt_ da seguinte forma:

   ```text
   python-dotenv
   openai
   pillow
   requests
   ```

1. Em seguida, crie um ambiente virtual e instale as bibliotecas:

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```

   Para Windows, use os seguintes comandos para criar e ativar o ambiente virtual:

   ```bash
   python3 -m venv venv
   venv\Scripts\activate.bat
   ```

1. Adicione o código abaixo em um arquivo chamado _app.py_:

    ```python
    import openai
    import os
    import requests
    from PIL import Image
    import dotenv
    from openai import OpenAI, AzureOpenAI
    
    # importa o dotenv
    dotenv.load_dotenv()
    
    # configura o cliente do serviço Azure OpenAI
    client = AzureOpenAI(
      azure_endpoint=os.environ["AZURE_OPENAI_ENDPOINT"],
      api_key=os.environ['AZURE_OPENAI_API_KEY'],
      api_version="2024-02-01"
      )
    try:
        # Cria uma imagem usando a API de geração de imagens
        generation_response = client.images.generate(
                                prompt='Bunny on horse, holding a lollipop, on a foggy meadow where it grows daffodils',
                                size='1024x1024', n=1,
                                model=os.environ['AZURE_OPENAI_DEPLOYMENT']
                              )

        # Define o diretório para armazenar a imagem
        image_dir = os.path.join(os.curdir, 'images')

        # Se o diretório não existir, cria-o
        if not os.path.isdir(image_dir):
            os.mkdir(image_dir)

        # Inicializa o caminho da imagem (o tipo de arquivo deve ser png)
        image_path = os.path.join(image_dir, 'generated-image.png')

        # Recupera a imagem gerada
        image_url = generation_response.data[0].url  # extrai a URL da imagem da resposta
        generated_image = requests.get(image_url).content  # faz o download da imagem
        with open(image_path, "wb") as image_file:
            image_file.write(generated_image)

        # Exibe a imagem no visualizador padrão
        image = Image.open(image_path)
        image.show()

    # captura exceções
    except openai.InvalidRequestError as err:
        print(err)
    ```

Vamos explicar este código:

- Primeiro, importamos as bibliotecas que precisamos, incluindo a biblioteca OpenAI, a biblioteca dotenv, a biblioteca requests e a biblioteca Pillow.

  ```python
  import openai
  import os
  import requests
  from PIL import Image
  import dotenv
  ```

- Em seguida, carregamos as variáveis de ambiente do arquivo _.env_.

  ```python
  # importa o dotenv
  dotenv.load_dotenv()
  ```

- Depois disso, configuramos o cliente do serviço Azure OpenAI.

  ```python
  # Obtem o endpoint e a chave das variáveis de ambiente
  client = AzureOpenAI(
      azure_endpoint=os.environ["AZURE_OPENAI_ENDPOINT"],
      api_key=os.environ['AZURE_OPENAI_API_KEY'],
      api_version="2024-02-01"
      )
  ```

- Em seguida, geramos a imagem:

  ```python
  # Cria uma imagem usando a API de geração de imagens
  generation_response = client.images.generate(
                        prompt='Bunny on horse, holding a lollipop, on a foggy meadow where it grows daffodils',
                        size='1024x1024', n=1,
                        model=os.environ['AZURE_OPENAI_DEPLOYMENT']
                      )
  ```

  O código acima responde com um objeto JSON que contém a URL da imagem gerada. Podemos usar essa URL para baixar a imagem e salvá-la em um arquivo.

- Por fim, abrimos a imagem e usamos o visualizador de imagens padrão para exibí-la:

  ```python
  image = Image.open(image_path)
  image.show()
  ```

### Mais detalhes sobre a geração da imagem

Vamos observar o código que gera a imagem em mais detalhes:

   ```python
     generation_response = client.images.generate(
                               prompt='Bunny on horse, holding a lollipop, on a foggy meadow where it grows daffodils',
                               size='1024x1024', n=1,
                               model=os.environ['AZURE_OPENAI_DEPLOYMENT']
                           )
   ```

- **prompt** é o prompt de texto que é usado para gerar a imagem. Neste caso, estamos usando o prompt "Bunny on horse, holding a lollipop, on a foggy meadow where it grows daffodils".
- **size** é o tamanho da imagem que será gerada. Neste caso, estamos gerando uma imagem com 1024x1024 pixels.
- **n** é o número de imagens que serão geradas. Neste caso, estamos gerando duas imagens.
- **temperature** é um parâmetro que controla a aleatoriedade da saída de um modelo de IA Generativa. A temperatura varia de 0 a 1, onde 0 significa que a saída é determinística e 1 significa que a saída é aleatória. O valor padrão é 0.7.

Há mais coisas que você pode fazer com imagens, e vamos cobrir isso na próxima seção.

## Capacidades adicionais de geração de imagem

Até agora você viu como gerar uma imagem usando poucas linhas em Python. No entanto, há mais coisas que você pode fazer com imagens.

Você também pode fazer o seguinte:

- **Realizar edições**. Ao fornecer uma imagem existente, uma máscara e um prompt, você pode alterar uma imagem. Por exemplo, você pode adicionar algo a uma parte da imagem. Imagine nossa imagem do coelho; você pode adicionar um chapéu ao coelho. Para fazer isso, forneça a imagem, uma máscara (que identifica a parte da área a ser alterada) e um prompt de texto dizendo o que deve ser feito.
> Observação: isso não é suportado no DALL-E 3.
 
Aqui está um exemplo usando GPT Image:

   ```python
   response = client.images.edit(
       model="gpt-image-1",
       image=open("sunlit_lounge.png", "rb"),
       mask=open("mask.png", "rb"),
       prompt="A sunlit indoor lounge area with a pool containing a flamingo"
   )
   image_url = response.data[0].url
   ```

  A imagem base conteria apenas o lounge com piscina, mas a imagem final teria um flamingo:

<div style="display: flex; justify-content: space-between; align-items: center; margin: 20px 0;">
  <img src="./images/sunlit_lounge.png" style="width: 30%; max-width: 200px; height: auto;">
  <img src="./images/mask.png" style="width: 30%; max-width: 200px; height: auto;">
  <img src="./images/sunlit_lounge_result.png" style="width: 30%; max-width: 200px; height: auto;">
</div>


- **Criar variações**. A ideia é pegar uma imagem existente e pedir que sejam criadas variações. Para criar uma variação, você fornece uma imagem e um prompt de texto e usa um código como este:

  ```python
  response = openai.Image.create_variation(
    image=open("bunny-lollipop.png", "rb"),
    n=1,
    size="1024x1024"
  )
  image_url = response['data'][0]['url']
  ```

  > Observação: isso é suportado apenas pela OpenAI.

## Temperatura

Temperatura é um parâmetro que controla a aleatoriedade da saída de um modelo de IA Generativa. A temperatura varia de 0 a 1, onde 0 significa que a saída é determinística e 1 significa que a saída é aleatória. O valor padrão é 0.7.

Vamos ver um exemplo de como a temperatura funciona, executando este prompt duas vezes:

> Prompt: "Bunny on horse, holding a lollipop, on a foggy meadow where it grows daffodils"

![Bunny on a horse holding a lollipop, version 1](./images/v1-generated-image.png)

Agora vamos executar o mesmo prompt apenas para ver que não obteremos a mesma imagem duas vezes:

![Generated image of bunny on horse](./images/v2-generated-image.png)

Como você pode ver, as imagens são semelhantes, mas não idênticas. Vamos tentar alterar o valor da temperatura para 0.1 e ver o que acontece:

```python
 generation_response = client.images.create(
        prompt='Bunny on horse, holding a lollipop, on a foggy meadow where it grows daffodils',    # Enter your prompt text here
        size='1024x1024',
        n=2
    )
```

### Alterando a temperatura

Então vamos tentar tornar a resposta mais determinística. Podemos observar nas duas imagens que geramos que na primeira imagem há um coelho e na segunda imagem há um cavalo, então as imagens variam bastante.

Vamos, portanto, mudar nosso código e definir a temperatura como 0, assim:

```python
generation_response = client.images.create(
        prompt='Bunny on horse, holding a lollipop, on a foggy meadow where it grows daffodils',    # Enter your prompt text here
        size='1024x1024',
        n=2,
        temperature=0
    )
```

Agora, quando você executar este código, obterá estas duas imagens:

- ![Temperature 0, v1](./images/v1-temp-generated-image.png)
- ![Temperature 0 , v2](./images/v2-temp-generated-image.png)

Aqui você pode ver claramente como as imagens se parecem mais entre si.

## Como definir limites para sua aplicação com metaprompts

Com nosso demo, já podemos gerar imagens para nossos clientes. No entanto, precisamos criar alguns limites para nossa aplicação.

Por exemplo, não queremos gerar imagens que não sejam seguras para o trabalho ou que não sejam apropriadas para crianças.

Podemos fazer isso com _metaprompts_. Metaprompts são prompts de texto usados para controlar a saída de um modelo de IA Generativa. Por exemplo, podemos usar metaprompts para controlar a saída e garantir que as imagens geradas sejam seguras para o trabalho ou apropriadas para crianças.

### Como isso funciona?

Agora, como funcionam os metaprompts?

Metaprompts são prompts de texto usados para controlar a saída de um modelo de IA Generativa; eles são posicionados antes do prompt de texto e são usados para controlar a saída do modelo e incorporados em aplicações para controlar essa saída. Eles encapsulam a entrada do prompt e a entrada do metaprompt em um único prompt de texto.

Um exemplo de metaprompt seria o seguinte:

```text
You are an assistant designer that creates images for children.

The image needs to be safe for work and appropriate for children.

The image needs to be in color.

The image needs to be in landscape orientation.

The image needs to be in a 16:9 aspect ratio.

Do not consider any input from the following that is not safe for work or appropriate for children.

(Input)

```

Agora, vamos ver como podemos usar metaprompts em nosso demo.

```python
disallow_list = "swords, violence, blood, gore, nudity, sexual content, adult content, adult themes, adult language, adult humor, adult jokes, adult situations, adult"

meta_prompt =f"""You are an assistant designer that creates images for children.

The image needs to be safe for work and appropriate for children.

The image needs to be in color.

The image needs to be in landscape orientation.

The image needs to be in a 16:9 aspect ratio.

Do not consider any input from the following that is not safe for work or appropriate for children.
{disallow_list}
"""

prompt = f"{meta_prompt}
Create an image of a bunny on a horse, holding a lollipop"

# TODO add request to generate image
```

A partir do prompt acima, você pode ver como todas as imagens criadas consideram o metaprompt.

## Atividade - vamos habilitar os estudantes

Apresentamos a Edu4All no início desta lição. Agora é hora de permitir que os estudantes gerem imagens para suas avaliações.

Os estudantes criarão imagens para suas avaliações contendo monumentos; quais monumentos serão definidos pelos próprios alunos. Os estudantes são incentivados a usar sua criatividade para colocar esses monumentos em diferentes contextos.

## Solução

Aqui está uma possível solução:

```python
import openai
import os
import requests
from PIL import Image
import dotenv
from openai import AzureOpenAI
# importa dotenv
dotenv.load_dotenv()

# Obtem o endpoint e a chave das variáveis de ambiente
client = AzureOpenAI(
  azure_endpoint=os.environ["AZURE_OPENAI_ENDPOINT"],
  api_key=os.environ['AZURE_OPENAI_API_KEY'],
  api_version="2024-02-01"
  )


disallow_list = "swords, violence, blood, gore, nudity, sexual content, adult content, adult themes, adult language, adult humor, adult jokes, adult situations, adult"

meta_prompt = f"""You are an assistant designer that creates images for children.

The image needs to be safe for work and appropriate for children.

The image needs to be in color.

The image needs to be in landscape orientation.

The image needs to be in a 16:9 aspect ratio.

Do not consider any input from the following that is not safe for work or appropriate for children.
{disallow_list}
"""

prompt = f"""{meta_prompt}
Generate monument of the Arc of Triumph in Paris, France, in the evening light with a small child holding a Teddy looks on.
"""

try:
    # Cria uma imagem usando a API de geração de imagens
    generation_response = client.images.generate(
        prompt=prompt,    # Enter your prompt text here
        size='1024x1024',
        n=1,
    )
    # Define o diretório para armazenar a imagem
    image_dir = os.path.join(os.curdir, 'images')

    # Se o diretório não existir, cria-o
    if not os.path.isdir(image_dir):
        os.mkdir(image_dir)

    # Inicializa o caminho da imagem (o tipo de arquivo deve ser png)
    image_path = os.path.join(image_dir, 'generated-image.png')

    # Recupera a imagem gerada
    image_url = generation_response.data[0].url  # extrai a URL da imagem da resposta
    generated_image = requests.get(image_url).content  # faz o download da imagem
    with open(image_path, "wb") as image_file:
        image_file.write(generated_image)

    # Exibe a imagem no visualizador padrão
    image = Image.open(image_path)
    image.show()

# captura exceções
except openai.BadRequestError as err:
    print(err)
```

## Ótimo trabalho! Continue aprendendo

Após concluir esta lição, confira nossa [coleção de aprendizado de IA Generativa](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) para continuar evoluindo seus conhecimentos em IA Generativa!

Vá para a Lição 10, onde veremos como [construir aplicações de IA com low-code](../10-building-low-code-ai-applications/README.md?WT.mc_id=academic-105485-koreyst)

