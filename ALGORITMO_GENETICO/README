# Algoritmos Genéticos com MLROSE 🌹

Este notebook utiliza a biblioteca MLROSE para estudar algoritmos genéticos de busca. Através de uma lista de produtos que apresenta nome, volume e valor, o algoritmo busca identificar a melhor combinação de produtos para gerar o maior lucro possível em um espaço de **3 metros cúbicos**. 
Pense no baú de um caminhão de transporte 🚚.

## Descrição 🔎

O estudo faz parte de uma aula do curso **"Inteligência Artificial e Machine Learning: O Guia Completo" por Jones Granatyr**, disponível na Udemy. O código foi construído e testado na plataforma Google Colab.

## Instalação ⚒️

Para executar o notebook, é necessário instalar a biblioteca `mlrose`. Use o comando abaixo:

```python
!pip install mlrose
```
Além disso, é necessário importar o módulo six para compatibilidade com o sklearn.externals.six:

```python
import six
import sys
sys.modules['sklearn.externals.six'] = six
import mlrose
```
## Código 🔢
### Lista de Produtos
A lista de produtos é composta por tuplas contendo **o nome do produto, o volume em metros cúbicos e o valor em reais**:
```python
produtos = [
    ('Refrigerador A', 0.751, 999.90),
    ('Celular', 0.0000899, 2911.12),
    ('TV 55', 0.400, 4346.99),
    ('TV 50', 0.290, 3999.90),
    ('TV 42', 0.200, 2999.00),
    ('Notebook A', 0.00350, 2499.90),
    ('Ventilador', 0.496, 199.90),
    ('Microondas A', 0.0424, 308.66),
    ('Microondas B', 0.0544, 429.90),
    ('Microondas C', 0.0319, 299.29),
    ('Refrigerador B', 0.635, 849.00),
    ('Refrigerador C', 0.870, 1199.89),
    ('Notebook B', 0.498, 1999.90),
    ('Notebook C', 0.527, 3999.00)]
```
### Função de Impressão da Solução
A função imprimirsolucao imprime os produtos selecionados pelo algoritmo:

```python
def imprimirsolucao(lista):
    for i in range(len(lista)):
        if lista[i] == 1:
            print('%s - %s' % (produtos[i][0], produtos[i][2]))
```
### Função de Aptidão
A função fitnessfunction calcula o valor total dos produtos selecionados, penalizando soluções que excedem o espaço disponível:

```python
def fitnessfunction(lista):
    volumeOcupado = 0
    valorTotal = 0
    for i in range(len(lista)):
        if lista[i] == 1:
            valorTotal += produtos[i][2]
            volumeOcupado += produtos[i][1]
        if volumeOcupado > 3:
            valorTotal = 1
    return valorTotal
```
### Configuração do Problema
Configuramos o problema de otimização discreta com a função de aptidão customizada:
```python
fitness = mlrose.CustomFitness(fitnessfunction)
problema = mlrose.DiscreteOpt(length=14, fitness_fn=fitness, maximize=True, max_val=2)
```
### Execução do Algoritmo Genético
Executamos o algoritmo genético com uma população de 500 indivíduos e uma taxa de mutação de 0.2:

```python
melhorsolucao, melhorcusto = mlrose.genetic_alg(problema, pop_size=500, mutation_prob=0.2)
print(melhorsolucao, melhorcusto)
```
### Resultado 🤩
O resultado obtido pelo algoritmo é a melhor combinação encontrada de produtos que pode ser levada, maximizando o valor total sem exceder o espaço disponível:

```python
(array([0, 1, 1, 1, 1, 1, 0, 1, 1, 1, 0, 1, 1, 1]), 24993.550000000003)
```
## Conclusão ✅
Este notebook demonstra como utilizar a biblioteca MLROSE para resolver problemas de otimização usando algoritmos genéticos. Através deste estudo, foi possível identificar a melhor combinação de produtos que maximizam o lucro dentro de um espaço limitado.

