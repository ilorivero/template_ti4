# 🕸️ 06 - Utilização de Grafos (Opcional)

**Atenção:** Este documento é opcional e deve ser preenchido apenas se o projeto utilizar conceitos de Teoria dos Grafos para modelar dados ou resolver problemas específicos.

## 1. Justificativa para o Uso de Grafos

A estrutura de dados de grafos foi escolhida para resolver o seguinte problema: [descrever o problema e por que um grafo é a solução ideal].

* **Exemplo 1 (Rede Social):** *Modelar as conexões entre tutores, cuidadores e seus pets. Isso nos permite, por exemplo, sugerir "cuidadores amigos de seus amigos" ou encontrar comunidades de tutores de uma mesma raça de cachorro.*
* **Exemplo 2 (Logística/Otimização):** *Calcular a rota mais curta para um cuidador que precisa visitar múltiplos pets em um mesmo dia, tratando as localizações como nós e as rotas entre elas como arestas com pesos (distância/tempo).*
* **Exemplo 3 (Sistema Antifraude):** *Identificar anéis de avaliações falsas, onde um grupo de usuários dá notas altas apenas entre si, formando um cluster densamente conectado no grafo de avaliações.*

## 2. Modelagem do Grafo

O grafo é estruturado com os seguintes componentes:

### Nós (Vértices)

Os nós representam as entidades principais do nosso sistema:

* `Usuario`: Representa um usuário, que pode ser um tutor ou um cuidador.
    * *Propriedades: `userId`, `nome`, `tipo` ('tutor'/'cuidador')*
* `Pet`: Representa um animal de estimação.
    * *Propriedades: `petId`, `nome`, `especie`, `raca`*
* `Localizacao`: Representa uma cidade ou bairro.
    * *Propriedades: `cidade`, `estado`*

### Arestas (Edges)

As arestas representam as relações entre os nós. O nosso grafo é **direcionado** e possui **arestas com pesos**.

* `(Usuario) -[:POSSUI]-> (Pet)`: Um tutor é dono de um pet.
* `(Usuario) -[:AVALIOU {nota: 5}]-> (Usuario)`: Um tutor avaliou um cuidador com uma nota. A nota é um peso na aresta.
* `(Usuario) -[:RESIDE_EM]-> (Localizacao)`: Um usuário mora em uma determinada localização.
* `(Usuario) -[:AMIGO_DE]-> (Usuario)`: Uma conexão mútua entre dois usuários (aresta não direcionada ou duas arestas direcionadas).

## 3. Tecnologia e Armazenamento

* **Banco de Dados de Grafo:** [Neo4j](https://neo4j.com/) (ou Amazon Neptune, TigerGraph, etc.).
* **Linguagem de Consulta:** Cypher (para Neo4j).
* **Alternativa:** Para grafos menores, a modelagem pode ser feita em memória usando uma biblioteca (ex: `NetworkX` em um backend Python) e populada a partir de um banco de dados relacional ou NoSQL.

## 4. Algoritmos Aplicados

Para extrair informações valiosas do grafo, aplicamos os seguintes algoritmos:

* **Busca em Profundidade/Largura (DFS/BFS):** Para encontrar se existe alguma conexão (ex: um "caminho de amizade") entre um tutor e um cuidador.
* **Caminho Mais Curto (Shortest Path - Dijkstra):** Para encontrar a rota mais eficiente para um cuidador visitar múltiplos clientes.
* **PageRank:** Para determinar a "influência" ou "reputação" de um cuidador com base não apenas na quantidade de avaliações, mas na reputação de quem o avaliou.
* **Detecção de Comunidades (Community Detection):** Para identificar grupos de tutores com interesses em comum (ex: donos de Golden Retrievers na mesma cidade) e criar fóruns ou eventos para eles.