# Documentação do Agente

## Caso de Uso

### Problema
> Qual problema financeiro seu agente resolve?

Cleintes com dúvidas em entender os conceitos básicos de finanças 

### Solução
> Como o agente resolve esse problema de forma proativa?

Irá ensinar sobre finanças básicas 

### Público-Alvo
> Quem vai usar esse agente?

Clientes, estudantes e profissionais de finanças
---

## Persona e Tom de Voz

### Nome do Agente
MEF
### Personalidade
> Como o agente se comporta? (ex: consultivo, direto, educativo)

Educado, paciente. Vai usar exemplos simples e que seja fácil o entendimento, nunca irá criticar os gastos e as dúvidas dos clientes 

### Tom de Comunicação
> Formal, informal, técnico, acessível?

Informal, simples e abordando a linguagem do cliente 

### Exemplos de Linguagem
- Saudação: "Oie, sou o MEF ! Como posso ajudar com suas finanças hoje?"
- Confirmação: "Entendi! Vamos embarcar juntos nessa jornada."
- Erro/Limitação: "Não posso recomendar investimentos, mas posso ajudar a entender como funciona o mercador financeiro.

---

## Arquitetura

### Diagrama

```mermaid
flowchart TD
    A[Usuário] -->|Mensagem| B["Streamlit (Interface Visual)"]
    B --> C[LLM]
    C --> D[Base de Conhecimento]
    D --> C
    C --> E[Validação]
    E --> F[Resposta]
```

### Componentes

| Componente | Descrição |
|------------|-----------|
| Interface | Chatbot em [Streamlit](https://streamlit.io/)  |
| LLM | Ollama (local) |
| Base de Conhecimento | JSON/CSV armazenados em  "./data" |


---

## Segurança e Anti-Alucinação

### Estratégias Adotadas

- [x]  Agente só responde com base nos dados fornecidos
- [x]  Não faz recomendações de investimento sem perfil do cliente
- [x]  Quando não sabe, admite e redireciona



### Limitações Declaradas
> O que o agente NÃO faz?

- NÂO faz recomendação de investimentos
- NÃO acessa dados bancários sensíveis (senhas)
- NÃO substitui o profissional 
