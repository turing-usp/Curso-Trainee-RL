# Tarefa 2 – SARSA, Q‑Learning e Exercício Racetrack
##Tempo estimado- 1 semana
## 1. Aprendizado por Diferença Temporal (Temporal‑Difference, **TD**)

Os métodos **TD** combinam ideias dos métodos de *Programação Dinâmica* (DP) e *Monte Carlo* (MC):

* **Amostragem** do ambiente como em MC – não precisam de modelo.
* **Atualização on‑line**: os valores são corrigidos a cada passo $t$, antes do fim do episódio.
* **Bootstrapping** como em DP – atualizam estimativas usando outras estimativas.
<br> (Em Aprendizado por Reforço, bootstrapping é o processo de atualizar uma estimativa com base em outra estimativa já disponível. Em vez de esperar todo o retorno ao final do episódio (estratégia Monte Carlo), um método com bootstrapping faz correções imediatas usando previsões posteriores, que ainda estão sujeitas a erro.)


A atualização genérica de TD para a função de valor‑estado $V$ é

$$
V(S_t) \leftarrow V(S_t) + \alpha\,\underbrace{[R_{t+1} + \gamma V(S_{t+1}) - V(S_t)]}_{\text{TD‑error } \delta_t}
$$

O termo entre colchetes é o **TD‑erro** (diferença temporal). Quando o TD‑erro converge para 0, as estimativas tornam‑se consistentes com a política avaliada.

---

## 2. **SARSA**  (State–Action–Reward–State–Action)

* **On‑policy**: aprende a própria política que executa (tipicamente ε‑greedy).
* Atualiza a função valor‑ação $Q$ usando a ação realmente seguida no próximo estado.

$$
Q(S_t,A_t) \leftarrow Q(S_t,A_t) + \alpha\,[R_{t+1} + \gamma\,Q(S_{t+1},A_{t+1}) - Q(S_t,A_t)]
$$

<img width="917" height="425" alt="image" src="https://github.com/user-attachments/assets/8cff2254-ff4a-4d3d-9894-40171eccdba5" />


**Características**

* Exploração e aprendizado alinhados (mesma política).
* Mais conservador que Q‑Learning em ambientes estocásticos.(estocástico é só uma palavra bonita para dizer que é aleatório)

---

## 3. **Q‑Learning**

* **Off‑policy**: aprende a política ótima (greedy) enquanto pode seguir outra política de comportamento (ex.: ε‑greedy).
* Usa a melhor ação **estimada** no próximo estado para a atualização.

$$
Q(S_t,A_t) \leftarrow Q(S_t,A_t) + \alpha\,[R_{t+1} + \gamma\,\max_{a}Q(S_{t+1},a) - Q(S_t,A_t)]
$$

Placeholder do pseudocódigo:

<img width="914" height="398" alt="image" src="https://github.com/user-attachments/assets/ae974f87-a4f5-4bf9-9c53-ba86045c414c" />


**Características**

* Converge para a política ótima sob condições suaves, mesmo com política de comportamento exploratória.
* Geralmente aprende mais rápido que SARSA, porém pode ser mais agressivo e arriscado antes da convergência.

---

*Os dois métodos são bem parecidos na parte do pseudocódigo e formula, a mudança é q ele pega o max do Q ao invés do Q, por isso que é para implementar os dois métodos.

## 4. Conteúdo preparatório
### 4.1 Leitura
* [Resumo de TD](https://github.com/turing-usp/Aprendizado-por-Reforco/tree/main/Aprendizado%20por%20Refor%C3%A7o%20Cl%C3%A1ssico/Temporal-Difference)
### 4.2 Vídeos
* [Temporal Difference Learning](https://www.youtube.com/watch?v=AJiG3ykOxmY)
### 4.3 Livro
* Capítulo 6 do clássico Reinforcement Learning: An Introduction aprofunda os métodos de TD.

# 4.4 Cursos (opcionais, só se quiser aprofundar ou estiver com muita dificuldade mesmo)
Esses cursos são gratuitos, vc tem que entrar como ouvinte, se tiver dificuldade de acessar manda mensagem pra algum dos lideres

* [Métodos de Aprendizado Baseados em Amostras]([url](https://www.coursera.org/learn/sample-based-learning-methods/home/module/4))

## 5. Exercício 5.12 do livro – **Racetrack** (R. Sutton & A. Barto, 2ª ed.)

> *Objetivo*: controlar um carro de corrida em uma curva de pista para chegar o mais rápido possível à linha de chegada sem sair da pista.

### Configuração do ambiente

* **Estados**: posição do carro em um tabuleiro (grid) **+** velocidade discreta de 0 a 4 no eixo x e y $(v_x,v_y)$. Na linha de partida ambas velocidades iniciam em 0.
* **Ações**: incrementos independentes $\Delta v_x,\,\Delta v_y \in \{-1,0,+1\}$ ⇒ 6 ações. As velocidades não podem ser negativas, nem ambas zero fora da largada.
* **Dinâmica**: a cada passo o carro se desloca segundo a nova velocidade. Antes de mover, traça‑se a linha do caminho previsto:

  * Se cruza a **linha de chegada**, o episódio termina.
  * Se cruza **qualquer** borda da pista, o carro **volta** a uma posição aleatória da linha de partida com velocidade $(0,0)$.
* **Ruído de controle**: com probabilidade 0,1 ambos incrementos são forçados a 0 (falha de aceleração).
* **Recompensa**: $-1$ por passo até cruzar a chegada (custo de tempo).

Mapas sugeridos:

<img width="772" height="448" alt="image" src="https://github.com/user-attachments/assets/2e82f8c3-1b23-444e-9706-429e7ccbb471" />


### Tarefas solicitadas

1. **Implementar** o ambiente *Racetrack* conforme descrito.
2. **Visualizar** o ambiente usando matbplotlib, pode ser uma tabela bem simples mesmo.
3. **Treinar** dois agentes independentes:

   * **SARSA** (on‑policy).
   * **Q‑Learning** (off‑policy).


### Sugestões:
* Primeiro faça uma versão jogável do ambiente para testar como funciona e se esta correto (sem os agentes).
* Faça a função valor para todas as celulas e todas as velocidades, para gerar isso é um loop quadruplo, um loop inicial para gerar o eixo x do grid, outro loop pro eixo y, e outro para as velocidades vx e vy.
* Faça o ambiente e o agente em classes de python diferentes.


# 
