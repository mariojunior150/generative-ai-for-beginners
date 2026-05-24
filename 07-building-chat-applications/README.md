# Construindo Aplicativos de Chat com IA Generativa

[![Building Generative AI-Powered Chat Applications](./images/07-lesson-banner.png?WT.mc_id=academic-105485-koreyst)](https://youtu.be/R9V0ZY1BEQo?si=IHuU-fS9YWT8s4sA)

> _(Clique na imagem acima para assistir ao vídeo desta lição)_

Agora que vimos como construir apps de geração de texto, vamos explorar aplicações de chat.

Aplicativos de chat já fazem parte do nosso dia a dia — vão além de conversas casuais e são peças centrais em atendimento ao cliente, suporte técnico e sistemas de aconselhamento. Ao integrar tecnologias avançadas como IA generativa, a complexidade e os desafios também aumentam.

Algumas perguntas importantes são:

- **Construção do app**: Como construir e integrar eficientemente essas aplicações com casos de uso específicos?
- **Monitoramento**: Depois de implantadas, como monitorar e garantir que operem com qualidade e em conformidade com os [seis princípios de IA responsável](https://www.microsoft.com/ai/responsible-ai?WT.mc_id=academic-105485-koreyst)?

Nesta lição investigaremos arquiteturas que suportam esses sistemas, metodologias para customizá-los a tarefas de domínio e métricas/considerações para um uso responsável de IA.

## Introdução

Esta lição cobre:

- Técnicas para construir e integrar aplicações de chat de forma eficiente.
- Como aplicar customização e fine-tuning em aplicações.
- Estratégias e considerações para monitorar aplicações de chat.

## Objetivos de Aprendizagem

Ao final desta lição, você será capaz de:

- Descrever considerações para integrar aplicações de chat a sistemas existentes.
- Customizar aplicações de chat para casos de uso específicos.
- Identificar métricas e considerações para monitorar e manter a qualidade de aplicações com IA.
- Garantir que aplicações de chat façam uso responsável da IA.

## Integrando IA Generativa em Aplicativos de Chat

Elevar um aplicativo de chat com IA generativa envolve mais do que torná-lo “mais inteligente”: trata-se de otimizar arquitetura, desempenho e interface para oferecer uma boa experiência ao usuário. Isso inclui fundamentos arquiteturais, integrações de API e considerações de interface. Esta seção oferece um roteiro para navegar por essas decisões, seja para integrar em sistemas existentes ou construir plataformas independentes.

Ao final desta seção, você terá conhecimentos necessários para construir e incorporar aplicações de chat de forma eficiente.

### Chatbot ou aplicação de chat?

Antes de começar a construir, comparemos “chatbots” com “aplicações de chat com IA” — eles têm papéis e funcionalidades diferentes. Um chatbot costuma automatizar tarefas específicas (responder perguntas frequentes, rastrear envios), normalmente com lógica baseada em regras ou modelos especializados. Em contraste, uma aplicação de chat com IA generativa é um ambiente mais amplo, capaz de suportar texto, voz e vídeo, e que integra um modelo generativo para produzir respostas mais humanas e contextualizadas. Uma aplicação com IA generativa pode dialogar em domínio aberto, adaptar-se ao contexto e gerar respostas criativas ou complexas.

| Chatbot                               | Aplicação de Chat com IA Generativa     |
| ------------------------------------- | -------------------------------------- |
| Focada em tarefas e baseada em regras | Consciente de contexto                  |
| Frequentemente parte de sistemas maiores| Pode hospedar um ou vários chatbots     |
| Limitada a funções programadas         | Incorpora modelos generativos           |
| Interações especializadas e estruturadas | Capaz de diálogos em domínio aberto   |

### Aproveitando SDKs e APIs prontas

Ao construir um app de chat, avalie primeiro o que já existe. Usar SDKs e APIs bem documentados é vantajoso:

- **Acelera o desenvolvimento e reduz esforço**: permite focar em diferenciais do negócio em vez de reinventar funcionalidades.
- **Melhor desempenho e escalabilidade**: SDKs maduros costumam tratar escala e resiliência.
- **Manutenção simplificada**: atualizações são feitas via atualização da dependência.
- **Acesso a tecnologias avançadas**: modelos ajustados e treinados em grandes conjuntos de dados.

Normalmente, o acesso a essas funcionalidades exige uma chave/credencial. Usaremos a OpenAI Python Library para exemplos; veja também os notebooks da lição: [notebook OpenAI](./python/oai-assignment.ipynb?WT.mc_id=academic-105485-koreyst) e [notebook Azure OpenAI](./python/aoai-assignment.ipynb?WT.mc_id=academic-105485-koreys).

```python
import os
from openai import OpenAI

API_KEY = os.getenv("OPENAI_API_KEY","")

client = OpenAI(
    api_key=API_KEY
    )

chat_completion = client.chat.completions.create(model="gpt-3.5-turbo", messages=[{"role": "user", "content": "Suggest two titles for an instructional lesson on chat applications for generative AI."}])
```

O exemplo acima usa `gpt-3.5-turbo` e pressupõe que a chave esteja definida — sem ela, ocorrerá um erro.

## Experiência do Usuário (UX)

Princípios gerais de UX se aplicam, mas há considerações específicas quando ML está envolvido:

- **Mecanismo para lidar com ambiguidade**: permita que usuários peçam esclarecimentos quando as respostas forem ambíguas.
- **Retenção de contexto**: modelos avançados lembram o contexto da conversa; dê ao usuário controle sobre isso e defina políticas de retenção para evitar vazamento de dados sensíveis.
- **Personalização**: perfis de usuário (ex.: “instruções personalizadas”) ajudam a adaptar respostas ao contexto do usuário.

Um exemplo de personalização é a funcionalidade “Custom instructions” do ChatGPT, que permite fornecer informações sobre o usuário para contextualizar respostas.

![Custom Instructions Settings in ChatGPT](./images/custom-instructions.png?WT.mc_id=academic-105485-koreyst)

![A prompt in ChatGPT for a lesson plan about linked lists](./images/lesson-plan-prompt.png?WT.mc_id=academic-105485-koreyst)

### Microsoft: System Message Framework para LLMs

[A Microsoft providencia orientações](https://learn.microsoft.com/azure/ai-services/openai/concepts/system-message#define-the-models-output-format?WT.mc_id=academic-105485-koreyst) para escrever mensagens de sistema eficazes, cobrindo:

1. Definir quem é o modelo e suas capacidades/limitações.
2. Definir o formato de saída esperado.
3. Fornecer exemplos que demonstrem o comportamento desejado.
4. Incluir guardrails comportamentais adicionais.

### Acessibilidade

Projete para usuários com diferentes necessidades (visual, auditiva, motora, cognitiva):

- **Visual**: temas de alto contraste, texto redimensionável, compatibilidade com leitores de tela.
- **Auditiva**: funções de texto-para-fala e fala-para-texto, indicações visuais para notificações.
- **Motora**: suporte a navegação por teclado, comandos de voz.
- **Cognitiva**: opções de linguagem simplificada.

## Customização e Fine-tuning para Modelos de Linguagem de Domínio

Imagine um chat que entende a terminologia da sua empresa e antecipa dúvidas comuns. Algumas abordagens:

- **Modelos de linguagem de domínio (DSL)**: treinar ou usar modelos especializados no domínio.
- **Fine-tuning**: adaptar um modelo pré-treinado com dados específicos.

## Customização: Usando um DSL

Modelos DSL fornecem interações mais contextuais e relevantes para um setor/assunto. Você pode treinar um modelo do zero, usar um existente via SDKs, ou aplicar fine-tuning para adaptar um modelo pré-treinado ao seu domínio.

## Customização: Aplicar fine-tuning

Use fine-tuning quando o modelo geral não for suficiente para tarefas especializadas. Casos complexos, como consultas médicas, exigem contexto extenso e informações atualizadas — um modelo geral pode não ser confiável sem adaptação.

### Exemplo: aplicação médica

Para um app que apoia profissionais de saúde (diretrizes, interações medicamentosas, pesquisas recentes), um modelo geral pode responder perguntas simples, mas falhar em casos altamente específicos. Fine-tuning com um dataset médico relevante pode melhorar precisão e confiabilidade — requerendo, entretanto, dados amplos e de qualidade.

## Considerações para uma Experiência de Chat de Alta Qualidade

Critérios para “alta qualidade” incluem métricas acionáveis e adesão a um quadro de uso responsável da IA.

### Métricas-chave

Para manter a qualidade, monitore métricas que avaliem tanto a aplicação quanto o modelo e a experiência do usuário:

| Métrica                        | Definição                                                                                                             | Considerações para o desenvolvedor de chat                                         |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| **Uptime**                    | Tempo em que a aplicação está operacional e acessível.                                                                 | Como minimizar downtime?                                           |
| **Tempo de Resposta**         | Tempo necessário para a aplicação responder a uma consulta.                                                            | Como otimizar o processamento para reduzir latência?           |
| **Precisão (Precision)**      | Razão entre predições verdadeiras positivas e o total de predições positivas.                                          | Como validar a precisão do modelo?                                |
| **Recall (Sensibilidade)**    | Razão entre verdadeiras positivas e o número real de positivos.                                                       | Como medir e melhorar recall?                                      |
| **F1 Score**                  | Média harmônica entre precision e recall, equilibrando ambos.                                                          | Qual o alvo para o F1? Como balancear precision e recall?         |
| **Perplexity**                | Mede o quão bem a distribuição prevista pelo modelo alinha-se com a distribuição real dos dados.                       | Como minimizar perplexity?                                         |
| **Métricas de Satisfação**    | Percepção do usuário sobre a aplicação (ex.: surveys).                                                                 | Com que frequência coletar feedback?                              |
| **Taxa de Erro**              | Frequência de falhas na compreensão ou na saída do modelo.                                                              | Quais estratégias para reduzir erros?                             |
| **Ciclos de Retraining**      | Frequência com que o modelo é atualizado com novos dados.                                                              | Quando acionar um ciclo de retraining?                             |
| **Detecção de Anomalias**     | Técnicas para identificar padrões incomuns no comportamento do sistema.                                                | Como responder a anomalias?                                         |

### Implementando Práticas de IA Responsável em Aplicações de Chat

Os seis princípios da Microsoft devem orientar o desenvolvimento e uso de IA. A tabela abaixo resume definições, considerações e motivos pelos quais cada princípio importa.

| Princípios             | Definição Microsoft                                | Considerações para o desenvolvedor                                      | Por que é importante                                                                     |
| ---------------------- | ------------------------------------------------- | ---------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| Fairness (Equidade)    | Sistemas de IA devem tratar as pessoas de forma justa.            | Assegure que a aplicação não discrimine com base em dados do usuário.  | Gera confiança e evita implicações legais.                |
| Reliability and Safety | Sistemas de IA devem operar de forma confiável e segura.        | Implemente testes e mecanismos de fallback para minimizar riscos.         | Garante satisfação do usuário e previne danos.                                 |
| Privacy and Security   | Sistemas de IA devem proteger a privacidade e ser seguros.      | Use criptografia e medidas de proteção de dados.              | Protege dados sensíveis e ajuda a cumprir leis de privacidade.                         |
| Inclusiveness          | Sistemas de IA devem empoderar e engajar pessoas diversas. | Projete UI/UX acessível e inclusivo. | Permite que mais pessoas usem a aplicação efetivamente.                   |
| Transparency           | Sistemas de IA devem ser compreensíveis.                  | Forneça documentação e explicações sobre decisões da IA.            | Usuários confiam mais quando entendem como decisões são tomadas.            |
| Accountability         | Pessoas devem ser responsáveis pelos sistemas de IA.          | Estabeleça processos de auditoria e melhoria contínua.     | Permite correções e melhorias constantes em caso de erros.               |

## Assignment

Veja os exercícios em [python](./python?WT.mc_id=academic-105485-koreyst). Eles guiarão desde os primeiros prompts de chat até classificação e sumarização de textos. Os exercícios estão disponíveis em várias linguagens.

## Excelente trabalho — continue a jornada

Após concluir esta lição, visite a [coleção de aprendizado de Generative AI](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) para aprofundar seus conhecimentos.

Siga para a Lição 8 e aprenda a construir aplicações de busca: [08-building-search-applications/README.md](../08-building-search-applications/README.md?WT.mc_id=academic-105485-koreyst)
