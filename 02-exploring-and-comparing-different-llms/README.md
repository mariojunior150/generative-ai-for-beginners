# Explorando e comparando diferentes LLMs

[![Exploring and comparing different LLMs](./images/02-lesson-banner.png?WT.mc_id=academic-105485-koreyst)](https://youtu.be/KIRUeDKscfI?si=8BHX1zvwzQBn-PlK)

> _Clique na imagem acima para ver o vídeo desta lição_

Na lição anterior, vimos como a IA generativa está mudando o cenário tecnológico, como os Grandes Modelos de Linguagem (LLMs) funcionam e como um negócio — como nossa startup — pode aplicá-los aos seus casos de uso e crescer! Neste capítulo, vamos comparar e contrastar diferentes tipos de LLMs para entender seus prós e contras.

O próximo passo na jornada da nossa startup é explorar o cenário atual de LLMs e entender quais são adequados para o nosso caso de uso.

## Introdução

Nesta lição, abordaremos:

- Diferentes tipos de LLMs no cenário atual.
- Testar, iterar e comparar diferentes modelos para seu caso de uso no Azure.
- Como implantar um LLM.

## Objetivos de Aprendizagem

Após concluir esta lição, você será capaz de:

- Selecionar o modelo certo para seu caso de uso.
- Entender como testar, iterar e melhorar o desempenho do seu modelo.
- Saber como empresas implantam modelos.

## Entendendo diferentes tipos de LLMs

Os LLMs podem ter múltiplas categorizações com base em sua arquitetura, dados de treinamento e caso de uso. Entender essas diferenças ajudará nossa startup a selecionar o modelo certo para o cenário e a entender como testar, iterar e melhorar o desempenho.

Existem muitos tipos diferentes de modelos LLM; a escolha depende do que você pretende usar, seus dados, quanto você está disposto a pagar e mais.

Dependendo se você pretende usar os modelos para texto, áudio, vídeo, geração de imagem e assim por diante, pode optar por um tipo diferente de modelo.

- **Áudio e reconhecimento de fala**. Para essa finalidade, modelos do tipo Whisper são uma excelente escolha, pois são de propósito geral e voltados ao reconhecimento de fala. Eles são treinados em áudio diverso e podem realizar reconhecimento de fala multilíngue. Saiba mais sobre [modelos do tipo Whisper aqui](https://platform.openai.com/docs/models/whisper?WT.mc_id=academic-105485-koreyst).

- **Geração de imagens**. Para geração de imagens, DALL-E e Midjourney são duas escolhas muito conhecidas. O DALL-E é oferecido pelo Azure OpenAI. [Leia mais sobre DALL-E aqui](https://platform.openai.com/docs/models/dall-e?WT.mc_id=academic-105485-koreyst) e também no Capítulo 9 deste currículo.

- **Geração de texto**. A maioria dos modelos é treinada para geração de texto e você tem uma grande variedade de opções, do GPT-3.5 ao GPT-4. Eles apresentam custos diferentes, sendo o GPT-4 o mais caro. Vale a pena olhar o [playground do Azure OpenAI](https://oai.azure.com/portal/playground?WT.mc_id=academic-105485-koreyst) para avaliar quais modelos se encaixam melhor às suas necessidades em termos de capacidade e custo.

- **Multi-modalidade**. Se você deseja lidar com múltiplos tipos de dados na entrada e na saída, pode querer observar modelos como [gpt-4 turbo com visão ou gpt-4o](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#gpt-4-and-gpt-4-turbo-models?WT.mc_id=academic-105485-koreyst) — os lançamentos mais recentes de modelos OpenAI — que são capazes de combinar processamento de linguagem natural com compreensão visual, permitindo interações por interfaces multimodais.

Selecionar um modelo significa obter algumas capacidades básicas, o que pode não ser suficiente. Frequentemente, você tem dados específicos da empresa que precisa informar ao LLM de alguma forma. Existem algumas escolhas diferentes sobre como abordar isso, e veremos mais nas próximas seções.

### Foundation Models versus LLMs

O termo Foundation Model foi [cunhado por pesquisadores de Stanford](https://arxiv.org/abs/2108.07258?WT.mc_id=academic-105485-koreyst) e definido como um modelo de IA que segue alguns critérios, tais como:

- **São treinados usando aprendizado não supervisionado ou auto-supervisionado**, ou seja, são treinados em dados multimodais não rotulados e não exigem anotação humana ou rotulagem de dados para o processo de treinamento.
- **São modelos muito grandes**, baseados em redes neurais profundas treinadas em bilhões de parâmetros.
- **Normalmente são destinados a servir como uma ‘base’ para outros modelos**, ou seja, podem ser usados como ponto de partida para outros modelos construídos sobre eles, o que pode ser feito por meio de fine-tuning.

![Foundation Models versus LLMs](./images/FoundationModel.png?WT.mc_id=academic-105485-koreyst)

Fonte da imagem: [Essential Guide to Foundation Models and Large Language Models | by Babar M Bhatti | Medium](https://thebabar.medium.com/essential-guide-to-foundation-models-and-large-language-models-27dab58f7404)

Para esclarecer melhor essa distinção, vamos usar o ChatGPT como exemplo. Para construir a primeira versão do ChatGPT, um modelo chamado GPT-3.5 serviu como modelo base. Isso significa que a OpenAI usou alguns dados específicos de chat para criar uma versão ajustada do GPT-3.5 que foi especializada em desempenho em cenários conversacionais, como chatbots.

![Foundation Model](./images/Multimodal.png?WT.mc_id=academic-105485-koreyst)

Fonte da imagem: [2108.07258.pdf (arxiv.org)](https://arxiv.org/pdf/2108.07258.pdf?WT.mc_id=academic-105485-koreyst)

### Modelos open source versus proprietários

Outra forma de categorizar LLMs é se eles são open source ou proprietários.

Modelos open source são modelos disponibilizados ao público e podem ser usados por qualquer pessoa. Frequentemente são disponibilizados pela empresa que os criou ou pela comunidade de pesquisa. Esses modelos podem ser inspecionados, modificados e personalizados para vários casos de uso. No entanto, nem sempre são otimizados para uso em produção e podem não ser tão performáticos quanto modelos proprietários. Além disso, o financiamento para modelos open source pode ser limitado, e eles podem não ser mantidos a longo prazo ou atualizados com a pesquisa mais recente. Exemplos de modelos open source populares incluem [Alpaca](https://crfm.stanford.edu/2023/03/13/alpaca.html?WT.mc_id=academic-105485-koreyst), [Bloom](https://huggingface.co/bigscience/bloom) e [LLaMA](https://llama.meta.com).

Modelos proprietários são modelos que pertencem a uma empresa e não são disponibilizados ao público. Esses modelos geralmente são otimizados para uso em produção. No entanto, não podem ser inspecionados, modificados ou personalizados para diferentes casos de uso. Além disso, nem sempre estão disponíveis gratuitamente e podem exigir assinatura ou pagamento para uso. Também, os usuários não têm controle sobre os dados usados para treinar o modelo, o que significa que devem confiar no proprietário do modelo para garantir comprometimento com privacidade de dados e uso responsável de IA. Exemplos de modelos proprietários populares incluem [modelos OpenAI](https://platform.openai.com/docs/models/overview?WT.mc_id=academic-105485-koreyst), [Google Bard](https://sapling.ai/llm/bard?WT.mc_id=academic-105485-koreyst) e [Claude 2](https://www.anthropic.com/index/claude-2?WT.mc_id=academic-105485-koreyst).

### Embeddings versus geração de imagem versus geração de texto e código

Os LLMs também podem ser categorizados pelo tipo de saída que geram.

Embeddings são um conjunto de modelos que podem converter texto em uma forma numérica, chamada embedding, que é uma representação numérica do texto de entrada. Embeddings facilitam para as máquinas entenderem as relações entre palavras ou frases e podem ser usados como entradas por outros modelos, como modelos de classificação ou de agrupamento, que apresentam melhor desempenho em dados numéricos. Modelos de embeddings são frequentemente usados para transfer learning, onde um modelo é construído para uma tarefa substituta com abundância de dados e, em seguida, os pesos do modelo (embeddings) são reutilizados para outras tarefas downstream. Um exemplo dessa categoria é [embeddings OpenAI](https://platform.openai.com/docs/models/embeddings?WT.mc_id=academic-105485-koreyst).

![Embedding](./images/Embedding.png?WT.mc_id=academic-105485-koreyst)

Modelos de geração de imagens são modelos que geram imagens. Esses modelos são frequentemente usados para edição de imagens, síntese de imagens e tradução de imagens. Modelos de geração de imagem são frequentemente treinados em grandes conjuntos de dados de imagens, como [LAION-5B](https://laion.ai/blog/laion-5b/?WT.mc_id=academic-105485-koreyst), e podem ser usados para gerar novas imagens ou editar imagens existentes com técnicas de inpainting, super-resolução e colorização. Exemplos incluem [DALL-E-3](https://openai.com/dall-e-3?WT.mc_id=academic-105485-koreyst) e [modelos Stable Diffusion](https://github.com/Stability-AI/StableDiffusion?WT.mc_id=academic-105485-koreyst).

![Image generation](./images/Image.png?WT.mc_id=academic-105485-koreyst)

Modelos de geração de texto e código são modelos que geram texto ou código. Esses modelos são frequentemente usados para sumarização de texto, tradução e perguntas e respostas. Modelos de geração de texto são frequentemente treinados em grandes conjuntos de dados de texto, como [BookCorpus](https://www.cv-foundation.org/openaccess/content_iccv_2015/html/Zhu_Aligning_Books_and_ICCV_2015_paper.html?WT.mc_id=academic-105485-koreyst), e podem ser usados para gerar novo texto ou responder perguntas. Modelos de geração de código, como [CodeParrot](https://huggingface.co/codeparrot?WT.mc_id=academic-105485-koreyst), são frequentemente treinados em grandes conjuntos de dados de código, como GitHub, e podem ser usados para gerar código novo ou corrigir bugs em código existente.

![Text and code generation](./images/Text.png?WT.mc_id=academic-105485-koreyst)

### Encoder-Decoder versus Decoder-only

Para falar sobre os diferentes tipos de arquiteturas de LLMs, vamos usar uma analogia.

Imagine que seu gerente lhe deu a tarefa de escrever um quiz para os alunos. Você tem dois colegas; um cuida da criação do conteúdo e o outro cuida da revisão.

O criador de conteúdo é como um modelo apenas Decoder: ele pode olhar para o tema e ver o que você já escreveu e então escrever um curso com base nisso. Eles são muito bons em escrever conteúdo envolvente e informativo, mas não são muito bons em entender o tema e os objetivos de aprendizagem. Alguns exemplos de modelos Decoder são os modelos da família GPT, como o GPT-3.

O revisor é como um modelo apenas Encoder: ele olha o curso escrito e as respostas, percebe a relação entre eles e entende o contexto, mas não é bom em gerar conteúdo. Um exemplo de modelo apenas Encoder seria o BERT.

Imagine que também podemos ter alguém que possa criar e revisar o quiz; esse é um modelo Encoder-Decoder. Alguns exemplos seriam BART e T5.

### Serviço versus Modelo

Agora, vamos falar sobre a diferença entre serviço e modelo. Um serviço é um produto oferecido por um provedor de nuvem e costuma ser uma combinação de modelos, dados e outros componentes. Um modelo é o componente central de um serviço e costuma ser um modelo base, como um LLM.

Os serviços são frequentemente otimizados para uso em produção e costumam ser mais fáceis de usar do que modelos, por meio de uma interface gráfica. No entanto, serviços nem sempre estão disponíveis gratuitamente e podem exigir assinatura ou pagamento para uso, em troca de aproveitar o equipamento e os recursos do proprietário do serviço, otimizar despesas e escalar facilmente. Um exemplo de serviço é o [Azure OpenAI Service](https://learn.microsoft.com/azure/ai-services/openai/overview?WT.mc_id=academic-105485-koreyst), que oferece um plano de tarifa pay-as-you-go, o que significa que os usuários são cobrados proporcionalmente ao quanto usam o serviço. Além disso, o Azure OpenAI Service oferece segurança em nível empresarial e um framework de IA responsável por cima das capacidades dos modelos.

Modelos são apenas a rede neural, com os parâmetros, pesos e outros. Permitir que empresas executem localmente exigiria comprar equipamento, construir uma estrutura para escalar e adquirir uma licença ou usar um modelo open source. Um modelo como LLaMA está disponível para uso, exigindo capacidade computacional para executar o modelo.

## Como testar e iterar com diferentes modelos para entender o desempenho no Azure

Uma vez que nossa equipe explorou o cenário atual de LLMs e identificou alguns bons candidatos para seus cenários, o próximo passo é testá-los em seus dados e em sua carga de trabalho. Esse é um processo iterativo, feito por experimentos e medições.
A maioria dos modelos mencionados nos parágrafos anteriores (modelos OpenAI, modelos open source como Llama2 e transformers do Hugging Face) estão disponíveis no [Catálogo de Modelos](https://learn.microsoft.com/azure/ai-studio/how-to/model-catalog-overview?WT.mc_id=academic-105485-koreyst) no [Azure AI Studio](https://ai.azure.com/?WT.mc_id=academic-105485-koreyst).

[Azure AI Studio](https://learn.microsoft.com/azure/ai-studio/what-is-ai-studio?WT.mc_id=academic-105485-koreyst) é uma plataforma em nuvem projetada para desenvolvedores construírem aplicações de IA generativa e gerenciarem todo o ciclo de vida de desenvolvimento - da experimentação à avaliação - combinando todos os serviços Azure AI em um único hub com uma interface gráfica prática. O Catálogo de Modelos no Azure AI Studio permite ao usuário:

- Encontrar o Foundation Model de interesse no catálogo - seja proprietário ou open source - filtrando por tarefa, licença ou nome. Para melhorar a capacidade de busca, os modelos são organizados em coleções, como a coleção Azure OpenAI, a coleção Hugging Face e outras.

![Model catalog](./images/AzureAIStudioModelCatalog.png?WT.mc_id=academic-105485-koreyst)

- Revisar a ficha do modelo, incluindo uma descrição detalhada do uso pretendido e dos dados de treinamento, exemplos de código e resultados de avaliação na biblioteca de avaliações internas.

![Model card](./images/ModelCard.png?WT.mc_id=academic-105485-koreyst)

- Comparar benchmarks entre modelos e conjuntos de dados disponíveis na indústria para avaliar qual atende ao cenário de negócio, por meio do painel [Model Benchmarks](https://learn.microsoft.com/azure/ai-studio/how-to/model-benchmarks?WT.mc_id=academic-105485-koreyst).

![Model benchmarks](./images/ModelBenchmarks.png?WT.mc_id=academic-105485-koreyst)

- Ajustar o modelo com dados de treinamento personalizados para melhorar o desempenho do modelo em uma carga de trabalho específica, aproveitando as capacidades de experimentação e rastreamento do Azure AI Studio.

![Model fine-tuning](./images/FineTuning.png?WT.mc_id=academic-105485-koreyst)

- Implantar o modelo pré-treinado original ou a versão ajustada em uma inferência em tempo real remota - compute gerenciado - ou endpoint de API serverless - [pay-as-you-go](https://learn.microsoft.com/azure/ai-studio/how-to/model-catalog-overview#model-deployment-managed-compute-and-serverless-api-pay-as-you-go?WT.mc_id=academic-105485-koreyst) - para permitir que aplicações o consumam.

![Model deployment](./images/ModelDeploy.png?WT.mc_id=academic-105485-koreyst)

> [!NOTE]
> Nem todos os modelos no catálogo estão atualmente disponíveis para fine-tuning e/ou implantação pay-as-you-go. Verifique a ficha do modelo para detalhes sobre as capacidades e limitações do modelo.

## Melhorando os resultados de LLMs

Exploramos com nossa equipe de startup diferentes tipos de LLMs e uma plataforma em nuvem (Azure Machine Learning) que nos permite comparar diferentes modelos, avaliá-los com dados de teste, melhorar o desempenho e implantá-los em endpoints de inferência.

Mas quando eles devem considerar ajustar um modelo em vez de usar um pré-treinado? Existem outras abordagens para melhorar o desempenho do modelo em cargas de trabalho específicas?

Existem várias abordagens que uma empresa pode usar para obter os resultados desejados de um LLM. Você pode selecionar diferentes tipos de modelos com diferentes graus de treinamento ao implantar um LLM em produção, com diferentes níveis de complexidade, custo e qualidade. Aqui estão algumas abordagens diferentes:

- **Engenharia de prompt com contexto**. A ideia é fornecer contexto suficiente ao prompt para garantir respostas que você precise.

- **Retrieval Augmented Generation, RAG**. Seus dados podem existir em um banco de dados ou endpoint web, por exemplo, e para garantir que esses dados, ou um subconjunto deles, sejam incluídos no momento do prompt, você pode buscar os dados relevantes e incluí-los no prompt do usuário.

- **Modelo fine-tuned**. Aqui, você treina o modelo adicionalmente com seus próprios dados, o que faz com que o modelo seja mais preciso e responsivo às suas necessidades, mas pode ser caro.

![LLMs deployment](./images/Deploy.png?WT.mc_id=academic-105485-koreyst)

Fonte da imagem: [Four Ways that Enterprises Deploy LLMs | Fiddler AI Blog](https://www.fiddler.ai/blog/four-ways-that-enterprises-deploy-llms?WT.mc_id=academic-105485-koreyst)

### Engenharia de prompt com contexto

LLMs pré-treinados funcionam muito bem em tarefas generalizadas de linguagem natural, mesmo sendo chamados com um prompt curto, como uma frase para completar ou uma pergunta — o chamado aprendizado “zero-shot”.

No entanto, quanto mais o usuário puder enquadrar sua consulta com um pedido detalhado e exemplos — o Contexto — mais precisa e próxima das expectativas do usuário a resposta será. Nesse caso, falamos em aprendizado “one-shot” se o prompt inclui apenas um exemplo e “few-shot learning” se inclui vários exemplos.
A engenharia de prompt com contexto é a abordagem mais econômica para começar.

### Retrieval Augmented Generation (RAG)

LLMs têm a limitação de que podem usar apenas os dados que foram usados durante seu treinamento para gerar uma resposta. Isso significa que eles não sabem nada sobre fatos que aconteceram após seu processo de treinamento e não conseguem acessar informações não públicas (como dados da empresa).

Isso pode ser superado por meio de RAG, uma técnica que aumenta o prompt com dados externos na forma de trechos de documentos, considerando os limites de tamanho do prompt. Isso é suportado por ferramentas de banco de dados vetorial (como [Azure Vector Search](https://learn.microsoft.com/azure/search/vector-search-overview?WT.mc_id=academic-105485-koreyst)) que recuperam trechos úteis de várias fontes de dados predefinidas e os adicionam ao contexto do prompt.

Essa técnica é muito útil quando uma empresa não tem dados suficientes, tempo suficiente ou recursos para ajustar um LLM, mas ainda deseja melhorar o desempenho em uma carga de trabalho específica e reduzir riscos de fabricação de fatos, ou seja, mistificação da realidade ou conteúdo prejudicial.

### Modelo fine-tuned

Fine-tuning é um processo que aproveita transfer learning para “adaptar” o modelo a uma tarefa downstream ou resolver um problema específico. Diferentemente do few-shot learning e do RAG, ele resulta em um novo modelo sendo gerado, com pesos e vieses atualizados. Requer um conjunto de exemplos de treinamento consistindo em uma única entrada (o prompt) e sua saída associada (a conclusão).

Essa seria a abordagem preferida se:

- **Usar modelos fine-tuned**. Uma empresa gostaria de usar modelos menos capazes, porém ajustados (como modelos de embeddings), em vez de modelos de alto desempenho, resultando em uma solução mais econômica e rápida.

- **Considerar latência**. A latência é importante para um caso de uso específico, então não é possível usar prompts muito longos ou o número de exemplos que o modelo precisa aprender não cabe no limite de tamanho do prompt.

- **Manter-se atualizado**. Uma empresa possui muitos dados de alta qualidade e rótulos de verdade básica (ground truth) e os recursos necessários para manter esses dados atualizados ao longo do tempo.

### Modelo treinado

Treinar um LLM do zero é, sem dúvida, a abordagem mais difícil e complexa de adotar, exigindo enormes quantidades de dados, recursos qualificados e poder computacional adequado. Essa opção deve ser considerada apenas em um cenário onde uma empresa tem um caso de uso altamente específico e uma grande quantidade de dados centrados no domínio.

## Verificação de conhecimento

Qual poderia ser uma boa abordagem para melhorar os resultados de conclusão de um LLM?

1. Engenharia de prompt com contexto
1. RAG
1. Modelo fine-tuned

R: 3, se você tiver tempo, recursos e dados de alta qualidade, o fine-tuning é a melhor opção para se manter atualizado. No entanto, se você estiver procurando melhorar as coisas e estiver sem tempo, vale a pena considerar o RAG primeiro.

## 🚀 Desafio

Leia mais sobre como você pode [usar RAG](https://learn.microsoft.com/azure/search/retrieval-augmented-generation-overview?WT.mc_id=academic-105485-koreyst) para o seu negócio.

## Excelente trabalho, continue aprendendo

Após concluir esta lição, confira nossa [coleção de aprendizado de IA generativa](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) para continuar aprimorando seu conhecimento em IA generativa!

Vá para a Lição 3, onde veremos como [construir com IA generativa de forma responsável](../03-using-generative-ai-responsibly/README.md?WT.mc_id=academic-105485-koreyst)!
