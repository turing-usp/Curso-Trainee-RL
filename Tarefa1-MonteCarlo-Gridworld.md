# Tarefa 1 — Monte Carlo Gridworld

*Tempo estimado de conclusão: 1 semana*

## 1. Visão geral

Nesta tarefa você vai implementar um agente **Monte Carlo** para resolver um ambiente *gridworld*. O agente deve aprender a sair do ponto A (canto superior esquerdo) e chegar ao ponto B (canto inferior direito) utilizando apenas as ações *cima*, *baixo*, *esquerda* e *direita*. **Não** use IA generativa para escrever o código — compreender o algoritmo faz parte do exercício.

## 2. Conteúdo preparatório

### 2.1 Leitura
- [Conceitos de RL – Introdução](https://github.com/turing-usp/Aprendizado-por-Reforco/tree/main/Introdu%C3%A7%C3%A3o)
- [Resumo de Monte Carlo](https://github.com/turing-usp/Aprendizado-por-Reforco/tree/main/Aprendizado%20por%20Refor%C3%A7o%20Cl%C3%A1ssico/Monte%20Carlo)

### 2.2 Vídeos
- [Reinforcement Learning, by the Book](https://www.youtube.com/watch?v=NFo9v_yKQXA)
- [Bellman Equations, Dynamic Programming, GPI — Parte 2](https://www.youtube.com/watch?v=_j6pvGEchWU&t=726s)
- [Monte Carlo & Off-Policy Methods — Parte 3](https://www.youtube.com/watch?v=bpUszPiWM7o)

### 2.3 Livro
Capítulo 5 do clássico *Reinforcement Learning: An Introduction* aprofunda o método de Monte Carlo.

## 2.4 Cursos (opcionais, só se quiser aprofundar ou estiver com muita dificuldade mesmo)
Esses cursos são gratuitos, vc tem que entrar como ouvinte, se tiver dificuldade de acessar manda mensagem pra algum dos lideres
- [Fundamentos do Aprendizado por Reforço](https://www.coursera.org/learn/fundamentals-of-reinforcement-learning?specialization=reinforcement-learning)
- [Métodos de Aprendizado Baseados em Amostras](https://www.coursera.org/learn/sample-based-learning-methods?specialization=reinforcement-learning)
- [Especialização completa (4 cursos)](https://www.coursera.org/specializations/reinforcement-learning) — apenas os dois acima são relevantes aqui.

## 3. O problema (Gridworld)

<img width="891" height="267" alt="image" src="https://github.com/user-attachments/assets/efc7fa7f-7442-4dfb-9985-77b0cc9be751" />

Seu ambiente é um tabuleiro com recompensas negativas pequenas (-0.05) em todas as células, exceto na meta (B) que concede +1.0 e termina o episódio. O agente começa em A e deve aprender a política ótima usando Monte Carlo.
Esse é um dos métodos de monte carlo possiveis, existem outros exemplos do pseudocódigo deles no livro, sinta-se livre pra implementar esse ou algum dos outros(os outros sao mais legais).

<img width="852" height="406" alt="image" src="https://github.com/user-attachments/assets/6e1361f1-2d9f-4881-8d7e-a237241887f1" />

## 4. Entregáveis
1. **Notebook Jupyter** contendo (nao use gpt nessa parte de preferencia):
   - Implementação do ambiente gridworld.
   - Algoritmo Monte Carlo (inclua comentários explicativos).
   - Impressão das matrizes de recompensas, valores e política final (veja exemplo abaixo).
   - (Opcional)Visualização usando matplotlib.
2. **Apresentação (PowerPoint ou similares)** resumindo:
   - Histórico do método de Monte Carlo.
   - Ideia central do algoritmo e do ambiente (método de primeira visita, retorno, média incremental, etc.).

## 5. Exemplo de saída esperada
```text
rewards
[[-0.05 -0.05 -0.05 -0.05 -0.05]
 [-0.05 -0.05 -0.05 -0.05 -0.05]
 [-0.05 -0.05 -0.05 -0.05 -0.05]
 [-0.05 -0.05 -0.05 -0.05 -0.05]
 [-0.05 -0.05 -0.05 -0.05  1.00]]
-------------
valores
[[3.93 4.43 4.99 5.61 6.30]
 [4.43 4.99 5.61 6.30 7.07]
 [4.99 5.61 6.30 7.07 7.91]
 [5.61 6.30 7.07 7.56 8.86]
 [6.30 7.07 7.91 8.86 9.91]]
-------------
política
['right', 'right', 'right', 'right', 'down']
['down',  'right', 'right', 'right', 'down']
['right', 'right', 'right', 'right', 'down']
['right', 'right', 'down',  'right', 'down']
['right', 'right', 'right', 'right', 'right']
```

