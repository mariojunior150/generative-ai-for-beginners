# Configuração Local 🖥️

**Use este guia se preferir executar tudo no seu próprio laptop.**  
Você tem dois caminhos: **(A) Python nativo + virtualenv** ou **(B) Contêiner de Desenvolvimento do VS Code com Docker**.  
Escolha o que achar mais fácil — ambos levam às mesmas lições.

## 1. Pré-requisitos

| Ferramenta         | Versão / Observações                                                                 |
|--------------------|--------------------------------------------------------------------------------------|
| **Python**         | 3.10+ (obtenha em https://python.org)                                                |
| **Git**            | Última versão (vem com Xcode / Git para Windows / gerenciador de pacotes do Linux)  |
| **VS Code**        | Opcional, mas recomendado https://code.visualstudio.com                              |
| **Docker Desktop** | *Somente* para a Opção B. Instalação gratuita: https://docs.docker.com/desktop/     |

> 💡 **Dica** – Verifique as ferramentas no terminal:  
> `python --version`, `git --version`, `docker --version`, `code --version`

## 2. Opção A – Python Nativo (mais rápido)

### Passo 1 Clone este repositório

```bash
git clone https://github.com/<your-github>/generative-ai-for-beginners
cd generative-ai-for-beginners
```

### Passo 2 Crie e ative um ambiente virtual

```bash
python -m venv .venv          # crie um
source .venv/bin/activate     # macOS / Linux
.\.venv\Scripts\activate      # Windows PowerShell
```

✅ O prompt deve começar com (.venv) — isso significa que você está dentro do ambiente virtual.

### Passo 3 Instale as dependências

```bash
pip install -r requirements.txt
```

Vá para a Seção 3 sobre [chaves de API](#3-add-your-api-keys)

## 2. Opção B – Contêiner de Desenvolvimento do VS Code (Docker)

Configuramos este repositório e o curso com um [container de desenvolvimento](https://containers.dev?WT.mc_id=academic-105485-koreyst) que possui um runtime Universal capaz de suportar desenvolvimento em Python3, .NET, Node.js e Java. A configuração relacionada está definida no arquivo `devcontainer.json` localizado na pasta `.devcontainer/` na raiz deste repositório.

> **Por que escolher isso?**  
> Ambiente idêntico ao Codespaces; evita divergência de dependências.

### Passo 0 Instale os extras

Docker Desktop – confirme com ```docker --version```.  
Extensão Remote – Containers do VS Code (ID: ms-vscode-remote.remote-containers).

### Passo 1 Abra o repositório no VS Code

Arquivo ▸ Open Folder… → generative-ai-for-beginners

O VS Code detecta `.devcontainer/` e exibe um prompt.

### Passo 2 Reabrir no contêiner

Clique em “Reopen in Container”. O Docker constrói a imagem (≈ 3 min na primeira vez).  
Quando o prompt do terminal aparecer, você estará dentro do contêiner.

## 2. Opção C – Miniconda

[Miniconda](https://conda.io/en/latest/miniconda.html?WT.mc_id=academic-105485-koreyst) é um instalador leve para instalar o [Conda](https://docs.conda.io/en/latest?WT.mc_id=academic-105485-koreyst), Python e alguns pacotes. O Conda é um gerenciador de pacotes que facilita criar e alternar entre ambientes virtuais e pacotes. Também é útil para instalar pacotes que não estão disponíveis via `pip`.

### Passo 0 Instale o Miniconda

Siga o [guia de instalação do Miniconda](https://docs.anaconda.com/free/miniconda/#quick-command-line-install?WT.mc_id=academic-105485-koreyst).

```bash
conda --version
```

### Passo 1 Crie um ambiente virtual

Crie um novo arquivo de ambiente (*environment.yml*). Se estiver seguindo usando Codespaces, crie-o dentro de `.devcontainer` como `.devcontainer/environment.yml`.

### Passo 2 Preencha seu arquivo de ambiente

Adicione o seguinte trecho ao seu `environment.yml`:

```yml
name: <environment-name>
channels:
 - defaults
 - microsoft
dependencies:
- python=<python-version>
- openai
- python-dotenv
- pip
- pip:
    - azure-ai-ml
```

### Passo 3 Crie seu ambiente Conda

Execute os comandos abaixo no terminal/linha de comando:

```bash
conda env create --name ai4beg --file .devcontainer/environment.yml # .devcontainer sub path applies to only Codespace setups
conda activate ai4beg
```

Consulte o [Guia de ambientes Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html?WT.mc_id=academic-105485-koreyst) se encontrar problemas.

## 2 Opção D – Jupyter / Jupyter Lab Clássico (no navegador)

> **Para quem é isso?**  
> Para quem prefere a interface clássica do Jupyter ou quer executar notebooks sem o VS Code.

### Passo 1 Certifique-se de que o Jupyter está instalado

Para iniciar o Jupyter localmente, abra um terminal, navegue até o diretório do curso e execute:

```bash
jupyter notebook
```

ou

```bash
jupyterhub
```

Isto iniciará uma instância do Jupyter e a URL de acesso será exibida no terminal.  
Ao acessar a URL, você verá o índice do curso e poderá navegar por qualquer arquivo `*.ipynb`. Por exemplo, `08-building-search-applications/python/oai-solution.ipynb`.

## 3. Adicione Suas Chaves de API

Manter suas chaves de API seguras é importante ao construir aplicações. Recomendamos não armazenar chaves diretamente no código. Cometer essas informações em um repositório público pode causar problemas de segurança e custos indesejados se forem usadas por terceiros.
A seguir, um passo a passo para criar um arquivo `.env` para Python e adicionar o `GITHUB_TOKEN`:

1. **Navegue até o diretório do projeto**: Abra o terminal e vá até a raiz do projeto onde quer criar o `.env`.

   ```bash
   cd path/to/your/project
   ```

2. **Crie o arquivo `.env`**: Use seu editor preferido para criar um novo arquivo chamado `.env`. No terminal, pode usar `touch` (Unix) ou `echo` (Windows):

   Sistemas Unix:

   ```bash
   touch .env
   ```

   Windows:

   ```cmd
   echo . > .env
   ```

3. **Edite o arquivo `.env`**: Abra `.env` em um editor (ex.: VS Code) e adicione a linha abaixo, substituindo `your_github_token_here` pela sua token do GitHub:

   ```env
   GITHUB_TOKEN=your_github_token_here
   ```

4. **Salve o arquivo**: Salve e feche o editor.

5. **Instale `python-dotenv`**: Se ainda não instalou, instale o pacote `python-dotenv` para carregar variáveis do `.env` em aplicações Python:

   ```bash
   pip install python-dotenv
   ```

6. **Carregue variáveis no seu script Python**: No seu script, use `python-dotenv` para carregar as variáveis do `.env`:

   ```python
   from dotenv import load_dotenv
   import os

   # Carrega variáveis do arquivo .env
   load_dotenv()

   # Acessa a variável GITHUB_TOKEN
   github_token = os.getenv("GITHUB_TOKEN")

   print(github_token)
   ```

🔐 Nunca comite o `.env` — ele já está no `.gitignore`.  
Instruções completas sobre provedores estão em [`providers.md`](03-providers.md).

## 4. O que vem a seguir?

| Quero…                  | Ir para…                                                                  |
|-------------------------|---------------------------------------------------------------------------|
| Começar a Lição 1       | [`01-introduction-to-genai`](../01-introduction-to-genai/README.md)      |
| Configurar um provedor LLM | [`providers.md`](03-providers.md)                                      |
| Conhecer outros aprendizes | [Participe do nosso Discord](https://aka.ms/genai-discord?WT.mc_id=academic-105485-koreyst) |

## 5. Solução de Problemas

| Sintoma                                   | Correção                                                          |
|-------------------------------------------|-------------------------------------------------------------------|
| `python not found`                        | Adicione o Python ao PATH ou reabra o terminal após a instalação  |
| `pip` não consegue buildar wheels (Windows)| `pip install --upgrade pip setuptools wheel` e tente novamente    |
| `ModuleNotFoundError: dotenv`             | Rode `pip install -r requirements.txt` (o ambiente não foi instalado) |
| Falha no build do Docker *No space left*  | Docker Desktop ▸ *Settings* ▸ *Resources* → aumente o espaço em disco. |
| VS Code continuar pedindo para reabrir    | Talvez você tenha as duas opções ativas; escolha uma (venv **ou** contêiner) |
| Erros OpenAI 401 / 429                    | Verifique o valor de `OPENAI_API_KEY` / limites de taxa de requisições. |
| Erros com Conda                            | Instale bibliotecas Microsoft AI com `conda install -c microsoft azure-ai-ml` |
