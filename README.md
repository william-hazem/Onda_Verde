## Verificação

A verificação é uma ferramenta do UPPAAL que permite verificar se certas propriedades do sistema (*Reachability, Safety and Liveness*) pela exploração *on-the-fly* do sistema em espaço de estados.

Esta ferramenta pode ser encontrado no menu de opções do UPPAAL na aba chamada verifier. Neste menu é possível escrever as queries (os requisitos do sistema), com o propósito de verificar se o modelo responde as especificações do projeto. O programa utiliza uma versão simplificada do Timed Computation Tree Logic (TCTL).

### A Linguagem de busca (The Query Language)

A linguagem de busca consiste de *State formulae* e *Path formulae* (propriedade de estado e propriedade de caminho). Esta linguagem é expressa formalmente e é bem definida, como também é uma linguagem de máquina legível.


**State Formulae** A State formula: é uma expressão que pode ser avaliada para um estado sem olhar para o comportamento do modelo. Por exemplo, pode ser uma expressão simples como `i == 7`, que é verdade em um estado qualquer onde `i` é iguala  7. Também é possível testar se um processo P está em uma localização I usando a expressão na forma `P.I`.


**Path formulae**: Quantifica em um caminho ou no *trace* de um modelo. É classificado como:
* Alcançável
* Seguro
* Liveness

**Estados**: São definidos como um tupla (L, v), onde L é um vetor de localização e v é a função de avaliação que mapeia uma variável inteira e *clocks* para seus respectivos valores.

**Propriedade de estado ou formula de estado**: Any side-effect free expression is a valid state property. É possível testar se um processo está em uma localização particular e se um estado é *deadlock*. Propriedades de estado são avaliadas para o estado inicial e para qualquer transição.

Exemplo:
```
E<> p1.cs and p2.cs
```

Propriedades de estado na localização:
. Expressões na forma P.l, onde P é um processo e l é uma localização, avalia para verdade em um estado (L, v) se e somente se P.l está em L.

Propriedade de Deadlock:
. O estado de propriedade *deadlock* é avaliada como verdadeiro para um estado (L, V) se e somente se para todo $d \get 0$ não existir nenhuma ação sucessora de (L, v + d). Em outras palavras, não existir nenhum estado (local) posterior a localização atual.

**Tipos de Queries**:
. Propriedades de alcançabilidade: Uma condição específica mantém-se num determinado estado(alguns) dos comportamentos potenciais dos modelos.
. Propriedades de segurança: Uma condição específica mantém-se em todos os estados de um caminho de execução.
. Propriedades de liveness: é garantido que uma determinada condição se verificará eventualmente( = num determinado momento).
. Propriedades de `deadlock`: Um `deadlock` é possível ou não no modelo.

**Tipos no UPPAAL**:
. E - existe um caminho
. A - para todos caminhos
. [] - todos os estados em um caminho
. <> - algum estado em um caminho

Algumas combinações também são suportadas:
```
A[] <expressão>
E<> <expressão>
E[] <expressão>
A<> <expressão>
<expressão> --> <expressão>
```

**Verificação de alcançabilidade**
Verifica se alguma estado é alcançável partindo do estado inicial.
. `E<> p`: é possível alcançar um estado em que p é satisfeito.
. p é verdadeiro se pelo menos um estado é alcançável.