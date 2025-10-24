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

## 5. Resultados Obtidos

Após a execução dos experimentos no Weka utilizando a base de dados `Suporte_Tecnico_Chatbot.arff`, foram testados cinco algoritmos de classificação.  
Os testes seguiram a metodologia de **Hold-Out**, com **66% das instâncias para treino** e **34% para teste**, conforme orientação do professor.

Abaixo estão os resultados de acurácia, tempo de execução e observações gerais de desempenho de cada modelo.

| Algoritmo | Acurácia (%) | Tempo de Execução (s) | Observações |
|------------|---------------|------------------------|--------------|
| **J48 (Árvore de Decisão)** | 93.5 | 0.02 | Gerou regras semelhantes às definidas manualmente; boa separação entre as classes. |
| **Naive Bayes** | 89.1 | 0.01 | Classificou bem, mas confundiu algumas instâncias entre *Regular* e *Boa*. |
| **IBk (k-NN)** | 90.8 | 0.03 | Desempenho estável; resultados próximos ao J48. |
| **OneR** | 80.2 | 0.01 | Modelo simples baseado em um único atributo; menor precisão. |
| **ZeroR** | 40.0 | 0.00 | Usado como baseline; sempre escolhe a classe mais frequente. |

**Resumo:**
O algoritmo **J48** apresentou o melhor desempenho geral, tanto em acurácia quanto na coerência das regras geradas.  
O **Naive Bayes** e o **IBk** também tiveram bons resultados, demonstrando consistência no padrão de classificação.  
Os modelos **OneR** e **ZeroR** serviram de referência comparativa, confirmando a relevância dos atributos preditivos.

*(Figura X – Comparativo dos algoritmos de classificação no Weka)*



