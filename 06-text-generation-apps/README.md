# Construindo Aplicativos de Geração de Texto

[![Building Text Generation Applications](./images/06-lesson-banner.png?WT.mc_id=academic-105485-koreyst)](https://youtu.be/0Y5Luf5sRQA?si=t_xVg0clnAI4oUFZ)

> _(Clique na imagem para assistir ao vídeo desta lição)_

Ao longo deste currículo você já viu conceitos centrais como prompts e até a disciplina de “engenharia de prompt”. Muitos serviços e ferramentas (ChatGPT, Office 365, Microsoft Power Platform etc.) aceitam prompts como forma de interação.

Para adicionar essa experiência a um aplicativo, é preciso entender conceitos como prompt, completion e escolher uma biblioteca para integrar com o modelo — é exatamente isso que veremos neste capítulo.

## Introdução

Nesta lição você irá:

- Conhecer a biblioteca `openai` e seus conceitos básicos.
- Construir um aplicativo de geração de texto usando `openai`.
- Aprender a usar parâmetros como `prompt`, `temperature` e tokens para controlar a geração.

## Objetivos de aprendizagem

Ao final desta lição, você será capaz de:

- Explicar o que é um aplicativo de geração de texto.
- Construir um aplicativo de geração de texto usando a biblioteca `openai`.
- Configurar o app para consumir mais ou menos tokens e ajustar a `temperature` para variar a saída.

## O que é um aplicativo de geração de texto?

Aplicativos tradicionais têm algum tipo de interface, por exemplo:

- Interface por comandos: apps de console onde você digita comandos (ex.: `git`).
- Interface gráfica (UI): apps com botões, formulários, campos de texto, opções, etc.

### Limitações de apps por console/UI tradicionais

- São limitados: aceitam apenas comandos ou entradas previstas pelo desenvolvedor.
- Em geral são feitos para uma língua/idioma padrão, a menos que você implemente suporte multilíngue.

### Benefícios dos aplicativos de geração de texto

Apps de geração de texto aceitam linguagem natural — você pode interagir usando frases livres, sem precisar conhecer comandos. Além disso, o modelo tem conhecimento pré-treinado em um grande corpus, o que amplia o alcance das interações além do que um banco de dados local entrega.

### Exemplos de aplicações possíveis

- Chatbot: responde dúvidas sobre sua empresa e produtos.
- Assistente de texto: sumariza textos, extrai insights, gera currículos, etc.
- Assistente de código: com o modelo certo, ajuda a escrever trechos de código (ex.: GitHub Copilot, ChatGPT).

## Como começar?

Para integrar um LLM você normalmente tem duas abordagens:

- Usar uma API: montar requisições HTTP com seu prompt e receber o texto gerado.
- Usar uma biblioteca/SDK: abstrai as chamadas à API e facilita o desenvolvimento.

## Bibliotecas/SDKs

Algumas bibliotecas conhecidas para trabalhar com LLMs:

- `openai`: biblioteca oficial que facilita a conexão com modelos e envio de prompts.
- Bibliotecas de nível mais alto, por exemplo:
  - LangChain (suporta Python)
  - Semantic Kernel (Microsoft — suporta C#, Python e Java)

## Primeiro app usando `openai`

Vamos construir um app simples: quais bibliotecas instalar, como configurar e como gerar texto.

### Instalar `openai`

Usaremos a biblioteca Python `openai`. Instale com pip:

```bash
pip install openai
```

### Criar o recurso (Azure)

Passos básicos:

- Crie uma conta no Azure: https://azure.microsoft.com/free/
- Solicite acesso ao Azure OpenAI: https://learn.microsoft.com/azure/ai-services/openai/overview#how-do-i-get-access-to-azure-openai

> [!NOTE]
> No momento da escrita deste material, o acesso ao Azure OpenAI exige uma solicitação prévia.

- Instale Python: https://www.python.org/
- Crie um recurso do Azure OpenAI (veja o guia de criação de recurso na documentação).

### Localizar chave de API e endpoint

Na seção "Keys and Endpoint" do recurso Azure OpenAI copie o valor da sua chave (Key 1) e o endpoint (API Base).

Recomenda-se manter a chave fora do código, usando variáveis de ambiente, por exemplo:

```bash
export OPENAI_API_KEY='sk-...'
```

### Configuração para Azure

Se estiver usando Azure OpenAI, configure a biblioteca assim:

```python
openai.api_type = 'azure'
openai.api_key = os.environ['OPENAI_API_KEY']
openai.api_version = '2023-05-15'
openai.api_base = os.getenv('API_BASE')
```

Onde `api_base` é o endpoint encontrado no Portal do Azure.

> Observação: `os.getenv` e `os.environ` leem variáveis de ambiente. Use um arquivo `.env` com `python-dotenv` se preferir não exportar variáveis no terminal.

## Gerar texto

Uma forma simples de gerar texto é usar `Completion` (dependendo da versão da API). Exemplo básico:

```python
prompt = "Complete the following: Once upon a time there was a"

completion = openai.Completion.create(model="davinci-002", prompt=prompt)
print(completion.choices[0].text)
```

### Chat completions

Para aplicações tipo chatbot, a API de chat é mais adequada. Exemplo:

```python
import openai

openai.api_key = "sk-..."

completion = openai.ChatCompletion.create(model="gpt-3.5-turbo", messages=[{"role": "user", "content": "Hello world"}])
print(completion.choices[0].message.content)
```

Veremos mais sobre chat em capítulos posteriores.

## Exercício — seu primeiro app de geração de texto

Agora que você sabe configurar `openai`, construa um app de geração de receitas (recipe generator). Siga estes passos:

1. Crie um ambiente virtual e instale `openai`:

```bash
python -m venv venv
source venv/bin/activate
pip install openai
```

No Windows: `venv\Scripts\activate` em vez de `source`.

2. Crie um arquivo `app.py` com este código de base (substitua chaves e endpoint conforme necessário):

```python
import openai

openai.api_key = "<replace this value with your open ai key or Azure OpenAI key>"

openai.api_type = 'azure'
openai.api_version = '2023-05-15'
openai.api_base = "<endpoint found in Azure Portal where your API key is>"
deployment_name = "<deployment name>"

# add your completion code
prompt = "Complete the following: Once upon a time there was a"
messages = [{"role": "user", "content": prompt}]

# make completion
completion = openai.chat.completions.create(model=deployment_name, messages=messages)

# print response
print(completion.choices[0].message.content)
```

Execute e você deverá ver um texto gerado pelo modelo.

## Tipos de prompts para tarefas diferentes

Você pode usar prompts para várias finalidades:

- Gerar um tipo de texto (poema, perguntas de quiz, descrições, etc.).
- Buscar ou explicar conceitos (ex.: "O que significa CORS em desenvolvimento web?").
- Gerar código (expressões regulares, trechos, até programas inteiros).

## Caso prático: gerador de receitas

Suponha que você tem ingredientes em casa e quer ideias de receitas. Um prompt simples:

> "Show me 5 recipes for a dish with the following ingredients: chicken, potatoes, and carrots. Per recipe, list all the ingredients used"

O modelo pode retornar várias receitas com listas de ingredientes. Para adaptar ao que você tem em casa, podemos refinar o prompt:

> "Please remove recipes with garlic as I'm allergic and replace it with something else. Also, please produce a shopping list for the recipes, considering I already have chicken, potatoes and carrots at home."

O resultado pode incluir receitas ajustadas e uma lista de compras filtrada considerando os ingredientes já disponíveis.

## Exercício prático — implementar um gerador de receitas

1. Use o `app.py` existente como ponto de partida.
2. Localize a variável `prompt` e substitua por:

```python
prompt = "Show me 5 recipes for a dish with the following ingredients: chicken, potatoes, and carrots. Per recipe, list all the ingredients used"
```

3. Execute o código e observe a saída (lembre-se que o modelo é não determinístico).

4. Para melhorar, torne os ingredientes e o número de receitas configuráveis pelo usuário.

## Melhorias e considerações

Ao construir aplicações reais, pense em:

- Validar e sanitizar prompts fornecidos por usuários.
- Conciliar custos (tokens e chamadas de API) com a necessidade de qualidade.
- Adicionar caching para respostas caras ou repetidas.
- Implementar filtragem e pós-processamento (por exemplo, remover ingredientes indesejados).

## Conclusão

Você implementou e executou um aplicativo simples de geração de texto. Explore variações de prompt, ajuste parâmetros (como `temperature`) e experimente formatos de saída (JSON, Markdown, etc.) para integrar ao seu app.

Siga para a Lição 7 para ver como aplicar esses conceitos em aplicativos de chat mais complexos: [07-building-chat-applications/README.md](../07-building-chat-applications/README.md?WT.mc_id=academic-105485-koreyst)
