# Fundamentos de Engenharia de Prompt

[![Prompt Engineering Fundamentals](./images/04-lesson-banner.png?WT.mc_id=academic-105485-koreyst)](https://youtu.be/GElCu2kUlRs?si=qrXsBvXnCW12epb8)

## Introdução
Este módulo aborda conceitos e técnicas essenciais para criar prompts eficazes em modelos de IA generativa. A forma como você escreve seu prompt para um LLM também importa. Um prompt cuidadosamente elaborado pode alcançar melhor qualidade de resposta. Mas o que exatamente significam termos como _prompt_ e _engenharia de prompt_? E como posso melhorar o _input_ do prompt que envio ao LLM? Essas são as perguntas que tentaremos responder neste capítulo e no próximo.

_IA generativa_ é capaz de criar novo conteúdo (por exemplo, texto, imagens, áudio, código etc.) em resposta a solicitações de usuários. Ela consegue isso usando _Grandes Modelos de Linguagem_ como a série GPT da OpenAI (“Generative Pre-trained Transformer”) treinados para usar linguagem natural e código.

Os usuários agora podem interagir com esses modelos usando paradigmas familiares como chat, sem precisar de qualquer expertise técnica ou treinamento. Os modelos são _baseados em prompt_ — os usuários enviam um input de texto (prompt) e recebem de volta a resposta da IA (completion). Eles podem então “conversar com a IA” de forma iterativa, em conversas de múltiplas etapas, refinando seu prompt até que a resposta corresponda às expectativas.

“Prompts” agora se tornam a principal _interface de programação_ para aplicativos de IA generativa, dizendo aos modelos o que fazer e influenciando a qualidade das respostas retornadas. “Engenharia de Prompt” é um campo de estudo em rápido crescimento que se concentra no _design e otimização_ de prompts para entregar respostas consistentes e de qualidade em escala.

## Objetivos de Aprendizagem

Nesta lição, aprendemos o que é Engenharia de Prompt, por que ela importa e como podemos criar prompts mais eficazes para um determinado modelo e objetivo de aplicação. Vamos entender conceitos centrais e boas práticas de engenharia de prompt — e conhecer um ambiente interativo de Jupyter Notebooks “sandbox” onde podemos ver esses conceitos aplicados em exemplos reais.

Ao final desta lição, seremos capazes de:

1. Explicar o que é engenharia de prompt e por que ela importa.
2. Descrever os componentes de um prompt e como eles são usados.
3. Aprender boas práticas e técnicas para engenharia de prompt.
4. Aplicar técnicas aprendidas em exemplos reais, usando um endpoint OpenAI.

## Termos-Chave

Engenharia de Prompt: A prática de projetar e refinar inputs para orientar modelos de IA a produzir saídas desejadas.
Tokenização: O processo de converter texto em unidades menores, chamadas tokens, que um modelo pode entender e processar.
LLMs Ajustados por Instrução: Grandes Modelos de Linguagem (LLMs) que foram fine-tuned com instruções específicas para melhorar a precisão e relevância das respostas.

## Sandbox de Aprendizado

A engenharia de prompt é atualmente mais arte do que ciência. A melhor forma de melhorar nossa intuição para ela é _praticar mais_ e adotar uma abordagem de tentativa e erro que combine expertise no domínio da aplicação com técnicas recomendadas e otimizações específicas de modelo.

O Jupyter Notebook que acompanha esta lição fornece um ambiente _sandbox_ onde você pode experimentar o que aprende — enquanto avança ou como parte do desafio de código no final. Para executar os exercícios, você precisará de:

1. **Uma chave de API Azure OpenAI** — o endpoint do serviço para um LLM implantado.
2. **Um runtime Python** — no qual o Notebook pode ser executado.
3. **Variáveis de ambiente locais** — _complete os passos de [SETUP](./../00-course-setup/02-setup-local.md?WT.mc_id=academic-105485-koreyst) agora para ficar pronto_.

O notebook vem com exercícios _starter_ — mas você é incentivado a adicionar suas próprias seções de _Markdown_ (descrição) e _Code_ (requisições de prompt) para experimentar mais exemplos ou ideias — e construir sua intuição para design de prompt.

## Guia Ilustrado

Quer ver o panorama do que esta lição cobre antes de se aprofundar? Confira este guia ilustrado, que mostra os principais tópicos abordados e as conclusões-chave para você refletir em cada um deles. O roteiro da lição leva você desde o entendimento dos conceitos e desafios centrais até como abordá-los com técnicas e boas práticas de engenharia de prompt relevantes. Note que a seção “Técnicas Avançadas” neste guia se refere a conteúdo coberto no _próximo_ capítulo deste currículo.

![Illustrated Guide to Prompt Engineering](./images/04-prompt-engineering-sketchnote.png?WT.mc_id=academic-105485-koreyst)

## Nossa Startup

Agora, vamos falar sobre como _este tópico_ se relaciona com a missão da nossa startup de [trazer inovação em IA para a educação](https://educationblog.microsoft.com/2023/06/collaborating-to-bring-ai-innovation-to-education?WT.mc_id=academic-105485-koreyst). Queremos construir aplicativos com IA para _aprendizado personalizado_ — então vamos pensar em como diferentes usuários do nosso aplicativo podem “desenhar” prompts:

- **Administradores** podem pedir à IA para _analisar dados curriculares e identificar lacunas na cobertura_. A IA pode resumir resultados ou visualizá-los com código.
- **Educadores** podem pedir à IA para _gerar um plano de aula para um público e tópico-alvo_. A IA pode construir o plano personalizado em um formato especificado.
- **Estudantes** podem pedir à IA para _tutorar em uma matéria difícil_. A IA pode agora orientar os alunos com lições, dicas e exemplos adaptados ao nível deles.

Isso é apenas a ponta do iceberg. Confira [Prompts For Education](https://github.com/microsoft/prompts-for-edu/tree/main?WT.mc_id=academic-105485-koreyst) — uma biblioteca open source de prompts curada por especialistas em educação — para ter uma visão mais ampla das possibilidades! _Experimente executar alguns desses prompts no sandbox ou usar o OpenAI Playground para ver o que acontece!_

<!--
LESSON TEMPLATE:
This unit should cover core concept #1.
Reinforce the concept with examples and references.

CONCEPT #1:
Prompt Engineering.
Define it and explain why it is needed.
-->

## O que é Engenharia de Prompt?

Começamos esta lição definindo **Engenharia de Prompt** como o processo de _desenhar e otimizar_ inputs de texto (prompts) para entregar respostas consistentes e de qualidade (completions) para um determinado objetivo de aplicação e modelo. Podemos pensar nisso como um processo em duas etapas:

- _desenhar_ o prompt inicial para um dado modelo e objetivo
- _refinar_ o prompt iterativamente para melhorar a qualidade da resposta

Este é necessariamente um processo de tentativa e erro que exige intuição do usuário e esforço para obter resultados ótimos. Então por que isso é importante? Para responder a essa pergunta, primeiro precisamos entender três conceitos:

- _Tokenização_ = como o modelo “vê” o prompt
- _LLMs base_ = como o modelo de fundação “processa” um prompt
- _LLMs ajustados por instrução_ = como o modelo agora pode ver “tarefas”

### Tokenização

Um LLM vê prompts como uma _sequência de tokens_ em que diferentes modelos (ou versões de um modelo) podem tokenizar o mesmo prompt de formas diferentes. Como os LLMs são treinados com tokens (e não com texto bruto), a forma como os prompts são tokenizados tem impacto direto na qualidade da resposta gerada.

Para ter intuição de como a tokenização funciona, experimente ferramentas como o [OpenAI Tokenizer](https://platform.openai.com/tokenizer?WT.mc_id=academic-105485-koreyst) mostrado abaixo. Copie seu prompt e veja como ele é convertido em tokens, prestando atenção em como os espaços e a pontuação são tratados. Note que este exemplo mostra um LLM mais antigo (GPT-3) — então tentar isto com um modelo mais novo pode produzir um resultado diferente.

![Tokenization](./images/04-tokenizer-example.png?WT.mc_id=academic-105485-koreyst)

### Conceito: Modelos de Fundação

Uma vez que um prompt é tokenizado, a função principal do [“LLM Base”](https://blog.gopenai.com/an-introduction-to-base-and-instruction-tuned-large-language-models-8de102c785a6?WT.mc_id=academic-105485-koreyst) (ou modelo de fundação) é prever o token seguinte nessa sequência. Como os LLMs são treinados em grandes conjuntos de dados textuais, eles têm um bom senso das relações estatísticas entre tokens e podem fazer essa previsão com certa confiança. Note que eles não entendem o _significado_ das palavras no prompt ou no token; eles apenas enxergam um padrão que podem “completar” com a próxima previsão. Eles podem continuar prevendo a sequência até serem interrompidos por intervenção do usuário ou alguma condição pré-estabelecida.

Quer ver como a conclusão baseada em prompt funciona? Insira o prompt acima no Azure OpenAI Studio [_Chat Playground_](https://oai.azure.com/playground?WT.mc_id=academic-105485-koreyst) com as configurações padrão. O sistema está configurado para tratar prompts como solicitações de informação — assim você deve ver uma completion que satisfaça esse contexto.

Mas e se o usuário quiser ver algo específico que atenda a algum critério ou objetivo de tarefa? É aí que os LLMs _ajustados por instrução_ entram em cena.

![Base LLM Chat Completion](./images/04-playground-chat-base.png?WT.mc_id=academic-105485-koreyst)

### Conceito: LLMs Ajustados por Instrução

Um [LLM Ajustado por Instrução](https://blog.gopenai.com/an-introduction-to-base-and-instruction-tuned-large-language-models-8de102c785a6?WT.mc_id=academic-105485-koreyst) parte do modelo de fundação e faz fine-tuning com exemplos ou pares de input/output (por exemplo, “mensagens” de múltiplas etapas) que podem conter instruções claras — e a resposta da IA tenta seguir essa instrução.

Isso usa técnicas como Reinforcement Learning with Human Feedback (RLHF) que podem treinar o modelo a _seguir instruções_ e _aprender com feedback_ para que produza respostas mais adequadas a aplicações práticas e mais relevantes aos objetivos do usuário.

Vamos testar — reconsidere o prompt acima, mas agora mude a _mensagem do sistema_ para fornecer a seguinte instrução como contexto:

> _Resuma o conteúdo fornecido para um aluno da segunda série. Mantenha o resultado em um parágrafo com 3 a 5 tópicos._

Veja como o resultado agora é sintonizado para refletir o objetivo e o formato desejados? Um educador pode usar essa resposta diretamente em seus slides para essa aula.

![Instruction Tuned LLM Chat Completion](./images/04-playground-chat-instructions.png?WT.mc_id=academic-105485-koreyst)

## Por que precisamos de Engenharia de Prompt?

Agora que sabemos como os prompts são processados pelos LLMs, vamos falar sobre _por que_ precisamos de engenharia de prompt. A resposta está no fato de que os LLMs atuais apresentam uma série de desafios que tornam mais difícil alcançar _completions confiáveis e consistentes_ sem empregar esforço na construção e otimização do prompt. Por exemplo:

1. **As respostas do modelo são estocásticas.** O _mesmo prompt_ provavelmente produzirá respostas diferentes em diferentes modelos ou versões de modelo. E pode até produzir resultados diferentes com o _mesmo modelo_ em momentos distintos. _Técnicas de engenharia de prompt podem nos ajudar a minimizar essas variações fornecendo guardrails melhores_.

1. **Modelos podem fabricar respostas.** Modelos são pré-treinados com conjuntos de dados _grandes, mas finitos_, o que significa que eles não conhecem conceitos fora desse escopo de treinamento. Como resultado, podem produzir completions imprecisas, imaginárias ou diretamente contraditórias a fatos conhecidos. _Técnicas de engenharia de prompt ajudam usuários a identificar e mitigar essas fabricações, por exemplo, pedindo à IA citações ou raciocínio_.

1. **As capacidades dos modelos variam.** Modelos ou gerações mais novas terão capacidades mais ricas, mas também trazem peculiaridades e tradeoffs únicos em custo e complexidade. _A engenharia de prompt pode nos ajudar a desenvolver melhores práticas e fluxos de trabalho que abstraem diferenças e se adaptam a requisitos específicos de cada modelo de forma escalável e fluida_.

Vamos ver isso em ação no Playground OpenAI ou Azure OpenAI:

- Use o mesmo prompt com diferentes implantações de LLM (por exemplo, OpenAI, Azure OpenAI, Hugging Face) — você notou variações?
- Use o mesmo prompt repetidamente com a _mesma_ implantação de LLM (por exemplo, playground Azure OpenAI) — como essas variações diferiram?

### Exemplo de Fabricações

Neste curso, usamos o termo **“fabricação”** para referir o fenômeno em que os LLMs às vezes geram informações factualmente incorretas devido a limitações no treinamento ou outras restrições. Você talvez também tenha ouvido isso referido como _“alucinações”_ em artigos populares ou trabalhos de pesquisa. No entanto, recomendamos fortemente usar _“fabricação”_ como termo para não antropomorfizar o comportamento ao atribuir uma característica parecida com a humana a um resultado gerado por máquina. Isso também reforça as [diretrizes de IA responsável](https://www.microsoft.com/ai/responsible-ai?WT.mc_id=academic-105485-koreyst) do ponto de vista terminológico, removendo termos que também podem ser considerados ofensivos ou não inclusivos em alguns contextos.

Quer ter uma ideia de como as fabricações funcionam? Pense em um prompt que instrui a IA a gerar conteúdo sobre um tópico inexistente (para garantir que não esteja no conjunto de treinamento). Por exemplo — tentei este prompt:

> **Prompt:** gere um plano de aula sobre a Guerra Marciana de 2076.

Uma busca na web mostrou que havia relatos fictícios (por exemplo, séries de TV ou livros) sobre guerras marcianas — mas nenhum em 2076. O senso comum também nos diz que 2076 está _no futuro_ e, portanto, não pode ser associado a um evento real.

Então o que acontece quando executamos esse prompt com diferentes provedores de LLM?

> **Resposta 1**: OpenAI Playground (GPT-35)

![Response 1](./images/04-fabrication-oai.png?WT.mc_id=academic-105485-koreyst)

> **Resposta 2**: Azure OpenAI Playground (GPT-35)

![Response 2](./images/04-fabrication-aoai.png?WT.mc_id=academic-105485-koreyst)

> **Resposta 3**: : Hugging Face Chat Playground (LLama-2)

![Response 3](./images/04-fabrication-huggingchat.png?WT.mc_id=academic-105485-koreyst)

Como esperado, cada modelo (ou versão de modelo) produz respostas ligeiramente diferentes graças ao comportamento estocástico e às variações de capacidade do modelo. Por exemplo, um modelo direcionou a resposta para um público da 8ª série, enquanto o outro assumiu um estudante de ensino médio. Mas os três modelos geraram respostas que poderiam convencer um usuário desinformado de que o evento era real.

Técnicas de engenharia de prompt como _metaprompting_ e _configuração de temperature_ podem reduzir fabricações do modelo até certo ponto. Novas _arquiteturas_ de engenharia de prompt também incorporam ferramentas e técnicas novas de forma integrada ao fluxo de prompt, para mitigar ou reduzir alguns desses efeitos.

## Estudo de Caso: GitHub Copilot

Vamos encerrar esta seção entendendo como a engenharia de prompt é usada em soluções do mundo real ao olhar um Estudo de Caso: [GitHub Copilot](https://github.com/features/copilot?WT.mc_id=academic-105485-koreyst).

O GitHub Copilot é seu “programador par AI” — ele converte prompts de texto em conclusões de código e é integrado ao seu ambiente de desenvolvimento (por exemplo, Visual Studio Code) para uma experiência de usuário fluida. Conforme documentado na série de blogs abaixo, a versão mais antiga baseava-se no modelo OpenAI Codex — com engenheiros percebendo rapidamente a necessidade de ajustar o modelo e desenvolver melhores técnicas de engenharia de prompt para melhorar a qualidade do código. Em julho, eles [lançaram um modelo de IA aprimorado que vai além do Codex](https://github.blog/2023-07-28-smarter-more-efficient-coding-github-copilot-goes-beyond-codex-with-improved-ai-model/?WT.mc_id=academic-105485-koreyst) para sugestões ainda mais rápidas.

Leia os posts em ordem para acompanhar a jornada de aprendizado deles.

- **Maio de 2023** | [O GitHub Copilot está melhorando na compreensão do seu código](https://github.blog/2023-05-17-how-github-copilot-is-getting-better-at-understanding-your-code/?WT.mc_id=academic-105485-koreyst)
- **Maio de 2023** | [Dentro do GitHub: trabalhando com os LLMs por trás do GitHub Copilot](https://github.blog/2023-05-17-inside-github-working-with-the-llms-behind-github-copilot/?WT.mc_id=academic-105485-koreyst)
- **Junho de 2023** | [Como escrever prompts melhores para o GitHub Copilot](https://github.blog/2023-06-20-how-to-write-better-prompts-for-github-copilot/?WT.mc_id=academic-105485-koreyst)
- **Julho de 2023** | [.. GitHub Copilot vai além do Codex com modelo de IA aprimorado](https://github.blog/2023-07-28-smarter-more-efficient-coding-github-copilot-goes-beyond-codex-with-improved-ai-model/?WT.mc_id=academic-105485-koreyst)
- **Julho de 2023** | [Um guia do desenvolvedor para engenharia de prompt e LLMs](https://github.blog/2023-07-17-prompt-engineering-guide-generative-ai-llms/?WT.mc_id=academic-105485-koreyst)
- **Setembro de 2023** | [Como construir um app LLM empresarial: lições do GitHub Copilot](https://github.blog/2023-09-06-how-to-build-an-enterprise-llm-application-lessons-from-github-copilot/?WT.mc_id=academic-105485-koreyst)

Você também pode explorar o [Engineering blog](https://github.blog/category/engineering/?WT.mc_id=academic-105485-koreyst) deles para mais posts como [este](https://github.blog/2023-09-27-how-i-used-github-copilot-chat-to-build-a-reactjs-gallery-prototype/?WT.mc_id=academic-105485-koreyst) que mostra como esses modelos e técnicas são _aplicados_ para impulsionar aplicações do mundo real.

---

<!--
LESSON TEMPLATE:
This unit should cover core concept #2.
Reinforce the concept with examples and references.

CONCEPT #2:
Prompt Design.
Illustrated with examples.
-->

## Construção de Prompts

Vimos por que a engenharia de prompt é importante — agora vamos entender como os prompts são _construídos_ para que possamos avaliar diferentes técnicas de design de prompt mais eficazes.

### Prompt Básico

Vamos começar com o prompt básico: uma entrada de texto enviada ao modelo sem outro contexto. Aqui está um exemplo — quando enviamos as primeiras palavras do hino nacional dos EUA para a [Completion API](https://platform.openai.com/docs/api-reference/completions?WT.mc_id=academic-105485-koreyst) da OpenAI, ela completa instantaneamente a resposta com as próximas linhas, ilustrando o comportamento básico de predição.

| Prompt (Input)     | Completion (Output)                                                                                                                        |
| :----------------- | :----------------------------------------------------------------------------------------------------------------------------------------- |
| Oh say can you see | It sounds like you're starting the lyrics to "The Star-Spangled Banner," the national anthem of the United States. The full lyrics are ... |

### Prompt Complexo

Agora vamos adicionar contexto e instruções a esse prompt básico. A [Chat Completion API](https://learn.microsoft.com/azure/ai-services/openai/how-to/chatgpt?WT.mc_id=academic-105485-koreyst) nos permite construir um prompt complexo como uma coleção de _mensagens_ com:

- pares de entrada/saída refletindo entrada do _usuário_ e resposta do _assistente_.
- mensagem de sistema estabelecendo o contexto para o comportamento ou personalidade do assistente.

A solicitação agora está na forma abaixo, em que a _tokenização_ captura efetivamente as informações relevantes do contexto e da conversa. Assim, mudar o contexto do sistema pode ser tão impactante na qualidade das completions quanto as entradas do usuário fornecidas.

```python
response = openai.chat.completions.create(
    model="gpt-3.5-turbo",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Who won the world series in 2020?"},
        {"role": "assistant", "content": "The Los Angeles Dodgers won the World Series in 2020."},
        {"role": "user", "content": "Where was it played?"}
    ]
)
```

### Prompt de Instrução

Nos exemplos acima, o prompt do usuário era uma consulta de texto simples que pode ser interpretada como um pedido de informação. Com prompts de _instrução_, podemos usar esse texto para especificar uma tarefa em mais detalhes, fornecendo uma orientação melhor à IA. Aqui está um exemplo:

| Prompt (Input)                                                                                                                                                                                                                         | Completion (Output)                                                                                                        | Tipo de Instrução    |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------- | :------------------ |
| Write a description of the Civil War                                                                                                                                                                                                   | _returned a simple paragraph_                                                                                              | Simples              |
| Write a description of the Civil War. Provide key dates and events and describe their significance                                                                                                                                     | _returned a paragraph followed by a list of key event dates with descriptions_                                             | Complex             |
| Write a description of the Civil War in 1 paragraph. Provide 3 bullet points with key dates and their significance. Provide 3 more bullet points with key historical figures and their contributions. Return the output as a JSON file | _returns more extensive details in a text box, formatted as JSON that you can copy-paste to a file and validate as needed_ | Complex. Formatted. |

## Conteúdo Primário

Nos exemplos acima, o prompt ainda era bastante aberto, permitindo que o LLM decidisse qual parte do seu conjunto pré-treinado era relevante. Com o padrão de design de _conteúdo primário_, o texto de entrada é dividido em duas partes:

- uma instrução (ação)
- conteúdo relevante (que influencia a ação)

Aqui está um exemplo em que a instrução é “resuma isso em 2 frases curtas”.

| Prompt (Input)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Completion (Output)                                                                                                                                                                                                                                                                             |
| :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Jupiter is the fifth planet from the Sun and the largest in the Solar System. It is a gas giant with a mass one-thousandth that of the Sun, but two-and-a-half times that of all the other planets in the Solar System combined. Jupiter is one of the brightest objects visible to the naked eye in the night sky, and has been known to ancient civilizations since before recorded history. It is named after the Roman god Jupiter.[19] When viewed from Earth, Jupiter can be bright enough for its reflected light to cast visible shadows,[20] and is on average the third-brightest natural object in the night sky after the Moon and Venus. <br/> **Summarize this in 2 short sentences** | Jupiter, the fifth planet from the Sun, is the largest in the Solar System and is known for being one of the brightest objects in the night sky. Named after the Roman god Jupiter, it's a gas giant whose mass is two-and-a-half times that of all other planets in the Solar System combined. |

O segmento de conteúdo primário pode ser usado de várias maneiras para conduzir instruções mais eficazes:

- **Exemplos** — em vez de dizer ao modelo o que fazer com uma instrução explícita, forneça exemplos do que fazer e permita que ele infira o padrão.
- **Sugestões** — siga a instrução com uma “sugestão” que prepare a conclusão, orientando o modelo em direção a respostas mais relevantes.
- **Templates** — são receitas repetíveis de prompts com espaços reservados (variáveis) que podem ser personalizadas com dados para casos de uso específicos.

Vamos explorar isso na prática.

### Usando Exemplos

Essa é uma abordagem em que você usa o conteúdo primário para “alimentar o modelo” com alguns exemplos do resultado desejado para uma determinada instrução, e deixa o modelo inferir o padrão do resultado desejado. Dependendo do número de exemplos fornecidos, podemos ter prompt zero-shot, one-shot, few-shot etc.

O prompt agora consiste em três componentes:

- Uma descrição da tarefa
- Alguns exemplos do resultado desejado
- O início de um novo exemplo (que se torna uma descrição implícita de tarefa)

| Tipo de Aprendizado | Prompt (Input)                                                                                                                                        | Completion (Output)         |
| :------------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------- |
| Zero-shot           | "The Sun is Shining". Translate to Spanish                                                                                                            | "El Sol está brillando".    |
| One-shot            | "The Sun is Shining" => ""El Sol está brillando". <br> "It's a Cold and Windy Day" =>                                                                 | "Es un día frío y ventoso". |
| Few-shot            | The player ran the bases => Baseball <br/> The player hit an ace => Tennis <br/> The player hit a six => Cricket <br/> The player made a slam-dunk => | Basketball                  |
|                     |                                                                                                                                                     |                             |

Perceba como tivemos que fornecer instrução explícita (“Translate to Spanish”) na prompt zero-shot, mas ela é inferida no exemplo one-shot. O exemplo few-shot mostra como adicionar mais exemplos permite que os modelos façam inferências mais precisas sem instruções adicionais.

### Sugestões de Prompt

Outra técnica para usar o conteúdo primário é fornecer _sugestões_ em vez de exemplos. Nesse caso, estamos dando ao modelo um empurrão na direção certa ao _começar_ com um trecho que reflete o formato de resposta desejado. O modelo então “segue a sugestão” para continuar nessa direção.

| Número de Sugestões | Prompt (Input)                                                                                                                                                                                                                                                                                                                                                                                                                                               | Completion (Output)                                                                                                                                                                                                                                                                                       |
| :------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0                   | Jupiter is the fifth planet from the Sun and the largest in the Solar System. It is a gas giant with a mass one-thousandth that of the Sun, but two-and-a-half times that of all the other planets in the Solar System combined. Jupiter is one of the brightest objects visible to the naked eye in the night sky, and has been known to ancient civilizations since before recorded history. <br/>**Summarize This**                                       | Jupiter is the largest planet in our Solar System and the fifth one from the Sun. It is a gas giant with a mass 1/1000th of the Sun's, but it is heavier than all the other planets combined. Ancient civilizations have known about Jupiter for a long time, and it is easily visible in the night sky.. |
| 1                   | Jupiter is the fifth planet from the Sun and the largest in the Solar System. It is a gas giant with a mass one-thousandth that of the Sun, but two-and-a-half times that of all the other planets in the Solar System combined. Jupiter is one of the brightest objects visible to the naked eye in the night sky, and has been known to ancient civilizations since before recorded history. <br/>**Summarize This** <br/> What we learned is that Jupiter | is the fifth planet from the Sun and the largest in the Solar System. It is a gas giant with a mass one-thousandth that of the Sun, but two-and-a-half times that of all the other planets combined. It is easily visible to the naked eye and has been known since ancient times.                        |
| 2                   | Jupiter is the fifth planet from the Sun and the largest in the Solar System. It is a gas giant with a mass one-thousandth that of the Sun, but two-and-a-half times that of all the other planets in the Solar System combined. Jupiter is one of the brightest objects visible to the naked eye in the night sky, and has been known to ancient civilizations since before recorded history. <br/>**Summarize This** <br/> Top 3 Facts We Learned:         | 1. Jupiter is the fifth planet from the Sun and the largest in the Solar System. <br/> 2. It is a gas giant with a mass one-thousandth that of the Sun...<br/> 3. Jupiter has been visible to the naked eye since ancient times ...                                                                       |
|                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                                           |

### Templates de Prompt

Um template de prompt é uma _receita pré-definida para um prompt_ que pode ser armazenada e reutilizada conforme necessário, para gerar experiências de usuário mais consistentes em escala. Em sua forma mais simples, é apenas uma coleção de exemplos de prompt como [este da OpenAI](https://platform.openai.com/examples?WT.mc_id=academic-105485-koreyst) que fornece tanto os componentes interativos do prompt (mensagens do usuário e do sistema) quanto o formato de requisição orientado à API — para suportar reutilização.

Em sua forma mais complexa, como [este exemplo do LangChain](https://python.langchain.com/docs/concepts/prompt_templates/?WT.mc_id=academic-105485-koreyst), ele contém _placeholders_ que podem ser substituídos por dados de várias fontes (entrada do usuário, contexto do sistema, fontes de dados externas etc.) para gerar um prompt dinamicamente. Isso nos permite criar uma biblioteca de prompts reutilizáveis que podem ser usados para conduzir experiências de usuário consistentes **programaticamente** em escala.

Finalmente, o valor real dos templates está na capacidade de criar e publicar _bibliotecas de prompts_ para domínios verticais de aplicação — onde o template de prompt agora é _otimizado_ para refletir contexto ou exemplos específicos do aplicativo que tornam as respostas mais relevantes e precisas para o público-alvo. O repositório [Prompts For Edu](https://github.com/microsoft/prompts-for-edu?WT.mc_id=academic-105485-koreyst) é um ótimo exemplo dessa abordagem, curando uma biblioteca de prompts para o domínio educacional com foco em objetivos-chave como planejamento de aulas, design curricular, tutoria de estudantes etc.

## Conteúdo de Apoio

Se pensarmos na construção de prompts como tendo uma instrução (tarefa) e um alvo (conteúdo primário), então o _conteúdo secundário_ é como contexto adicional que fornecemos para **influenciar a saída de alguma forma**. Pode ser parâmetros de ajuste, instruções de formatação, taxonomias de tópico etc. que ajudam o modelo a _adaptar_ sua resposta ao objetivo ou expectativas do usuário.

Por exemplo: Dado um catálogo de cursos com metadados extensos (nome, descrição, nível, tags de metadados, instrutor etc.) sobre todos os cursos disponíveis no currículo:

- podemos definir uma instrução para “resumir o catálogo de cursos para o Outono de 2023”
- podemos usar o conteúdo primário para fornecer alguns exemplos da saída desejada
- podemos usar o conteúdo secundário para identificar as 5 principais “tags” de interesse.

Agora, o modelo pode fornecer um resumo no formato mostrado pelos poucos exemplos — mas se um resultado tiver várias tags, ele pode priorizar as 5 tags identificadas no conteúdo secundário.

---

<!--
LESSON TEMPLATE:
This unit should cover core concept #1.
Reinforce the concept with examples and references.

CONCEPT #3:
Prompt Engineering Techniques.
What are some basic techniques for prompt engineering?
Illustrate it with some exercises.
-->

## Melhores Práticas de Prompt

Agora que sabemos como os prompts podem ser _construídos_, podemos começar a pensar em como _desenhá-los_ para refletir boas práticas. Podemos pensar sobre isso em duas partes — ter a mentalidade certa e aplicar as técnicas certas.

### Mentalidade de Engenharia de Prompt

Engenharia de Prompt é um processo de tentativa e erro, então mantenha três fatores orientadores em mente:

1. **Entender o domínio importa.** A precisão e relevância da resposta é uma função do _domínio_ em que aquela aplicação ou usuário opera. Aplique sua intuição e expertise de domínio para **customizar técnicas** ainda mais. Por exemplo, defina _personalidades específicas de domínio_ em seus prompts de sistema, ou use _templates específicos do domínio_ em seus prompts de usuário. Forneça conteúdo secundário que reflita contextos específicos do domínio, ou use _sugestões e exemplos específicos do domínio_ para guiar o modelo a padrões de uso familiares.

2. **Entender o modelo importa.** Sabemos que modelos são estocásticos por natureza. Mas as implementações de modelo também podem variar em termos do conjunto de dados de treinamento que usam (conhecimento pré-treinado), das capacidades que fornecem (por exemplo, via API ou SDK) e do tipo de conteúdo que são otimizados (por exemplo, código vs. imagens vs. texto). Entenda os pontos fortes e limitações do modelo que você está usando e use esse conhecimento para _priorizar tarefas_ ou construir _templates personalizados_ otimizados para as capacidades do modelo.

3. **Iteração e validação importam.** Os modelos estão evoluindo rapidamente, e também estão as técnicas de engenharia de prompt. Como especialista no domínio, você pode ter outro contexto ou critérios _do seu_ aplicativo específico, que podem não se aplicar à comunidade em geral. Use ferramentas e técnicas de engenharia de prompt para “dar um impulso” à construção do prompt, depois itere e valide os resultados usando sua própria intuição e expertise de domínio. Registre seus insights e crie uma **base de conhecimento** (por exemplo, bibliotecas de prompts) que possa ser usada como nova linha de base por outros, para iterações mais rápidas no futuro.

## Boas Práticas

Agora vamos olhar para boas práticas comuns recomendadas por [OpenAI](https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-openai-api?WT.mc_id=academic-105485-koreyst) e por profissionais de [Azure OpenAI](https://learn.microsoft.com/azure/ai-services/openai/concepts/prompt-engineering#best-practices?WT.mc_id=academic-105485-koreyst).

| O que                              | Por que                                                                                                                                                                                                                                               |
| :-------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Avalie os modelos mais recentes.  | Gerações de modelo mais novas provavelmente terão recursos e qualidade aprimorados — mas também podem incorrer em custos mais altos. Avalie-os pelo impacto e depois tome decisões de migração.                                              |
| Separe instruções e contexto      | Verifique se seu modelo/provedor define _delimitadores_ para distinguir instruções, conteúdo primário e conteúdo secundário de forma mais clara. Isso pode ajudar os modelos a atribuir pesos mais precisos aos tokens.                      |
| Seja específico e claro            | Dê mais detalhes sobre o contexto desejado, resultado, comprimento, formato, estilo etc. Isso melhorará tanto a qualidade quanto a consistência das respostas. Capture receitas em templates reutilizáveis.                               |
| Seja descritivo, use exemplos     | Modelos podem responder melhor a uma abordagem de “mostrar e contar”. Comece com uma abordagem `zero-shot` onde você dá uma instrução (mas sem exemplos) e depois tente `few-shot` como refinamento, fornecendo alguns exemplos do resultado desejado. Use analogias. |
| Use sugestões para iniciar respostas | Encaminhe o modelo para um resultado desejado dando palavras ou frases iniciais que ele possa usar como ponto de partida para a resposta.                                                                                                      |
| Insista                          | Às vezes você pode precisar se repetir para o modelo. Dê instruções antes e depois do seu conteúdo primário, use uma instrução e uma sugestão, etc. Itere e valide para ver o que funciona.                                                   |
| A ordem importa                   | A ordem em que você apresenta informações ao modelo pode impactar a saída, mesmo nos exemplos de aprendizado, devido ao viés de recência. Experimente diferentes opções para ver o que funciona melhor.                                        |
| Dê uma “saída” ao modelo         | Dê ao modelo uma resposta de _fallback_ que ele possa fornecer se não conseguir completar a tarefa por algum motivo. Isso pode reduzir as chances de o modelo gerar respostas falsas ou fabricadas.                                         |
|                                   |                                                                                                                                                                                                                                                       |

Como em qualquer boa prática, lembre-se de que _seu resultado pode variar_ com base no modelo, na tarefa e no domínio. Use isso como ponto de partida e itere para encontrar o que funciona melhor para você. Reavalie constantemente seu processo de engenharia de prompt à medida que novos modelos e ferramentas se tornam disponíveis, com foco na escalabilidade do processo e na qualidade das respostas.

<!--
LESSON TEMPLATE:
This unit should provide a code challenge if applicable

CHALLENGE:
Link to a Jupyter Notebook with only the code comments in the instructions (code sections are empty).

SOLUTION:
Link to a copy of that Notebook with the prompts filled in and run, showing what one example could be.
-->

## Exercício

Parabéns! Você chegou ao final da lição! É hora de colocar alguns desses conceitos e técnicas à prova com exemplos reais!

Para nosso exercício, usaremos um Jupyter Notebook com exercícios que você pode completar interativamente. Você também pode estender o Notebook com suas próprias células de Markdown e Código para explorar ideias e técnicas por conta própria.

### Para começar, faça um fork do repositório e depois

- (Recomendado) Inicie o GitHub Codespaces
- (Alternativamente) Clone o repositório para seu dispositivo local e use-o com Docker Desktop
- (Alternativamente) Abra o Notebook com seu ambiente de runtime preferido.

### Em seguida, configure suas variáveis de ambiente

- Copie o arquivo `.env.copy` na raiz do repositório para `.env` e preencha os valores `AZURE_OPENAI_API_KEY`, `AZURE_OPENAI_ENDPOINT` e `AZURE_OPENAI_DEPLOYMENT`. Volte à seção [Sandbox de Aprendizado](#learning-sandbox) para saber como.

### Em seguida, abra o Jupyter Notebook

- Selecione o kernel de runtime. Se estiver usando as opções 1 ou 2, basta selecionar o kernel Python 3.10.x padrão fornecido pelo dev container.

Você está pronto para executar os exercícios. Observe que não há respostas _certas ou erradas_ aqui — apenas explorar opções por tentativa e erro e construir intuição sobre o que funciona para um determinado modelo e domínio de aplicação.

_Por esse motivo, não há segmentos de Solução de Código nesta lição. Em vez disso, o Notebook terá células de Markdown intituladas “Minha Solução:” que mostram um exemplo de saída como referência._

## Verificação de conhecimento

Qual das seguintes é um bom prompt seguindo algumas práticas razoáveis?

1. Show me an image of red car
1. Show me an image of red car of make Volvo and model XC90 parked by a cliff with the sun setting
1. Show me an image of red car of make Volvo and model XC90

R: 2, é o melhor prompt porque fornece detalhes sobre o “o quê” e entra em especificações (não apenas qualquer carro, mas uma marca e modelo específicos) e também descreve o cenário geral. 3 é o segundo melhor, pois também contém muita descrição.

## 🚀 Desafio

Veja se você consegue aproveitar a técnica de “sugestão” com o prompt: Complete the sentence "Show me an image of red car of make Volvo and ". Como ele responde, e como você melhoraria?

## Excelente trabalho! Continue aprendendo

Quer aprender mais sobre diferentes conceitos de Engenharia de Prompt? Vá para a [página de aprendizado continuado](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) para encontrar outros ótimos recursos sobre este tópico.

Vá para a Lição 5, onde veremos [técnicas avançadas de prompting](../05-advanced-prompts/README.md?WT.mc_id=academic-105485-koreyst)!
