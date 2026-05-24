# Configuração Local 🖥️

**Use este guia se preferir executar tudo no seu próprio laptop.**   
Você tem dois caminhos: **(A) Python nativo + virtualenv** ou **(B) Dev Container do VS Code com Docker**.  
Escolha o que parecer mais fácil — ambos levam às mesmas lições.

## 1.  Pré-requisitos

| Ferramenta          | Versão / Observações                                                                 |
|---------------------|--------------------------------------------------------------------------------------|
| **Python**          | 3.10 + (obtenha em <https://python.org>)                                             |
| **Git**             | Versão mais recente (vem com Xcode / Git para Windows / gerenciador de pacotes Linux)|
| **VS Code**         | Opcional, mas recomendado <https://code.visualstudio.com>                            |
| **Docker Desktop**  | *Somente* para a Opção B. Instalação gratuita: <https://docs.docker.com/desktop/>   |

> 💡 **Dica** – Verifique as ferramentas em um terminal:  
> `python --version`, `git --version`, `docker --version`, `code --version`  

## 2.  Opção A – Python Nativo (mais rápido)

### Passo 1  Clone este repositório

```bash
git clone https://github.com/<seu-github>/generative-ai-for-beginners
cd generative-ai-for-beginners
```

### Passo 2 Crie e ative um ambiente virtual

```bash
python -m venv .venv          # crie um
source .venv/bin/activate     # macOS / Linux
.\.venv\Scripts\activate      # Windows PowerShell
```

✅ O prompt deve agora começar com (.venv) — isso significa que você está dentro do ambiente.

### Passo 3 Instale as dependências

```bash
pip install -r requirements.txt
```

Vá para a Seção 3 em [Chaves de API](#3-adicione-suas-chaves-de-api)

## 2. Opção B – Dev Container do VS Code (Docker)

Configuramos este repositório e curso com um [dev container](https://containers.dev?WT.mc_id=academic-105485-koreyst) que traz um runtime Universal capaz de suportar desenvolvimento em Python3, .NET, Node.js e Java. A configuração relacionada está definida no arquivo `devcontainer.json` localizado na pasta `.devcontainer/` na raiz deste repositório.

>**Por que escolher esta opção?**
>Ambiente idêntico ao Codespaces; sem deriva de dependências.

### Passo 0 Instale os extras

Docker Desktop – confirme que `docker --version` funciona.  
Extensão VS Code Remote – Containers (ID: ms-vscode-remote.remote-containers).

### Passo 1 Abra o repositório no VS Code

File ▸ Open Folder…  → generative-ai-for-beginners

O VS Code detecta a pasta `.devcontainer/` e exibe um prompt.

### Passo 2 Reabra no container

Clique em “Reopen in Container”. O Docker constrói a imagem (≈ 3 min na primeira vez).  
Quando o prompt do terminal aparecer, você estará dentro do container.

## 2.  Opção C – Miniconda

[Miniconda](https://conda.io/en/latest/miniconda.html?WT.mc_id=academic-105485-koreyst) é um instalador leve para instalar [Conda](https://docs.conda.io/en/latest?WT.mc_id=academic-105485-koreyst), Python e alguns pacotes.
O Conda é um gerenciador de pacotes que facilita a criação e a troca entre diferentes [**ambientes virtuais**](https://docs.python.org/3/tutorial/venv.html?WT.mc_id=academic-105485-koreyst) e pacotes Python. Ele também é útil para instalar pacotes que não estão disponíveis via `pip`.

### Passo 0  Instale o Miniconda

Siga o [guia de instalação do Miniconda](https://docs.anaconda.com/free/miniconda/#quick-command-line-install?WT.mc_id=academic-105485-koreyst) para configurá-lo.

```bash
conda --version
```

### Passo 1 Crie um ambiente virtual

Crie um novo arquivo de ambiente (*environment.yml*). Se você estiver usando Codespaces, crie dentro do diretório `.devcontainer`, ou seja, `.devcontainer/environment.yml`.

### Passo 2  Preencha o arquivo de ambiente

Adicione o trecho abaixo ao seu `environment.yml`

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

### Passo 3 Crie seu ambiente Conda

Execute os comandos abaixo no terminal:

```bash 
conda env create --name ai4beg --file .devcontainer/environment.yml # caminho .devcontainer se aplica apenas a configurações Codespaces
conda activate ai4beg
```

Consulte o [guia de ambientes Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html?WT.mc_id=academic-105485-koreyst) se tiver problemas.

## 2  Opção D – Jupyter / Jupyter Lab clássico (no navegador)

> **Para quem é esta opção?**  
> Qualquer pessoa que prefira a interface clássica do Jupyter ou queira executar notebooks sem usar o VS Code.  

### Passo 1  Verifique se o Jupyter está instalado

Para iniciar o Jupyter localmente, vá ao terminal/linha de comando, navegue até a pasta do curso e execute:

```bash
jupyter notebook
```

ou

```bash
jupyterhub
```

Isso iniciará uma instância do Jupyter e a URL para acessá-la será exibida na janela do terminal.

Depois de acessar a URL, você deverá ver o índice do curso e poderá navegar para qualquer arquivo `*.ipynb`. Por exemplo, `08-building-search-applications/python/oai-solution.ipynb`.

## 3. Adicione suas chaves de API

Manter suas chaves de API seguras é importante ao construir qualquer tipo de aplicação. Recomendamos não armazenar chaves de API diretamente no código. Cometer esses dados em um repositório público pode causar problemas de segurança e até custos indesejados se usados por alguém mal-intencionado.
Aqui está um guia passo a passo para criar um arquivo `.env` para Python e adicionar o `GITHUB_TOKEN`:

1. **Navegue até o diretório do seu projeto**: Abra o terminal ou prompt de comando e vá para a raiz do projeto onde deseja criar o arquivo `.env`.

   ```bash
   cd caminho/para/seu/projeto
   ```

2. **Crie o arquivo `.env`**: Use seu editor de texto preferido para criar um novo arquivo chamado `.env`. Se estiver usando a linha de comando, pode usar `touch` (em sistemas Unix) ou `echo` (no Windows):

   Sistemas Unix:

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

5. **Instale o `python-dotenv`**: Se ainda não instalou, será necessário instalar o pacote `python-dotenv` para carregar variáveis de ambiente do arquivo `.env` em sua aplicação Python. Você pode instalar com `pip`:

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

🔐 Nunca comite o `.env` — ele já está no `.gitignore`.
As instruções completas de provedores estão em [`providers.md`](03-providers.md).

## 4. O que vem a seguir?

| Eu quero…           | Ir para…                                                                 |
|---------------------|--------------------------------------------------------------------------|
| Começar a Lição 1   | [`01-introduction-to-genai`](../01-introduction-to-genai/README.md)      |
| Configurar um provedor de LLM | [`providers.md`](03-providers.md)                                       |
| Conhecer outros aprendizes | [Participe do nosso Discord](https://aka.ms/genai-discord?WT.mc_id=academic-105485-koreyst)   |

## 5. Solução de problemas

| Sintoma                                   | Correção                                                          |
|-------------------------------------------|-------------------------------------------------------------------|
| `python not found`                        | Adicione Python ao PATH ou reabra o terminal após a instalação   |
| `pip` cannot build wheels (Windows)       | `pip install --upgrade pip setuptools wheel` e tente novamente.    |
| `ModuleNotFoundError: dotenv`             | Execute `pip install -r requirements.txt` (o ambiente não foi instalado). |
| Docker build fails *No space left*        | Docker Desktop ▸ *Settings* ▸ *Resources* → aumente o espaço em disco. |
| O VS Code continua solicitando reabrir  | Você pode ter ambas as opções ativas; escolha uma (venv **ou** container)|
| Erros OpenAI 401 / 429                    | Verifique o valor de `OPENAI_API_KEY` / limites de taxa de requisição. |
| Erros usando Conda                         | Instale as bibliotecas Microsoft AI usando `conda install -c microsoft azure-ai-ml`|

