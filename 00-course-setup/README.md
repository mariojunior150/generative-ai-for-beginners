# Começando com este curso

Estamos muito animados por você começar este curso e ver no que se inspirará para construir com IA Generativa!

Para garantir seu sucesso, esta página descreve as etapas de configuração, requisitos técnicos e onde obter ajuda, se necessário.

## Etapas de Configuração

Para começar a fazer este curso, você precisará completar as etapas abaixo.

### 1. Faça um fork deste repositório

[Fork neste repositório inteiro](https://github.com/microsoft/generative-ai-for-beginners/fork?WT.mc_id=academic-105485-koreyst) para a sua própria conta do GitHub para poder alterar qualquer código e completar os desafios. Você também pode [dar uma estrela (🌟) neste repo](https://docs.github.com/en/get-started/exploring-projects-on-github/saving-repositories-with-stars?WT.mc_id=academic-105485-koreyst) para encontrá-lo e repositórios relacionados com mais facilidade.

### 2. Crie um codespace

Para evitar problemas de dependência ao executar o código, recomendamos executar este curso em um [GitHub Codespaces](https://github.com/features/codespaces?WT.mc_id=academic-105485-koreyst).

No seu fork: **Code -> Codespaces -> New on main**

![Caixa de diálogo mostrando botões para criar um codespace](./images/who-will-pay.webp?WT.mc_id=academic-105485-koreyst)

#### 2.1 Adicione um secret

1. ⚙️ Ícone de engrenagem -> Command Palette -> Codespaces : Manage user secret -> Add a new secret.
2. Nome: OPENAI_API_KEY, cole sua chave, Salvar.

### 3. O que vem a seguir?

| Eu quero…            | Ir para…                                                                 |
|----------------------|-------------------------------------------------------------------------|
| Começar a Lição 1    | [`01-introduction-to-genai`](../01-introduction-to-genai/README.md)     |
| Trabalhar offline    | [`setup-local.md`](02-setup-local.md)                                   |
| Configurar um provedor de LLM | [`providers.md`](03-providers.md)                                   |
| Conhecer outros aprendizes | [Participe do nosso Discord](https://aka.ms/genai-discord?WT.mc_id=academic-105485-koreyst)   |

## Solução de Problemas

| Sintoma                                   | Correção                                                          |
|-------------------------------------------|-------------------------------------------------------------------|
| Container travado por mais de 10 min      | **Codespaces ➜ “Rebuild Container”**                               |
| `python: command not found`               | O terminal não foi anexado; clique **+** ➜ *bash*                  |
| `401 Unauthorized` do OpenAI              | `OPENAI_API_KEY` incorreto ou expirado                             |
| VS Code mostra “Dev container mounting…”   | Atualize a guia do navegador — às vezes o Codespaces perde conexão  |
| Kernel do notebook ausente                | Menu do notebook ➜ **Kernel ▸ Select Kernel ▸ Python 3**           |

   Sistemas baseados em Unix:

   ```bash
   touch .env
   ```

   Windows:

   ```cmd
   echo . > .env
   ```

3. **Edite o arquivo `.env`**: Abra o arquivo `.env` em um editor de texto (por exemplo, VS Code, Notepad++ ou qualquer outro editor). Adicione a linha abaixo ao arquivo, substituindo `your_github_token_here` pelo seu token do GitHub:

   ```env
   GITHUB_TOKEN=your_github_token_here
   ```

4. **Salve o arquivo**: Salve as alterações e feche o editor de texto.

5. **Instale o `python-dotenv`**: Se ainda não instalou, você precisará instalar o pacote `python-dotenv` para carregar variáveis de ambiente do arquivo `.env` em sua aplicação Python. Você pode instalar com `pip`:

   ```bash
   pip install python-dotenv
   ```

6. **Carregue as variáveis de ambiente no seu script Python**: No seu script Python, use o pacote `python-dotenv` para carregar as variáveis de ambiente do arquivo `.env`:

   ```python
   from dotenv import load_dotenv
   import os

   # Carrega variáveis de ambiente do arquivo .env
   load_dotenv()

   # Acessa a variável GITHUB_TOKEN
   github_token = os.getenv("GITHUB_TOKEN")

   print(github_token)
   ```

Pronto! Você criou com sucesso um arquivo `.env`, adicionou seu token do GitHub e carregou-o na sua aplicação Python.

## Como executar localmente no seu computador

Para executar o código localmente no seu computador, você precisará ter alguma versão do [Python instalado](https://www.python.org/downloads/?WT.mc_id=academic-105485-koreyst).

Para usar o repositório, você precisa cloná-lo:

```shell
git clone https://github.com/microsoft/generative-ai-for-beginners
cd generative-ai-for-beginners
```

Depois de ter tudo clonado, você pode começar!

## Etapas Opcionais

### Instalando o Miniconda

[Miniconda](https://conda.io/en/latest/miniconda.html?WT.mc_id=academic-105485-koreyst) é um instalador leve para instalar [Conda](https://docs.conda.io/en/latest?WT.mc_id=academic-105485-koreyst), Python e alguns pacotes.
O Conda é um gerenciador de pacotes que facilita configurar e alternar entre diferentes [**ambientes virtuais**](https://docs.python.org/3/tutorial/venv.html?WT.mc_id=academic-105485-koreyst) e pacotes Python. Ele também é útil para instalar pacotes que não estão disponíveis via `pip`.

Você pode seguir o [guia de instalação do Miniconda](https://docs.anaconda.com/free/miniconda/#quick-command-line-install?WT.mc_id=academic-105485-koreyst) para configurá-lo.

Com o Miniconda instalado, você precisa clonar o [repositório](https://github.com/microsoft/generative-ai-for-beginners/fork?WT.mc_id=academic-105485-koreyst) (se ainda não tiver feito isso).

Em seguida, crie um ambiente virtual. Para fazer isso com o Conda, crie um novo arquivo de ambiente (_environment.yml_). Se estiver usando Codespaces, crie-o dentro do diretório `.devcontainer`, ou seja, `.devcontainer/environment.yml`.

Preencha o seu arquivo de ambiente com o trecho abaixo:

```yml
name: <nome-do-ambiente>
channels:
  - defaults
  - microsoft
dependencies:
  - python=<versao-do-python>
  - openai
  - python-dotenv
  - pip
  - pip:
      - azure-ai-ml
```

Se você estiver recebendo erros ao usar o Conda, pode instalar manualmente as bibliotecas Microsoft AI com o comando abaixo em um terminal:

```
conda install -c microsoft azure-ai-ml
```

O arquivo de ambiente especifica as dependências de que precisamos. `<nome-do-ambiente>` é o nome que você deseja usar para seu ambiente Conda e `<versao-do-python>` é a versão do Python que você deseja usar, por exemplo `3` para a versão principal mais recente.

Com isso pronto, crie seu ambiente Conda executando os comandos abaixo no terminal:

```bash
conda env create --name ai4beg --file .devcontainer/environment.yml # o caminho .devcontainer se aplica apenas a configurações Codespaces
conda activate ai4beg
```

Consulte o [guia de ambientes Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html?WT.mc_id=academic-105485-koreyst) se encontrar problemas.

### Usando o Visual Studio Code com a extensão de suporte a Python

Recomendamos usar o editor [Visual Studio Code (VS Code)](https://code.visualstudio.com/?WT.mc_id=academic-105485-koreyst) com a extensão de suporte a [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python&WT.mc_id=academic-105485-koreyst) instalada para este curso. Esta recomendação é opcional, não obrigatória.

> **Observação**: Ao abrir o repositório do curso no VS Code, você tem a opção de configurar o projeto dentro de um container. Isso é possível graças ao diretório especial [`.devcontainer`](https://code.visualstudio.com/docs/devcontainers/containers?itemName=ms-python.python&WT.mc_id=academic-105485-koreyst) encontrado no repositório do curso. Mais sobre isso depois.

> **Observação**: Depois de clonar e abrir o diretório no VS Code, ele sugerirá automaticamente que você instale a extensão de suporte a Python.

> **Observação**: Se o VS Code sugerir que você reabra o repositório em um container, recuse essa solicitação para usar a versão do Python instalada localmente.

### Usando o Jupyter no navegador

Você também pode trabalhar no projeto usando o ambiente [Jupyter](https://jupyter.org?WT.mc_id=academic-105485-koreyst) diretamente no navegador. Tanto o Jupyter clássico quanto o [Jupyter Hub](https://jupyter.org/hub?WT.mc_id=academic-105485-koreyst) oferecem um ambiente de desenvolvimento agradável com recursos como auto-completar, destaque de sintaxe, etc.

Para iniciar o Jupyter localmente, abra o terminal/linha de comando, navegue até o diretório do curso e execute:

```bash
jupyter notebook
```

ou

```bash
jupyterhub
```

Isso iniciará uma instância do Jupyter e a URL de acesso será exibida na janela do terminal.

Depois de acessar a URL, você deverá ver o índice do curso e poderá navegar para qualquer arquivo `*.ipynb`. Por exemplo, `08-building-search-applications/python/oai-solution.ipynb`.

### Executando em um container

Uma alternativa para configurar tudo no seu computador ou no Codespace é usar um [container](<https://en.wikipedia.org/wiki/Containerization_(computing)?WT.mc_id=academic-105485-koreyst>). A pasta especial `.devcontainer` no repositório do curso torna possível ao VS Code configurar o projeto dentro de um container. Fora do Codespaces, isso exigirá a instalação do Docker e, francamente, envolve um pouco de trabalho, então recomendamos essa opção apenas para quem tem experiência com containers.

Uma das melhores maneiras de manter suas chaves de API seguras ao usar o GitHub Codespaces é usar os Secrets do Codespace. Siga o guia de [gerenciamento de secrets no Codespaces](https://docs.github.com/en/codespaces/managing-your-codespaces/managing-secrets-for-your-codespaces?WT.mc_id=academic-105485-koreyst) para saber mais.


## Lições e Requisitos Técnicos

O curso tem 6 lições conceituais e 6 lições de código.

Para as lições de código, usamos o Azure OpenAI Service. Você precisará de acesso ao Azure OpenAI Service e de uma chave de API para executar este código. Você pode se inscrever para obter acesso [completando esta solicitação](https://azure.microsoft.com/products/ai-services/openai-service?WT.mc_id=academic-105485-koreyst).

Enquanto aguarda o processamento da sua solicitação, cada lição de código também inclui um arquivo `README.md` onde você pode ver o código e os resultados.

## Usando o Azure OpenAI Service pela primeira vez

Se esta é a primeira vez que você trabalha com o Azure OpenAI Service, siga este guia sobre como [criar e implantar um recurso Azure OpenAI Service.](https://learn.microsoft.com/azure/ai-services/openai/how-to/create-resource?pivots=web-portal&WT.mc_id=academic-105485-koreyst)

## Usando a API OpenAI pela primeira vez

Se esta é a primeira vez que você usa a API OpenAI, siga o guia sobre como [criar e usar a Interface.](https://platform.openai.com/docs/quickstart?context=pythont&WT.mc_id=academic-105485-koreyst)

## Conheça outros aprendizes

Criamos canais em nosso servidor oficial do [Discord da Comunidade de IA](https://aka.ms/genai-discord?WT.mc_id=academic-105485-koreyst) para você conhecer outros aprendizes. Esta é uma ótima forma de se conectar com outros empreendedores, construtores, estudantes e qualquer pessoa que queira evoluir em IA Generativa.

[![Junte-se ao canal do Discord](https://dcbadge.limes.pink/api/server/ByRwuEEgH4)](https://aka.ms/genai-discord?WT.mc_id=academic-105485-koreyst)

A equipe do projeto também estará neste servidor Discord para ajudar os aprendizes.

## Contribua

Este curso é uma iniciativa open-source. Se você identificar áreas de melhoria ou problemas, crie um [Pull Request](https://github.com/microsoft/generative-ai-for-beginners/pulls?WT.mc_id=academic-105485-koreyst) ou registre um [issue no GitHub](https://github.com/microsoft/generative-ai-for-beginners/issues?WT.mc_id=academic-105485-koreyst).

A equipe do projeto acompanhará todas as contribuições. Contribuir para código aberto é uma excelente forma de construir sua carreira em IA Generativa.

A maioria das contribuições exige que você concorde com um Acordo de Licença de Contribuidor (CLA) declarando que você tem o direito e de fato concede os direitos de uso da sua contribuição. Para mais detalhes, visite o [site do CLA, Contributor License Agreement](https://cla.microsoft.com?WT.mc_id=academic-105485-koreyst).

Importante: ao traduzir texto neste repositório, certifique-se de não usar tradução automática. Vamos verificar as traduções pela comunidade, então traduza apenas se for proficiente no idioma.

Quando você enviar um pull request, um bot de CLA determinará automaticamente se você precisa fornecer um CLA e marcará o PR adequadamente (por exemplo, com label ou comentário). Basta seguir as instruções fornecidas pelo bot. Você precisará fazer isso apenas uma vez para todos os repositórios que usam nosso CLA.

Este projeto adotou o [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct?WT.mc_id=academic-105485-koreyst). Para mais informações, leia o FAQ do Code of Conduct ou entre em contato com [Email opencode](opencode@microsoft.com) para quaisquer perguntas ou comentários adicionais.

## Vamos começar

Agora que você concluiu as etapas necessárias para começar este curso, vamos iniciar com uma [introdução à IA Generativa e LLMs](../01-introduction-to-genai/README.md?WT.mc_id=academic-105485-koreyst).

