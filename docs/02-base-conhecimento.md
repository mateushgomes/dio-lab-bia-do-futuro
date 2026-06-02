# Base de Conhecimento

## Dados Utilizados

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores |
| `perfil_investidor.json` | JSON | Personalizar recomendações |
| `produtos_financeiros.json` | JSON | Sugerir produtos adequados ao perfil |
| `transacoes.csv` | CSV | Analisar padrão do cliente |

> [!TIP]
> **Quer um dataset mais robusto?** Você pode utilizar datasets públicos do [Hugging Face](https://huggingface.co/datasets) relacionados a finanças, desde que sejam adequados ao contexto do desafio.

---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

Sim, realizei alterações nos dados da pasta `data`(historico, perfil,produtos, transacoes) para que possa estar no padrão do meu assistente de emprestimos, contendo novos tipos de dados.

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

Existem duas possibilidades, injetar manualmente (ctrl + c, ctrl + v) ou importado através do código abaixo.

```python
import pandas as pd
import json 

# CSV
historico = pd.read_csv('data/historico_atendimento.csv')
transacoes = pd.read_csv('data/transacoes.csv')

# JSON
with open('data/perfil_investidor.json', 'r', encoding='utf-8') as f:
    perfil = json.load(f)

with open('data/produtos_financeiros.json', 'r', encoding='utf-8') as f:
    produtos = json.load(f)

```

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

Os dados são inseridos dinamicamente no contexto do prompt, permitindo que o assistente personalize suas respostas de acordo com o perfil financeiro e histórico do cliente.

O agente utiliza:

Perfil do cliente para identificar elegibilidade e capacidade financeira;
Transações financeiras para analisar renda, despesas e comprometimento financeiro;
Histórico de atendimento para fornecer continuidade ao relacionamento e evitar perguntas repetidas;
Base de empréstimos para recomendar modalidades compatíveis com o perfil do usuário.

As informações são utilizadas como contexto para geração das respostas, sem alterar o comportamento principal definido no System Prompt.

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
Perfil do Cliente:

Nome: João Silva
Idade: 62 anos
Tipo de Cliente: Aposentado INSS
Benefício Mensal: R$ 3.500,00
Margem Consignável Disponível: R$ 900,00

Resumo Financeiro:

Receitas Mensais: R$ 3.500,00
Despesas Mensais: R$ 2.600,00
Saldo Mensal: R$ 900,00

Histórico de Atendimento:

Consulta sobre simulação de empréstimo consignado
Solicitação de informações sobre refinanciamento
Interesse em portabilidade de crédito

Produtos Disponíveis:

Consignado INSS
Taxa média: 1,66% a.m.
Prazo máximo: 84 meses
Consignado Servidor Público
Taxa média: 1,80% a.m.
Prazo máximo: 96 meses

Objetivo do Assistente:

Orientar o cliente sobre crédito consignado, realizar simulações, explicar conceitos financeiros, avaliar comprometimento de renda e sugerir alternativas compatíveis com seu perfil financeiro. 
```
