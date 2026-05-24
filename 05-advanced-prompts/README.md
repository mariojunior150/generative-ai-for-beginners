# Prompts Avançados

[![Creating Advanced Prompts](./images/05-lesson-banner.png?WT.mc_id=academic-105485-koreyst)](https://youtu.be/BAjzkaCdRok?si=NmUIyRf7-cDgbjtt)

Vamos recapitular alguns aprendizados do capítulo anterior:

> Engenharia de prompts é o processo de **guiar o modelo para respostas mais relevantes** fornecendo instruções e contexto adequados.

Ao criar prompts existem duas etapas principais: **construção** (fornecer o contexto certo) e **otimização** (ajustar o prompt para melhorar resultados).

Neste capítulo vamos aprofundar: você deixará de apenas experimentar prompts para entender por que um prompt funciona melhor que outro e aprenderá técnicas aplicáveis a qualquer LLM.

## Introdução

Nesta lição você vai:

- Aprofundar técnicas de engenharia de prompt aplicadas a diferentes cenários.
- Configurar prompts para controlar a variação da saída.

## Objetivos de aprendizagem

Ao final desta lição você deverá ser capaz de:

- Aplicar técnicas de prompt que melhorem a qualidade das respostas.
- Fazer prompts que resultem em saídas determinísticas ou variáveis, conforme a necessidade.

## Engenharia de prompt

Engenharia de prompt é o conjunto de técnicas para criar entradas que produzam o resultado desejado. Não é uma disciplina de engenharia formal, mas um repertório prático de padrões e estratégias.

### Exemplo simples

Considere o prompt:

> Gere 10 perguntas sobre geografia.

Esse prompt já contém técnicas fundamentais:

- **Contexto**: o tema é geografia.
- **Limite de saída**: solicita 10 itens.

### Limitações de um prompt simples

Mesmo um prompt direto pode não devolver o que você espera:

- **Escopo amplo**: geografia pode abranger países, capitais, rios, mapas, etc.
- **Formato**: o usuário pode querer um formato específico (JSON, bullets, questões com alternativas, etc.).

Por isso precisamos de técnicas adicionais para direcionar o modelo.

### Técnicas de prompting

Prompting é uma propriedade emergente dos LLMs — aprendemos o que funciona testando. Técnicas comuns:

- **Zero-shot**: enviar uma instrução única sem exemplos.
- **Few-shot**: fornecer alguns exemplos para definir formato e estilo.
- **Chain-of-thought**: guiar o modelo por passos de raciocínio.
- **Generated knowledge**: injetar fatos ou dados externos no prompt.
- **Least-to-most**: decompor um problema em subproblemas ordenados.
- **Self-refine**: pedir ao modelo para criticar e melhorar sua resposta.
- **Maieutic prompting**: solicitar explicações detalhadas para validar consistência.

### Zero-shot

Simples e direto. Ex.:

- Prompt: "O que é Álgebra?"
- Resposta esperada: definição concisa de Álgebra.

### Few-shot

Inclui exemplos para mostrar o formato desejado. Ex.: pedir um soneto no estilo de Shakespeare e fornecer trechos como referência.

### Chain-of-thought

Ensina o modelo a seguir um processo passo a passo. Em problemas de raciocínio, apresentar um exemplo resolvido antes do problema real normalmente melhora a resposta.

### Generated knowledge

Combine dados da sua organização com a instrução para obter respostas alinhadas ao seu domínio. Use templates com variáveis (`{{variable}}`) que são preenchidas por dados reais.

Exemplo (template preenchido):

```text
Insurance company: ACME Insurance
Insurance products (cost per month):
- Car, cheap, 500 USD
- Car, expensive, 1100 USD
- Home, cheap, 600 USD
- Home, expensive, 1200 USD
- Life, cheap, 100 USD

Please suggest an insurance given the following budget and requirements:
Budget: $1000
Requirements: Car, Home, and Life insurance
```

Se o modelo sugerir itens fora do orçamento, refinar o template (por exemplo, incluir `type` e `cost` e usar a palavra `restrict`) melhora o resultado.

### Least-to-most

Divida um problema complexo em etapas ordenadas e peça ao LLM para resolver cada etapa sequencialmente (útil em análise de dados, debugging, etc.).

### Self-refine (autocrítica)

Peça ao LLM para revisar e melhorar sua própria saída: solicite a solução inicial, critique-a e peça uma nova versão considerando a crítica.

Exemplo: peça um esboço de API em Flask, solicite 3 melhorias e aplique as sugestões retornadas.

### Maieutic prompting

Peça ao modelo que explique cada parte da resposta em detalhe — isso ajuda a detectar contradições e a aumentar a confiabilidade.

## Variabilidade das respostas

LLMs são inerentemente não determinísticos: executar o mesmo prompt várias vezes pode devolver respostas diferentes. Se você precisar de previsibilidade, ajuste parâmetros como `temperature` (0 = mais determinístico, 1 = mais variado). O padrão costuma ser 0.7.

Com `temperature` baixa (ex.: 0.1) as respostas tendem a ser similares; com `temperature` alta (ex.: 0.9) as variações aumentam significativamente.

Observação: outros parâmetros como `top-k`, `top-p`, penalidades de repetição e limite de comprimento também influenciam a saída, mas ficam fora do escopo desta lição.

## Boas práticas

- **Defina o contexto**: quanto mais específico o domínio e as restrições, melhor o resultado.
- **Limite a saída**: especifique contagem, formato e tamanho quando necessário.
- **Descreva o quê e o como**: informe conteúdo esperado e formato (ex.: "Gere uma API Python com rotas products e customers, dividida em 3 arquivos").
- **Use templates**: padronize prompts que usam dados reais.
- **Seja claro e com boa ortografia**: formulários claros geram respostas melhores.

## Exercício

Exemplo de API simples em Flask para usar como ponto de partida:

```python
from flask import Flask, request

app = Flask(__name__)

@app.route('/')
def hello():
    name = request.args.get('name', 'World')
    return f'Hello, {name}!'

if __name__ == '__main__':
    app.run()
```

Use um assistente de IA (por exemplo, GitHub Copilot ou ChatGPT) e aplique a técnica de `self-refine` para iterativamente melhorar esse código.

## Solução

Adicione prompts claros ao código para pedir melhorias específicas (arquitetura, segurança, performance, testes), limitando o número de sugestões desejadas.

[Solution](./python/aoai-solution.py?WT.mc_id=academic-105485-koreyst)

## Verificação de conhecimento

Por que usar chain-of-thought prompting? Mostre 1 resposta correta e 2 incorretas.

1. Para ensinar o LLM a resolver um problema.
1. B, Para ensinar o LLM a encontrar erros em código.
1. C, Para instruir o LLM a propor soluções diferentes.

Resposta: 1 — chain-of-thought mostra ao LLM como resolver um problema por meio de passos e exemplos similares.

## 🚀 Desafio

Use `self-refine` num programa que você escreveu: identifique melhorias, peça ao LLM que as aplique e compare os resultados.

## Excelente trabalho — continue aprendendo

Explore a [coleção de aprendizado sobre Generative AI](https://aka.ms/genai-collection?WT.mc_id=academic-105485-koreyst) para aprofundar seus conhecimentos.

Vá para a Lição 6, onde aplicaremos engenharia de prompt para construir [aplicativos de geração de texto](../06-text-generation-apps/README.md?WT.mc_id=academic-105485-koreyst).
