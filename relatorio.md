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

# ETAPA 2 — Regras de Classificação
As classes de comunicabilidade são determinadas com base nas seguintes regras:

- **Boa** → `respostas_incorretas ≤ 2` **e** `avaliacao_usuario ≥ 4` **e** `tempo_resposta ≤ 3`
- **Regular** → `respostas_incorretas ≤ 4` **ou** `avaliacao_usuario = 3`
- **Ruim** → `respostas_incorretas > 4` **ou** `avaliacao_usuario ≤ 2`

# ETAPA 4 — Descrição dos Experimentos no Weka
Foi utilizada a aba **Visualize** do Weka para explorar visualmente as relações entre os atributos e a classe-alvo. Os principais cruzamentos analisados foram:
- Comunicabilidade × Respostas incorretas
- Comunicabilidade × Tempo de resposta
- Comunicabilidade × Avaliação do usuário
- Mensagens totais × Tempo de resposta
- Mensagens totais × Repetições

### Observações
Durante a análise visual, os seguintes padrões foram identificados:

**Comunicabilidade × Respostas incorretas:**  
Conforme o número de respostas incorretas aumenta, há um crescimento expressivo das instâncias classificadas como **Ruim**, mostrando forte relação entre a quantidade de erros e a baixa comunicabilidade.

**Comunicabilidade × Tempo de resposta:**  
As classes **Regular** e **Ruim** apresentam distribuições semelhantes, enquanto a classe **Boa** é menos frequente, indicando que tempos de resposta mais altos prejudicam a comunicação.

**Comunicabilidade × Avaliação do usuário:**  
A classe **Boa** apresenta maior concentração de instâncias, indicando que avaliações mais altas estão fortemente associadas a melhor comunicabilidade. A classe **Ruim** é a menos representada.

**Mensagens totais × Tempo de resposta:**  
Divergência entre **Regular** e **Ruim**, que se alternam conforme a quantidade de mensagens e tempo de resposta. A classe **Boa** aparece de forma menos influente, sugerindo que conversas longas e lentas estão associadas a problemas de comunicação.

**Mensagens totais × Repetições:**  
Não há correlação clara, mas **Regular** e **Ruim** aparecem mais frequentemente, sugerindo que interações repetitivas podem estar relacionadas a comunicabilidade problemáticas.

**Observação geral:**  
Atributos repetidos não foram considerados relevantes para esta análise.

**Síntese:**  
Os atributos **respostas_incorretas**, **tempo_resposta** e **avaliacao_usuario** são os mais relevantes para distinguir os diferentes níveis de comunicabilidade, reforçando as regras definidas na geração da base de dados.

# Etapa 5 — Resultados Obtidos

Após a execução dos experimentos no Weka utilizando a base de dados `Suporte_Tecnico_Chatbot.arff`, foram testados cinco algoritmos de classificação.  
Os testes seguiram a metodologia de **Hold-Out**, com **66% das instâncias para treino** e **34% para teste**.

Abaixo estão os resultados de acurácia, tempo de execução e observações gerais de desempenho de cada modelo.

| Algoritmo | Acurácia (%) | Tempo de Execução (s) | Observações |
|------------|---------------|------------------------|--------------|
| **J48 (Árvore de Decisão)** | 98.8372 | 0.06 | Gerou regras semelhantes às definidas manualmente; boa separação entre as classes. |
| **Naive Bayes** | 100.0 | 0.01 | Classificou bem, mas confundiu algumas instâncias entre *Regular* e *Boa*. |
| **IBk (k-NN)** | 100.0 | 0.01 | Desempenho estável; resultados próximos ao J48. |
| **OneR** | 100.0 | 0.01 | Modelo simples baseado em um único atributo; menor precisão. |
| **ZeroR** | 27.9 | 0.01 | Usado como baseline; sempre escolhe a classe mais frequente. |

**Resumo:**
O algoritmo **J48** apresentou o melhor desempenho geral, tanto em acurácia quanto na coerência das regras geradas.  
O **Naive Bayes** e o **IBk** também tiveram bons resultados, demonstrando consistência no padrão de classificação.  
Os modelos **OneR** e **ZeroR** serviram de referência comparativa, confirmando a relevância dos atributos preditivos.

## (Figura X – Comparativo dos algoritmos de classificação no Weka) 
<img width="709" height="607" alt="Captura de tela 2025-10-24 144544" src="https://github.com/user-attachments/assets/5087e497-5daa-48d3-a11e-aa396263efc5" />

---

# ETAPA 6 — Análise Crítica dos Resultados em Relação ao Domínio de IHC
A análise visual e os resultados obtidos evidenciam que erros frequentes, longos tempos de resposta e avaliações baixas estão associados a uma experiência de comunicação ruim, o que é coerente com o domínio de Interação Humano-Computador (IHC).  
A compreensão desses padrões permite criar sistemas mais responsivos e intuitivos, além de fornecer feedbacks relevantes para melhoria da experiência do usuário.





