# ONDA VERDE

Este projeto tem como objetivo modelar, utilizando a ferramenta UPPAAL, um sistema de semáforos que permita a um motorista percorrer um trajeto de forma otimizada, passando por no máximo um semáforo vermelho.

## Etapa 1: Modelagem dos Autômatos Temporizados

Nesta etapa inicial do projeto, serão criados os modelos de autômatos temporizados que definem o comportamento dos 4 semáforos e do motorista. Abaixo estão os dados relevantes para a modelagem:

- **Distância do posto ao 1º semáforo:** 1.200m
- **Distância do 1º ao 2º semáforo:** 130m
- **Distância do 2º ao 3º semáforo:** 160m
- **Distância do 3º ao 4º semáforo:** 170m
- **Distância do 4º semáforo ao Rota:** 90m
- **Distância total:** 1.750m
- **Velocidade média de deslocamento:** 40 km/h

Para garantir que o motorista chegue ao destino parando em no máximo um semáforo, será necessário sincronizar os semáforos de forma inteligente, considerando as distâncias entre eles e a velocidade média de deslocamento.

## Verificação

A verificação é uma ferramenta essencial do UPPAAL, permitindo verificar se certas propriedades do sistema (*Reachability, Safety and Liveness*) são mantidas pela exploração *on-the-fly* do sistema em seu espaço de estados.

Para utilizar essa ferramenta, basta acessar o menu de opções do UPPAAL e selecionar a aba chamada "Verifier". Nesse menu, é possível escrever as queries (requisitos do sistema) para verificar se o modelo atende às especificações do projeto. O UPPAAL utiliza uma versão simplificada do Timed Computation Tree Logic (TCTL) para essa finalidade.

### A Linguagem de Busca (The Query Language)

A linguagem de busca consiste em *State formulae* e *Path formulae* (propriedades de estado e de caminho). Essa linguagem é formalmente expressa e bem definida, sendo legível tanto por humanos quanto por máquinas.

**State Formulae**:
Uma State formula é uma expressão que pode ser avaliada para um estado sem considerar o comportamento do modelo. Por exemplo, pode ser uma expressão simples como `i == 7`, que é verdadeira em qualquer estado onde `i` seja igual a 7. Também é possível testar se um processo P está em uma localização I usando a expressão na forma `P.I`.

**Path Formulae**:
Quantifica em um caminho ou *trace* de um modelo e é classificado como alcançável, seguro ou de liveness.

**Estados**:
São definidos como uma tupla (L, v), onde L é um vetor de localização e v é a função de avaliação que mapeia uma variável inteira e *clocks* para seus respectivos valores.

**Tipos de Queries**:
- Propriedades de alcançabilidade: Verifica se uma condição específica é mantida em um determinado estado ou em alguns comportamentos potenciais do modelo.
- Propriedades de segurança: Garante que uma condição específica é mantida em todos os estados de um caminho de execução.
- Propriedades de liveness: Garante que uma determinada condição será eventualmente verificada em algum momento.
- Propriedades de deadlock: Verifica se um deadlock é possível ou não no modelo.

**Tipos no UPPAAL**:
- E - Existe um caminho
- A - Para todos os caminhos
- [] - Todos os estados em um caminho
- <> - Algum estado em um caminho

Algumas combinações também são suportadas, como:
A[] <expressão>
E<> <expressão>
E[] <expressão>
A<> <expressão>
<expressão> --> <expressão>

**Verificação de Alcançabilidade**:
Verifica se algum estado é alcançável a partir do estado inicial.
- `E<> p`: É possível alcançar um estado onde p é satisfeito.
- p é verdadeira se pelo menos um estado é alcançável.
