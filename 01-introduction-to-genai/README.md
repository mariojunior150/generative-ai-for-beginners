# Introdução à IA Generativa e Grandes Modelos de Linguagem

[![Introduction to Generative AI and Large Language Models](./images/01-lesson-banner.png?WT.mc_id=academic-105485-koreyst)](https://youtu.be/lFXQkBvEe0o?si=6ZBcQTwLJJDpnX0K)

> _Clique na imagem acima para ver o vídeo desta lição_

IA generativa é inteligência artificial capaz de gerar texto, imagens e outros tipos de conteúdo. O que a torna uma tecnologia fantástica é que ela democratiza a IA: qualquer pessoa pode usá-la com tão pouco quanto um prompt de texto, uma frase escrita em linguagem natural. Não é preciso aprender uma linguagem como Java ou SQL para realizar algo relevante; tudo o que você precisa é usar sua linguagem, dizer o que deseja e surge uma sugestão de um modelo de IA. As aplicações e o impacto disso são enormes: você escreve ou entende relatórios, escreve aplicações e muito mais, tudo em segundos.

Neste currículo, exploraremos como nossa startup aproveita a IA generativa para desbloquear novos cenários no mundo da educação e como abordamos os desafios inevitáveis associados às implicações sociais de sua aplicação e às limitações da tecnologia.

## Introdução

Esta lição abordará:

- Introdução ao cenário de negócio: a ideia e missão da nossa startup.
- IA generativa e como chegamos ao cenário tecnológico atual.
- Funcionamento interno de um grande modelo de linguagem.
- Principais capacidades e casos de uso práticos de Grandes Modelos de Linguagem.

## Objetivos de Aprendizagem

Após concluir esta lição, você entenderá:

- O que é IA generativa e como funcionam os Grandes Modelos de Linguagem.
- Como você pode aproveitar grandes modelos de linguagem para diferentes casos de uso, com foco em cenários educacionais.

## Cenário: nossa startup educacional

A Inteligência Artificial Generativa (IA) representa o auge da tecnologia de IA, ampliando os limites do que antes era considerado impossível. Modelos de IA generativa têm várias capacidades e aplicações, mas neste currículo exploraremos como ela está revolucionando a educação por meio de uma startup fictícia. Chamaremos essa startup de _nossa startup_. Nossa startup atua no domínio da educação com a ambiciosa declaração de missão:

> _melhorar a acessibilidade no aprendizado, em escala global, garantindo acesso equitativo à educação e oferecendo experiências de aprendizagem personalizadas a cada estudante, de acordo com suas necessidades_.

Nossa equipe da startup sabe que não será possível alcançar esse objetivo sem aproveitar uma das ferramentas mais poderosas dos tempos modernos — os Grandes Modelos de Linguagem (LLMs).

Espera-se que a IA generativa revolucione a maneira como aprendemos e ensinamos hoje, com estudantes tendo à disposição professores virtuais 24 horas por dia que fornecem grandes quantidades de informação e exemplos, e professores podendo utilizar ferramentas inovadoras para avaliar seus alunos e dar feedback.

![Cinco jovens estudantes olhando para um monitor - imagem por DALLE2](./images/students-by-DALLE2.png?WT.mc_id=academic-105485-koreyst)

Para começar, vamos definir alguns conceitos e termos básicos que usaremos ao longo do currículo.

## Como chegamos à IA Generativa?

Apesar do extraordinário _hype_ criado recentemente pelo anúncio de modelos de IA generativa, essa tecnologia tem décadas em desenvolvimento, com os primeiros esforços de pesquisa datando dos anos 60. Agora estamos em um ponto em que a IA possui capacidades cognitivas humanas, como conversação, como mostrado por exemplo pelo [OpenAI ChatGPT](https://openai.com/chatgpt) ou pelo [Bing Chat](https://www.microsoft.com/edge/features/bing-chat?WT.mc_id=academic-105485-koreyst), que também usa um modelo GPT para as conversas de busca da web do Bing.

Voltando um pouco, os primeiros protótipos de IA consistiam em chatbots escritos, baseados em uma base de conhecimento extraída de um grupo de especialistas e representada em um computador. As respostas na base de conhecimento eram acionadas por palavras-chave aparecendo no texto de entrada. No entanto, logo ficou claro que essa abordagem não escalava bem.

### Uma abordagem estatística para IA: Machine Learning

Um ponto de virada chegou durante os anos 90, com a aplicação de uma abordagem estatística à análise de texto. Isso levou ao desenvolvimento de novos algoritmos — conhecidos como machine learning — capazes de aprender padrões a partir de dados sem serem explicitamente programados. Essa abordagem permite que máquinas simulem a compreensão da linguagem humana: um modelo estatístico é treinado em pares texto-rótulo, permitindo que ele classifique um texto de entrada desconhecido com um rótulo pré-definido que representa a intenção da mensagem.

### Redes neurais e assistentes virtuais modernos

Nos últimos anos, a evolução tecnológica do hardware, capaz de lidar com maiores quantidades de dados e cálculos mais complexos, incentivou a pesquisa em IA, levando ao desenvolvimento de algoritmos avançados de machine learning conhecidos como redes neurais ou deep learning.

Redes neurais (e, em particular, Redes Neurais Recorrentes – RNNs) melhoraram significativamente o processamento de linguagem natural, possibilitando a representação do significado do texto de maneira mais relevante, valorizando o contexto de uma palavra em uma frase.

É essa tecnologia que impulsionou os assistentes virtuais surgidos na primeira década do novo século, muito proficientes em interpretar a linguagem humana, identificar uma necessidade e executar uma ação para satisfazê-la — como responder com um roteiro pré-definido ou consumir um serviço de terceiros.

### Hoje em dia, IA Generativa

Assim chegamos à IA Generativa de hoje, que pode ser vista como um subconjunto de deep learning.

![AI, ML, DL and Generative AI](./images/AI-diagram.png?WT.mc_id=academic-105485-koreyst)

Após décadas de pesquisa na área de IA, uma nova arquitetura de modelo — chamada _Transformer_ — superou os limites das RNNs, sendo capaz de processar sequências de texto muito mais longas como entrada. Transformers se baseiam no mecanismo de atenção, permitindo que o modelo atribua pesos diferentes às entradas que recebe, “prestando mais atenção” onde a informação mais relevante está concentrada, independentemente da ordem na sequência de texto.

A maioria dos modelos recentes de IA generativa — também conhecidos como Grandes Modelos de Linguagem (LLMs), já que trabalham com entradas e saídas textuais — é, de fato, baseada nessa arquitetura. O interessante sobre esses modelos — treinados em uma enorme quantidade de dados não rotulados de fontes diversas como livros, artigos e sites — é que eles podem ser adaptados para uma ampla variedade de tarefas e gerar texto gramaticalmente correto com um semblante de criatividade. Assim, eles não apenas ampliaram incrivelmente a capacidade de uma máquina de “entender” um texto de entrada, mas também possibilitaram sua capacidade de gerar uma resposta original em linguagem humana.

## Como funcionam os grandes modelos de linguagem?

No próximo capítulo vamos explorar diferentes tipos de modelos de IA generativa, mas por enquanto vamos olhar como grandes modelos de linguagem funcionam, com foco nos modelos OpenAI GPT (Generative Pre-trained Transformer).

- **Tokenizador, texto para números**: Grandes Modelos de Linguagem recebem um texto como entrada e geram um texto como saída. Contudo, por serem modelos estatísticos, eles funcionam muito melhor com números do que com sequências de texto. Por isso, toda entrada ao modelo é processada por um tokenizador antes de ser usada pelo modelo principal. Um token é um pedaço de texto — consistindo em um número variável de caracteres — então a tarefa principal do tokenizador é dividir a entrada em um array de tokens. Em seguida, cada token é mapeado para um índice de token, que é a codificação inteira do pedaço de texto original.

![Example of tokenization](./images/tokenizer-example.png?WT.mc_id=academic-105485-koreyst)

- **Predição de tokens de saída**: Dado n tokens como entrada (com o valor máximo de n variando de um modelo para outro), o modelo é capaz de prever um token como saída. Esse token é então incorporado à entrada da próxima iteração, em um padrão de janela expansiva, possibilitando uma melhor experiência ao usuário ao obter uma ou várias frases como resposta. Isso explica por que, se você já brincou com o ChatGPT, pode ter percebido que às vezes ele parece parar no meio de uma frase.

- **Processo de seleção, distribuição de probabilidade**: O token de saída é escolhido pelo modelo de acordo com sua probabilidade de ocorrer após a sequência de texto atual. Isso porque o modelo prevê uma distribuição de probabilidade sobre todos os possíveis “próximos tokens”, calculada com base em seu treinamento. No entanto, nem sempre é escolhido o token com maior probabilidade da distribuição resultante. Um grau de aleatoriedade é adicionado a essa escolha, de forma que o modelo opere de maneira não determinística — não obtemos a mesma saída exata para a mesma entrada. Esse grau de aleatoriedade é adicionado para simular o processo de pensamento criativo e pode ser ajustado usando um parâmetro do modelo chamado temperature.

## Como nossa startup pode aproveitar Grandes Modelos de Linguagem?

Agora que temos uma compreensão melhor do funcionamento interno de um grande modelo de linguagem, vamos ver alguns exemplos práticos das tarefas mais comuns que eles podem realizar muito bem, com foco em nosso cenário de negócio.
Dissemos que a principal capacidade de um Grande Modelo de Linguagem é _gerar um texto do zero, a partir de uma entrada textual escrita em linguagem natural_.

Mas que tipo de entrada e saída textual?
A entrada de um grande modelo de linguagem é conhecida como prompt, enquanto a saída é conhecida como completion, termo que se refere ao mecanismo do modelo de gerar o próximo token para completar a entrada atual. Vamos nos aprofundar no que é um prompt e como desenhá-lo para obter o máximo do nosso modelo. Mas, por agora, digamos apenas que um prompt pode incluir:

- Uma **instrução** especificando o tipo de saída que esperamos do modelo. Essa instrução às vezes pode incorporar alguns exemplos ou dados adicionais.

  1. Resumo de um artigo, livro, avaliações de produtos e muito mais, juntamente com extração de insights de dados não estruturados.
    
    ![Example of summarization](./images/summarization-example.png?WT.mc_id=academic-105485-koreyst)
  
  2. Ideação criativa e elaboração de um artigo, redação, tarefa ou mais.
      
     ![Example of creative writing](./images/creative-writing-example.png?WT.mc_id=academic-105485-koreyst)

- Uma **pergunta**, feita na forma de uma conversa com um agente.
  
  ![Example of conversation](./images/conversation-example.png?WT.mc_id=academic-105485-koreyst)

- Um pedaço de **texto para completar**, que implicitamente é um pedido de assistência de escrita.
  
  ![Example of text completion](./images/text-completion-example.png?WT.mc_id=academic-105485-koreyst)

- Um pedaço de **código** junto com o pedido de explicá-lo e documentá-lo, ou um comentário pedindo para gerar um trecho de código que execute uma tarefa específica.
  
  ![Coding example](./images/coding-example.png?WT.mc_id=academic-105485-koreyst)

Os exemplos acima são bastante simples e não têm a intenção de ser uma demonstração exaustiva das capacidades dos Grandes Modelos de Linguagem. Eles servem para mostrar o potencial do uso da IA generativa, em contextos educacionais em particular, mas não se limitam a eles.

Além disso, a saída de um modelo de IA generativa não é perfeita e, às vezes, a criatividade do modelo pode jogar contra ele, resultando em uma saída que é uma combinação de palavras que o usuário humano pode interpretar como uma mistificação da realidade, ou pode ser ofensiva. IA generativa não é inteligente — pelo menos na definição mais ampla de inteligência, incluindo raciocínio crítico e criativo ou inteligência emocional; ela não é determinística e não é confiável, já que fabricações, como referências, conteúdo e afirmações incorretas, podem ser combinadas com informações corretas e apresentadas de maneira persuasiva e confiante. Nas próximas lições, lidaremos com todas essas limitações e veremos o que podemos fazer para mitigá-las.

## Exercício

Sua tarefa é ler mais sobre [IA generativa](https://en.wikipedia.org/wiki/Generative_artificial_intelligence?WT.mc_id=academic-105485-koreyst) e tentar identificar uma área em que você adicionaria IA generativa hoje, que ainda não a utiliza. Como o impacto seria diferente do “jeito antigo”? Você poderia fazer algo que não podia antes ou seria mais rápido? Escreva um resumo de 300 palavras sobre como seria sua startup de IA dos sonhos e inclua cabeçalhos como “Problema”, “Como eu usaria IA”, “Impacto” e opcionalmente um plano de negócios.

Se você fizer essa tarefa, pode até estar pronto para se inscrever no programa de incubação da Microsoft, o [Microsoft for Startups Founders Hub](https://www.microsoft.com/startups?WT.mc_id=academic-105485-koreyst): oferecemos créditos para Azure, OpenAI, mentoria e muito mais. Confira!

## Verificação de conhecimento

O que é verdadeiro sobre grandes modelos de linguagem?

1. Você obtém a mesma resposta exata todas as vezes.
1. Eles fazem as coisas perfeitamente, são ótimos em somar números e produzir código funcional, etc.
1. A resposta pode variar apesar de usar o mesmo prompt. Também é ótimo para lhe dar um primeiro rascunho de algo, seja texto ou código. Mas você precisa aperfeiçoar os resultados.

R: 3, um LLM é não determinístico, a resposta varia; no entanto, você pode controlar sua variância por meio da configuração de temperatura. Você também não deve esperar que ele faça as coisas perfeitamente; ele está aqui para fazer o trabalho pesado por você, o que muitas vezes significa que você obtém uma boa primeira tentativa em algo que precisa melhorar gradualmente.

## Excelente trabalho! Continue sua jornada

Após concluir esta lição, confira nossa [coleção de aprendizado de IA generativa](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) para continuar desenvolvendo seu conhecimento em IA generativa!

Vá para a Lição 2, onde veremos como [explorar e comparar diferentes tipos de LLMs](../02-exploring-and-comparing-different-llms/README.md?WT.mc_id=academic-105485-koreyst)!
