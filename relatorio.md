# Definição do Problema

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

# Regras de Classificação
As classes de comunicabilidade são determinadas com base nas seguintes regras:

- **Boa** → `respostas_incorretas ≤ 2` **e** `avaliacao_usuario ≥ 4` **e** `tempo_resposta ≤ 3`
- **Regular** → `respostas_incorretas ≤ 4` **ou** `avaliacao_usuario = 3`
- **Ruim** → `respostas_incorretas > 4` **ou** `avaliacao_usuario ≤ 2`

# Descrição da Base Sintética

A base de dados utilizada neste estudo foi **gerada de forma sintética** com o objetivo de simular interações de usuários e permitir a avaliação de algoritmos de classificação sem depender de dados reais. Ela contém **200 instâncias** e os seguintes atributos:

- **respostas_incorretas**: quantidade de respostas incorretas fornecidas pelo usuário em uma interação. Os valores variam de 0 a 10, representando diferentes níveis de desempenho.
- **tempo_resposta**: tempo médio em segundos que o usuário leva para responder. Os valores variam entre 1 e 30 segundos, simulando respostas rápidas e lentas.
- **avaliacao_usuario**: nota atribuída ao usuário ao final da interação, variando de 1 a 5. Notas altas refletem boa performance e satisfação.
- **mensagens_totais**: total de mensagens enviadas durante a interação, variando entre 1 e 50, simulando interações curtas e longas.
- **repeticoes**: número de mensagens repetidas ou similares dentro da interação, variando de 0 a 5.
- **comunicabilidade** (classe-alvo): classificada como **Boa**, **Regular** ou **Ruim**, definida com base em regras combinando os atributos preditores (por exemplo, alto número de respostas incorretas e tempo de resposta elevado resulta em comunicabilidade Ruim).

### Justificativa do uso da base sintética
- Permite testar algoritmos de classificação sem depender de dados reais, garantindo **privacidade e controle total sobre os cenários simulados**.
- Facilita a geração de situações específicas, como interações com diferentes níveis de erro, tempo de resposta e avaliação, possibilitando analisar o comportamento dos algoritmos em diversas condições.
- Serve como base inicial para futuros experimentos com dados reais, podendo ser refinada ou ajustada conforme necessidade.

# Descrição dos Experimentos no Weka
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

<img width="973" height="682" alt="Captura de tela 2025-11-03 212519" src="https://github.com/user-attachments/assets/8975ec38-38d1-4ef8-9504-26ef7aedffd3" />

---
**Comunicabilidade × Tempo de resposta:**  
As classes **Regular** e **Ruim** apresentam distribuições semelhantes, enquanto a classe **Boa** é menos frequente, indicando que tempos de resposta mais altos prejudicam a comunicação.

<img width="965" height="692" alt="Captura de tela 2025-11-03 212610" src="https://github.com/user-attachments/assets/1835713e-a8a3-4100-9363-e8311182da18" />


---
**Comunicabilidade × Avaliação do usuário:**  
A classe **Boa** apresenta maior concentração de instâncias, indicando que avaliações mais altas estão fortemente associadas a melhor comunicabilidade. A classe **Ruim** é a menos representada.



---
**Mensagens totais × Tempo de resposta:**  
Divergência entre **Regular** e **Ruim**, que se alternam conforme a quantidade de mensagens e tempo de resposta. A classe **Boa** aparece de forma menos influente, sugerindo que conversas longas e lentas estão associadas a problemas de comunicação.



---
**Mensagens totais × Repetições:**  
Não há correlação clara, mas **Regular** e **Ruim** aparecem mais frequentemente, sugerindo que interações repetitivas podem estar relacionadas a comunicabilidade problemáticas. 


---
**Observação geral:**  
Atributos repetidos não foram considerados relevantes para esta análise.

**Síntese:**  
Os atributos **respostas_incorretas**, **tempo_resposta** e **avaliacao_usuario** são os mais relevantes para distinguir os diferentes níveis de comunicabilidade, reforçando as regras definidas na geração da base de dados.

