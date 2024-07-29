# Q-Learning com OpenAI Gym: Taxi-v3 🚕

Este notebook implementa um sistema de busca no modelo A*, programado em Python. O objetivo do algoritmo é encontrar o caminho mais vantajoso até a cidade de **Curitiba**, partindo da cidade **Porto União**. Pense em um sistema de navegação 🚗.

## Descrição 🔎

Este projeto implementa um algoritmo de aprendizado por reforço chamado Q-learning para treinar um agente a resolver o ambiente Taxi-v3 da biblioteca OpenAI Gym. O objetivo é ensinar o agente táxi a pegar um passageiro em um local e deixá-lo em outro no caminho mais curto possível, evitando penalidades por movimentos ilegais.

## Instalação ⚒️

**Dependências**\
Para executar este projeto, você precisa das seguintes bibliotecas Python:

* numpy
* gym==0.17.3
* random
* time
* IPython
#
```python
!pip install gym==0.17.3
```

## Código 🔢
### 1. Configuração do Ambiente:

```python
import gym
env = gym.make('Taxi-v3')
```
### 2. Inicialização da Tabela Q:
```python
q_table = np.zeros([env.observation_space.n, env.action_space.n])
```


### 3. Treinamento do Agente: 🏋️

O agente é treinado em 100.000 episódios.
Os parâmetros do Q-learning usados são:

* alpha = 0.1    **(Taxa de aprendizado)**
* gamma = 0.6    **(Fator de desconto)**
* epsilon = 0.1 **(Taxa de exploração)**

#### Loop de treinamento:
```python
for i in range(100000):
    estado = env.reset()
    penalidades, recompensa = 0, 0
    done = False

    while not done:
        if random.uniform(0, 1) < epsilon:
            acao = env.action_space.sample()
        else:
            acao = np.argmax(q_table[estado])

        proximo_estado, recompensa, done, info = env.step(acao)

        q_antigo = q_table[estado, acao]
        proximo_maximo = np.max(q_table[proximo_estado])

        q_novo = (1 - alpha) * q_antigo + alpha * (recompensa + gamma * proximo_maximo)
        q_table[estado, acao] = q_novo

        if recompensa == -10:
            penalidades += 1

        estado = proximo_estado

    if i % 100 == 0:
        clear_output(wait=True)
        print('Episódio: ', i)

```

### 4. Avaliação:

O agente treinado é avaliado em 50 episódios para verificar seu desempenho.

```python
total_penalidades = 0
episodios = 50
frames = []

for _ in range(episodios):
    estado = env.reset()
    penalidades, recompensa = 0, 0
    done = False
    while not done:
        acao = np.argmax(q_table[estado])
        estado, recompensa, done, info = env.step(acao)

        if recompensa == -10:
            penalidades +=1

        frames.append({
           'frame': env.render(mode='ansi'),
           'state': estado,
           'action': acao,
           'reward': recompensa
           })

    total_penalidades += penalidades

print('Episódio, ', episodios)
print('Penalidades, ', total_penalidades)

```
### 5. Visualização:
O desempenho do agente pode ser visualizado usando os frames armazenados.
```python
for frame in frames:
    clear_output(wait=True)
    print(frame['frame'])
    print('Estado', frame['state'])
    print('Ação', frame['action'])
    print('Recompensa', frame['reward'])
    sleep(.7)

```

## Considerações finais: 🤓☝️
### **Notas**
A versão do gym usada neste projeto não requer renderização gráfica, tornando-o adequado para execução em linha de comando.

## Conclusão:

Este projeto demonstra a aplicação do Q-learning, um algoritmo de aprendizado por reforço sem modelo, para resolver o ambiente Taxi-v3. Ao final do treinamento, o agente táxi aprende a navegar pelo ambiente de forma eficiente, minimizando penalidades e completando as tarefas de maneira otimizada.

Sinta-se à vontade para experimentar o código e ajustar os parâmetros para ver como o desempenho do agente se altera.
