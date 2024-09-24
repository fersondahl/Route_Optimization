
# Framework de Otimização de Rotas
> Otimização | Pyomo | PLI 

## 🎯 Objetivo
O foco desse projeto é o desenvolvimento de um modelo capaz de resolver problemas de roteamento. Sumariamente o modelo deve ser suficiente para ao receber um conjunto de coordenadas definir o trajeto mínimo viável passando por todos os pontos definidos.

No escopo desse projeto não serão avaliadas diferentes meios de transporte, barreiras físicas ou outros parâmetros que influam nas dificuldades de se chegar em cada coordenada. Vale destacar que esse tipo de avaliação não altera a modelagem em si, mas apenas o peso do percurso entre cada nó do problema na matriz de distâncias; Nesse caso serão consideradas as distâncias euclidianas.

## 💡 Estrutura da Modelagem
#### 🚶🏽 Caixeiro Viajante

O modelo proposto para o problema do caixeiro viajante (PCV) será utilizado como base para a definição do modelo matemático, seguindo a literatura dos Problemas de Programação Linear Inteira (PLI). Para a definição do modelo em *Python* foi utilizado o pacote **Pyomo**.

Em complemento ao modelo clássico de resolução do PCV, foi utilizada a formulação *DFJ* para contornar os problemas de viabilidade da solução. As restrições do tipo *DFJ* são implementadas utilizado o método de *Lazy Constraint* para evitar a explosão exponencial do problema.

#### 🧠 Modelo Matemático

*max* $\sum_{j=1}^{n}$ $\sum_{i=1}^{n}$ $x_{ij}$ * $d_{ij}$

*St.*

$\sum_{i=1}^{n}$ $x_{ij}$ = 1, ∀ j | j ≠ i

$\sum_{j=1}^{n}$ $x_{ij}$ = 1, ∀ i | j ≠ i

$\sum_{i ∈ K}$$\sum_{j≠i, j ϵ K}$ $x_{ij}$ ≤ |*K*| - 1, ∀ *K* ⊊ {1, ... , n}, |*K*| ≥ 2  (*DFJ*)

0 ≤ $x_{ij}$ ≤ 1, $x_{ij}$ ∈ ℤ

Sendo:

$x_{ij}$: Variável binária que assumirá 1 se o trajeto entre as cidades *i* e *j* for percorrido, e 0 caso contrário.  

$d_{ij}$: A distância entre as cidades *i* e *j*.


## 🏅 Solução do caso
Para ilustrar a implementação da solução, o estudo foi construído através do estudo de caso em que se buscara passar por todos os municípios do Rio de Janeiro. A solução do modelo é exibida a seguir:


![Optimal Route](optimal%20route.png)
