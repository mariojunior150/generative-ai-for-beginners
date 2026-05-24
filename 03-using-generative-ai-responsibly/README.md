# Usando IA Generativa de Forma Responsável

[![Using Generative AI Responsibly](./images/03-lesson-banner.png?WT.mc_id=academic-105485-koreyst)](https://youtu.be/YOp-e1GjZdA?si=7Wv4wu3x44L1DCVj)

> _Clique na imagem acima para ver o vídeo desta lição_

É fácil se encantar com IA e, em particular, com IA generativa, mas é preciso considerar como usá-la de forma responsável. É necessário pensar em aspectos como garantir que a saída seja justa, não prejudicial e mais. Este capítulo tem como objetivo fornecer o contexto mencionado, o que considerar e como tomar medidas ativas para melhorar seu uso de IA.

## Introdução

Nesta lição, abordaremos:

- Por que você deve priorizar IA responsável ao construir aplicações de IA generativa.
- Princípios fundamentais da IA responsável e como eles se relacionam com IA generativa.
- Como colocar esses princípios de IA responsável em prática por meio de estratégia e ferramentas.

## Objetivos de Aprendizagem

Após concluir esta lição, você saberá:

- A importância da IA responsável ao construir aplicações de IA generativa.
- Quando pensar e aplicar os princípios centrais de IA responsável ao construir aplicações de IA generativa.
- Quais ferramentas e estratégias estão disponíveis para colocar o conceito de IA responsável em prática.

## Princípios de IA Responsável

O entusiasmo em torno da IA generativa nunca foi tão grande. Esse entusiasmo trouxe muitos novos desenvolvedores, atenção e investimentos para esse espaço. Embora isso seja muito positivo para quem deseja construir produtos e empresas usando IA generativa, também é importante avançarmos com responsabilidade.

Ao longo deste curso, estamos focando em construir nossa startup e nosso produto educacional de IA. Usaremos os princípios de IA responsável: Equidade, Inclusividade, Confiabilidade/Segurança, Segurança e Privacidade, Transparência e Responsabilidade. Com esses princípios, exploraremos como eles se relacionam ao uso de IA generativa em nossos produtos.

## Por que você deve priorizar IA responsável

Ao construir um produto, adotar uma abordagem centrada no ser humano, colocando o melhor interesse do seu usuário em primeiro lugar, leva aos melhores resultados.

A singularidade da IA generativa está em seu poder de criar respostas úteis, informações, orientação e conteúdo para os usuários. Isso pode ser feito sem muitos passos manuais, o que pode levar a resultados muito impressionantes. Sem planejamento e estratégias adequadas, isso também pode, infelizmente, gerar resultados prejudiciais para seus usuários, seu produto e a sociedade como um todo.

Vamos ver alguns (mas não todos) desses resultados potencialmente prejudiciais:

### Alucinações

Alucinações são um termo usado para descrever quando um LLM produz conteúdo que é completamente sem sentido ou algo que sabemos ser factualmente incorreto com base em outras fontes de informação.

Vamos tomar como exemplo a construção de um recurso para nossa startup que permite que estudantes façam perguntas históricas a um modelo. Um estudante pergunta: `Quem foi o único sobrevivente do Titanic?`

O modelo produz uma resposta como a abaixo:

![Prompt dizendo "Who was the sole survivor of the Titanic"](../03-using-generative-ai-responsibly/images/ChatGPT-titanic-survivor-prompt.webp?WT.mc_id=academic-105485-koreyst)

> _(Fonte: [Flying bisons](https://flyingbisons.com?WT.mc_id=academic-105485-koreyst))_

Esta é uma resposta muito confiante e detalhada. Infelizmente, ela está incorreta. Mesmo com uma pesquisa mínima, alguém descobriria que houve mais de um sobrevivente do desastre do Titanic. Para um estudante que está começando a pesquisar esse tópico, essa resposta pode ser persuasiva o suficiente para não ser questionada e ser tratada como fato. As consequências disso podem tornar o sistema de IA pouco confiável e impactar negativamente a reputação da nossa startup.

A cada iteração de qualquer LLM, temos visto melhorias de desempenho em minimizar alucinações. Mesmo com essa melhoria, nós, como construtores de aplicações e usuários, ainda precisamos estar cientes dessas limitações.

### Conteúdo prejudicial

Já abordamos na seção anterior quando um LLM produz respostas incorretas ou sem sentido. Outro risco do qual precisamos estar cientes é quando um modelo responde com conteúdo prejudicial.

Conteúdo prejudicial pode ser definido como:

- Fornecer instruções ou encorajar automutilação ou dano a determinados grupos.
- Conteúdo odioso ou rebaixante.
- Orientações para planejar qualquer tipo de ataque ou ato violento.
- Fornecer instruções sobre como encontrar conteúdo ilegal ou cometer atos ilegais.
- Exibir conteúdo sexualmente explícito.

Para nossa startup, queremos garantir que tenhamos as ferramentas e estratégias adequadas para impedir que esse tipo de conteúdo seja visto pelos estudantes.

### Falta de equidade

Equidade é definida como “garantir que um sistema de IA seja livre de vieses e discriminação e que trate todas as pessoas de forma justa e igual.” No mundo da IA generativa, queremos garantir que visões de mundo excludentes de grupos marginalizados não sejam reforçadas pela saída do modelo.

Esses tipos de resultados não são apenas destrutivos para a construção de experiências de produto positivas para nossos usuários, mas também causam danos sociais adicionais. Como construtores de aplicações, devemos sempre ter em mente uma base de usuários ampla e diversa ao criar soluções com IA generativa.

## Como usar IA generativa de forma responsável

Agora que identificamos a importância da IA generativa responsável, vamos olhar para 4 passos que podemos tomar para construir nossas soluções de IA de forma responsável:

![Mitigate Cycle](./images/mitigate-cycle.png?WT.mc_id=academic-105485-koreyst)

### Medir os danos potenciais

Em testes de software, testamos as ações esperadas de um usuário em uma aplicação. Da mesma forma, testar um conjunto diverso de prompts que os usuários provavelmente irão usar é uma boa maneira de medir danos potenciais.

Como nossa startup está construindo um produto educacional, seria bom preparar uma lista de prompts relacionados à educação. Isso pode cobrir um determinado assunto, fatos históricos e prompts sobre a vida estudantil.

### Mitigar os danos potenciais

Agora é hora de encontrar maneiras de prevenir ou limitar os danos potenciais causados pelo modelo e suas respostas. Podemos olhar para isso em 4 camadas diferentes:

![Mitigation Layers](./images/mitigation-layers.png?WT.mc_id=academic-105485-koreyst)

- **Modelo**. Escolher o modelo certo para o caso de uso certo. Modelos maiores e mais complexos, como o GPT-4, podem apresentar mais risco de conteúdo prejudicial quando aplicados a casos de uso menores e mais específicos. Usar seus dados de treinamento para ajustar o modelo também reduz o risco de conteúdo prejudicial.

- **Sistema de segurança**. Um sistema de segurança é um conjunto de ferramentas e configurações na plataforma que serve o modelo e ajuda a mitigar danos. Um exemplo disso é o sistema de filtragem de conteúdo no serviço Azure OpenAI. Os sistemas também devem detectar ataques de jailbreak e atividades indesejadas como solicitações de bots.

- **Metaprompt**. Metaprompts e grounding são formas de direcionar ou limitar o modelo com base em certos comportamentos e informações. Isso pode ser feito usando entradas de sistema para definir certos limites do modelo. Além disso, fornecer saídas que sejam mais relevantes para o escopo ou domínio do sistema.

Também pode envolver técnicas como Retrieval Augmented Generation (RAG) para fazer com que o modelo busque informações apenas em uma seleção de fontes confiáveis. Há uma lição posterior neste curso sobre [construir aplicações de busca](../08-building-search-applications/README.md?WT.mc_id=academic-105485-koreyst)

- **Experiência do usuário**. A camada final é onde o usuário interage diretamente com o modelo por meio da interface da nossa aplicação de alguma forma. Dessa forma, podemos projetar a interface/UX para limitar os tipos de entradas que o usuário pode enviar ao modelo, assim como os textos ou imagens exibidos ao usuário. Ao implantar a aplicação de IA, também devemos ser transparentes sobre o que nossa aplicação de IA generativa pode e não pode fazer.

Temos uma lição inteira dedicada a [Projetar UX para Aplicações de IA](../12-designing-ux-for-ai-applications/README.md?WT.mc_id=academic-105485-koreyst)

- **Avaliar o modelo**. Trabalhar com LLMs pode ser desafiador porque nem sempre temos controle sobre os dados com os quais o modelo foi treinado. Independentemente disso, devemos sempre avaliar o desempenho e as saídas do modelo. Ainda é importante medir a precisão, similaridade, fundamentação e relevância da saída do modelo. Isso ajuda a fornecer transparência e confiança a stakeholders e usuários.

### Operar uma solução de IA generativa responsável

Construir uma prática operacional em torno de suas aplicações de IA é a etapa final. Isso inclui parceria com outras áreas da nossa startup, como Jurídico e Segurança, para garantir que estejamos em conformidade com todas as políticas regulatórias. Antes do lançamento, também queremos criar planos em torno da entrega, do tratamento de incidentes e do rollback para evitar qualquer dano aos nossos usuários à medida que crescemos.

## Ferramentas

Embora o trabalho de desenvolver soluções de IA responsável possa parecer muito, ele vale a pena. À medida que a área de IA generativa cresce, mais ferramentas para ajudar desenvolvedores a integrar responsabilidade em seus fluxos de trabalho amadurecerão. Por exemplo, o [Azure AI Content Safety](https://learn.microsoft.com/azure/ai-services/content-safety/overview?WT.mc_id=academic-105485-koreyst) pode ajudar a detectar conteúdo e imagens prejudiciais por meio de uma solicitação de API.

## Verificação de conhecimento

Quais são algumas coisas com as quais você precisa se preocupar para garantir o uso responsável da IA?

1. Que a resposta esteja correta.
1. Uso prejudicial, que a IA não seja usada para fins criminais.
1. Garantir que a IA esteja livre de viés e discriminação.

R: 2 e 3 estão corretas. IA responsável ajuda você a considerar como mitigar efeitos prejudiciais, vieses e mais.

## 🚀 Desafio

Leia sobre o [Azure AI Content Safety](https://learn.microsoft.com/azure/ai-services/content-safety/overview?WT.mc_id=academic-105485-koreyst) e veja o que você pode adotar para seu uso.

## Excelente trabalho, continue aprendendo

Após concluir esta lição, confira nossa [coleção de aprendizado de IA generativa](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) para continuar evoluindo seu conhecimento em IA generativa!

Vá para a Lição 4, onde veremos [Fundamentos de Engenharia de Prompt](../04-prompt-engineering-fundamentals/README.md?WT.mc_id=academic-105485-koreyst)!
