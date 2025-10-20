# ETAPA 1 — Definição do Problema

## Contexto
O problema a ser resolvido envolve a **avaliação da comunicabilidade** de um **chatbot de suporte técnico**.  
O objetivo é classificar o desempenho do chatbot com base em métricas que refletem sua eficiência e clareza na comunicação com o usuário.

## Atributos Utilizados
- **respostas_incorretas**: número de respostas incorretas fornecidas pelo chatbot.  
- **tempo_resposta**: tempo médio (em segundos) que o chatbot leva para responder.  
- **repeticoes**: número de vezes que o chatbot repete informações.  
- **avaliacao_usuario**: nota atribuída pelo usuário após o atendimento (escala de 1 a 5).  
- **mensagens_totais**: total de mensagens trocadas entre o usuário e o chatbot.

## Classe-Alvo
- **comunicabilidade**: indica a qualidade da comunicação do chatbot, podendo assumir os valores:
  - **Boa**
  - **Regular**
  - **Ruim**

## Regras de Classificação
As classes de comunicabilidade são determinadas com base nas seguintes regras:

- **Boa** → `respostas_incorretas ≤ 2` **e** `avaliacao_usuario ≥ 4` **e** `tempo_resposta ≤ 3`
- **Regular** → `respostas_incorretas ≤ 4` **ou** `avaliacao_usuario = 3`
- **Ruim** → `respostas_incorretas > 4` **ou** `avaliacao_usuario ≤ 2`

---


