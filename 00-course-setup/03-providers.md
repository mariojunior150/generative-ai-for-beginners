# Escolhendo e Configurando um Provedor de LLM 🔑

As atividades **podem** também ser configuradas para funcionar com um ou mais deployments de Large Language Model (LLM) por meio de um provedor de serviço compatível como OpenAI, Azure ou Hugging Face. Esses provedores oferecem um _endpoint hospedado_ (API) ao qual podemos acessar programaticamente com as credenciais corretas (chave de API ou token). Neste curso, discutimos estes provedores:

 - [OpenAI](https://platform.openai.com/docs/models?WT.mc_id=academic-105485-koreyst) com modelos diversos, incluindo a série principal GPT.
 - [Azure OpenAI](https://learn.microsoft.com/azure/ai-services/openai/?WT.mc_id=academic-105485-koreyst) para modelos OpenAI com foco em prontidão empresarial.
 - [Hugging Face](https://huggingface.co/docs/hub/index?WT.mc_id=academic-105485-koreyst) para modelos open-source e servidores de inferência.

**Você precisará usar suas próprias contas para esses exercícios**. As atividades são opcionais, então você pode configurar um, todos ou nenhum dos provedores com base nos seus interesses. Aqui vai uma orientação para o cadastro:

| Cadastro | Custo | Chave de API | Playground | Comentários |
|:---|:---|:---|:---|:---|
| [OpenAI](https://platform.openai.com/signup?WT.mc_id=academic-105485-koreyst)| [Pricing](https://openai.com/pricing#language-models?WT.mc_id=academic-105485-koreyst)| [Project-based](https://platform.openai.com/api-keys?WT.mc_id=academic-105485-koreyst) | [No-Code, Web](https://platform.openai.com/playground?WT.mc_id=academic-105485-koreyst) | Vários modelos disponíveis |
| [Azure](https://aka.ms/azure/free?WT.mc_id=academic-105485-koreyst)| [Pricing](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/?WT.mc_id=academic-105485-koreyst)| [SDK Quickstart](https://learn.microsoft.com/azure/ai-services/openai/quickstart?WT.mc_id=academic-105485-koreyst)| [Studio Quickstart](https://learn.microsoft.com/azure/ai-services/openai/quickstart?WT.mc_id=academic-105485-koreyst) |  [É necessário solicitar acesso antecipadamente](https://learn.microsoft.com/azure/ai-services/openai/?WT.mc_id=academic-105485-koreyst)|
| [Hugging Face](https://huggingface.co/join?WT.mc_id=academic-105485-koreyst) | [Pricing](https://huggingface.co/pricing) | [Access Tokens](https://huggingface.co/docs/hub/security-tokens?WT.mc_id=academic-105485-koreyst) | [Hugging Chat](https://huggingface.co/chat/?WT.mc_id=academic-105485-koreyst)| [Hugging Chat tem modelos limitados](https://huggingface.co/chat/models?WT.mc_id=academic-105485-koreyst) |
| | | | | |

Siga as instruções abaixo para _configurar_ este repositório para uso com diferentes provedores. Atividades que exigem um provedor específico terão uma destas tags no nome do arquivo:

- `aoai` - requer endpoint e chave Azure OpenAI
- `oai` - requer endpoint e chave OpenAI
- `hf` - requer token Hugging Face

Você pode configurar um, nenhum ou todos os provedores. As atividades relacionadas simplesmente apresentarão erro se as credenciais estiverem ausentes.

## Criar arquivo `.env`

Assumimos que você já leu as orientações acima, se cadastrou no provedor relevante e obteve as credenciais de autenticação necessárias (API_KEY ou token). No caso do Azure OpenAI, assumimos também que você tem um deployment válido de um serviço Azure OpenAI (endpoint) com pelo menos um modelo GPT implantado para chat completion.

O próximo passo é configurar suas **variáveis de ambiente locais** da seguinte forma:

1. Procure na pasta raiz um arquivo `.env.copy` que deve conter algo como isto:

   ```bash
   # OpenAI Provider
   OPENAI_API_KEY='<add your OpenAI API key here>'

   ## Azure OpenAI
   AZURE_OPENAI_API_VERSION='2024-02-01' # Default is set!
   AZURE_OPENAI_API_KEY='<add your AOAI key here>'
   AZURE_OPENAI_ENDPOINT='<add your AOIA service endpoint here>'
   AZURE_OPENAI_DEPLOYMENT='<add your chat completion model name here>' 
   AZURE_OPENAI_EMBEDDINGS_DEPLOYMENT='<add your embeddings model name here>'

   ## Hugging Face
   HUGGING_FACE_API_KEY='<add your HuggingFace API or token here>'
   ```

2. Copie esse arquivo para `.env` usando o comando abaixo. Este arquivo está no `.gitignore`, mantendo os segredos seguros.

   ```bash
   cp .env.copy .env
   ```

3. Preencha os valores (substitua os placeholders à direita de `=`) conforme descrito na próxima seção.

4. (Opcional) Se você usar GitHub Codespaces, tem a opção de salvar variáveis de ambiente como _Codespaces secrets_ associadas a este repositório. Nesse caso, não será necessário configurar um arquivo `.env` local. **No entanto, observe que essa opção funciona apenas se você usar GitHub Codespaces.** Você ainda precisará configurar o arquivo `.env` se usar Docker Desktop.

## Preencher o arquivo `.env`

Vamos conferir rapidamente os nomes das variáveis para entender o que representam:

| Variável  | Descrição  |
| :--- | :--- |
| HUGGING_FACE_API_KEY | Este é o token de acesso de usuário que você configura no seu perfil |
| OPENAI_API_KEY | Esta é a chave de autorização para usar o serviço nos endpoints OpenAI não-Azure |
| AZURE_OPENAI_API_KEY | Esta é a chave de autorização para usar o serviço Azure OpenAI |
| AZURE_OPENAI_ENDPOINT | Este é o endpoint implantado para um recurso Azure OpenAI |
| AZURE_OPENAI_DEPLOYMENT | Este é o deployment do modelo de _geração de texto_ |
| AZURE_OPENAI_EMBEDDINGS_DEPLOYMENT | Este é o deployment do modelo de _embeddings de texto_ |
| | |

Observação: As duas últimas variáveis do Azure OpenAI refletem um modelo padrão para chat completion (geração de texto) e busca vetorial (embeddings), respectivamente. As instruções para configurá-las serão definidas nas atividades relevantes.

## Configurar Azure: Pelo Portal

Os valores de endpoint e chave do Azure OpenAI serão encontrados no [Azure Portal](https://portal.azure.com?WT.mc_id=academic-105485-koreyst), então vamos começar por lá.

1. Acesse o [Azure Portal](https://portal.azure.com?WT.mc_id=academic-105485-koreyst)
1. Clique em **Keys and Endpoint** na barra lateral (menu à esquerda).
1. Clique em **Show Keys** - você verá o seguinte: KEY 1, KEY 2 e Endpoint.
1. Use o valor de KEY 1 para AZURE_OPENAI_API_KEY
1. Use o valor de Endpoint para AZURE_OPENAI_ENDPOINT

Em seguida, precisamos dos endpoints para os modelos específicos que implantamos.

1. Clique em **Model deployments** na barra lateral (menu à esquerda) do recurso Azure OpenAI.
1. Na página de destino, clique em **Manage Deployments**

Isso levará você ao site Azure OpenAI Studio, onde encontraremos os outros valores conforme descrito abaixo.

## Configurar Azure: Pelo Studio

1. Navegue até o [Azure OpenAI Studio](https://oai.azure.com?WT.mc_id=academic-105485-koreyst) **a partir do seu recurso**, conforme descrito acima.
1. Clique na aba **Deployments** (barra lateral à esquerda) para ver os modelos atualmente implantados.
1. Se o modelo desejado não estiver implantado, use **Create new deployment** para implantá-lo.
1. Você precisará de um modelo de _text-generation_ - recomendamos: **gpt-35-turbo**
1. Você precisará de um modelo de _text-embedding_ - recomendamos **text-embedding-ada-002**

Agora atualize as variáveis de ambiente para refletir o nome do _Deployment_ usado. Isso normalmente será igual ao nome do modelo, a menos que você o tenha alterado explicitamente. Por exemplo, você pode ter:

```bash
AZURE_OPENAI_DEPLOYMENT='gpt-35-turbo'
AZURE_OPENAI_EMBEDDINGS_DEPLOYMENT='text-embedding-ada-002'
```

**Não se esqueça de salvar o arquivo .env quando terminar**. Agora você pode sair do arquivo e retornar às instruções para executar o notebook.

## Configurar OpenAI: Pelo Perfil

Sua chave de API OpenAI pode ser encontrada na sua [conta OpenAI](https://platform.openai.com/api-keys?WT.mc_id=academic-105485-koreyst). Se você não tiver uma, pode se inscrever para obter uma conta e criar uma chave de API. Assim que tiver a chave, use-a para preencher a variável `OPENAI_API_KEY` no arquivo `.env`.

## Configurar Hugging Face: Pelo Perfil

Seu token Hugging Face pode ser encontrado no seu perfil em [Access Tokens](https://huggingface.co/settings/tokens?WT.mc_id=academic-105485-koreyst). Não publique nem compartilhe isso publicamente. Em vez disso, crie um token novo para uso neste projeto e copie-o para o arquivo `.env` na variável `HUGGING_FACE_API_KEY`. _Observação:_ isso tecnicamente não é uma chave de API, mas é usado para autenticação, então mantemos essa convenção de nomenclatura por consistência.