# Resultados Obtidos

Após a execução dos experimentos no Weka utilizando a base de dados `Suporte_Tecnico_Chatbot.arff`, foram testados cinco algoritmos de classificação.  
Os testes seguiram a metodologia de **Hold-Out**, com **66% das instâncias para treino** e **34% para teste**.

Abaixo estão os resultados de acurácia, tempo de execução e observações gerais de desempenho de cada modelo.

| Algoritmo | Acurácia (%) | Tempo de Execução (s) | Observações |
|------------|---------------|------------------------|--------------|
| **J48 (Árvore de Decisão)** | 98.8372% | 0.06 | Gerou regras claras e compreensíveis, semelhantes às definidas manualmente. |
| **Naive Bayes** | 100.0% | 0.00 | Classificou corretamente todas as instâncias, mas houve pequenas confusões entre as classes “Regular” e “Boa”. |
| **IBk (k-NN)** | 100.0% | 0.01 | Mostrou desempenho estável e resultados próximos aos da Árvore de Decisão. |
| **OneR** | 100.0% | 0.01 | É um modelo simples, baseado em um único atributo. |
| **ZeroR** | 27.907% | 0.00 | Serve apenas como baseline (modelo de referência). |

## Matrizes de Confusão
### -J48
<img width="267" height="158" alt="Captura de tela 2025-11-03 211415" src="https://github.com/user-attachments/assets/a16ab812-4018-4b43-906f-0c43a5823b1c" />

---
### -Naive Bayes
<img width="260" height="156" alt="Captura de tela 2025-11-03 211524" src="https://github.com/user-attachments/assets/0e20b428-d823-47e8-a989-7b8fc37094b6" />

---
### -Ibk (k-NN)
<img width="259" height="157" alt="Captura de tela 2025-11-03 211327" src="https://github.com/user-attachments/assets/cf216afc-77a1-4825-85cc-02ae7ede3139" />
  
---
### -OneR
<img width="256" height="150" alt="Captura de tela 2025-11-03 211637" src="https://github.com/user-attachments/assets/89bfaa1c-144e-424b-bf78-00dd67d4dc01" />

---  
### -ZeroR
<img width="260" height="146" alt="Captura de tela 2025-11-03 211831" src="https://github.com/user-attachments/assets/61fb4b59-17ae-4ae4-81e5-55fdbe27ead8" />

---

**Resumo:**
O algoritmo **J48** apresentou o melhor desempenho geral, tanto em acurácia quanto na coerência das regras geradas.  
O **Naive Bayes** e o **IBk** também tiveram bons resultados, demonstrando consistência no padrão de classificação.  
Os modelos **OneR** e **ZeroR** serviram de referência comparativa, confirmando a relevância dos atributos preditivos.

## (Figura X – Comparativo dos algoritmos de classificação no Weka) 
<img width="709" height="607" alt="Captura de tela 2025-10-24 144544" src="https://github.com/user-attachments/assets/5087e497-5daa-48d3-a11e-aa396263efc5" />

---

# Análise Crítica dos Resultados em Relação ao Domínio de IHC
A análise visual e os resultados obtidos evidenciam que erros frequentes, longos tempos de resposta e avaliações baixas estão associados a uma experiência de comunicação ruim, o que é coerente com o domínio de Interação Humano-Computador (IHC).  
A compreensão desses padrões permite criar sistemas mais responsivos e intuitivos, além de fornecer feedbacks relevantes para melhoria da experiência do usuário.

# Conclusão
O estudo demonstrou que é possível aplicar técnicas de **aprendizado de máquina** para avaliar a **comunicabilidade** de um chatbot de suporte técnico.  
Os resultados reforçam que atributos como **tempo de resposta**, **número de erros** e **avaliação do usuário** são determinantes para a percepção de qualidade da interação.  
A análise realizada fornece insights úteis para aprimorar a **experiência do usuário** e a **eficiência comunicacional** de assistentes virtuais.





