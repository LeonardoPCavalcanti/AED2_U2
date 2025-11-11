
# Trabalho 2 — Unidade 2 (A* + MST)

Este projeto integra os conceitos de **busca heurística (A\*)** e **Árvore Geradora Mínima (MST)** aplicados à malha viária real de cidades brasileiras.  
O objetivo é **estimar a distância total mínima necessária para interligar pontos de interesse (POIs)** em cada cidade, utilizando dados reais obtidos do **OpenStreetMap** através da biblioteca **OSMnx**, combinados com os algoritmos do **NetworkX**.

---

## Objetivos e Fundamentação

O trabalho propõe a aplicação conjunta dos algoritmos **A\*** (A-Star) e **Kruskal** (MST) em contextos geográficos reais.  
O **A\*** permite encontrar o menor caminho entre dois pontos, incorporando uma heurística que reduz o custo computacional e garante otimalidade quando admissível.  
A **MST (Árvore Geradora Mínima)**, por sua vez, fornece a menor soma de distâncias possível para conectar todos os POIs sem ciclos.

Assim, ao combinar ambos, obtemos uma estimativa do **menor comprimento total necessário para conectar todos os pontos de interesse urbanos** por vias reais — o que pode representar, por exemplo, o comprimento mínimo de infraestrutura (estradas, cabos, tubulações, etc.) necessária para integrar serviços distribuídos na cidade.

---

## Estrutura da Solução

1. **Modelagem do grafo viário:**  
   O grafo é obtido a partir do OpenStreetMap usando OSMnx, representando ruas, avenidas e conexões.  
   Foi utilizada a função `graph_from_place` com o tipo de rede `drive` (vias veiculares).

2. **Conversão e correção de atributos:**  
   Utilizou-se `ox.convert.to_undirected(G)` para tornar o grafo não-direcionado e `ox.distance.add_edge_lengths(G)` para garantir que todas as arestas possuam o atributo de comprimento (`length`).

3. **Cálculo de rotas A\*:**  
   O algoritmo A\* (`networkx.astar_path_length`) foi empregado entre todos os pares de POIs, com heurística **geodésica (great-circle)** — baseada na distância direta entre as coordenadas geográficas dos nós.  
   Essa heurística é **admissível**, pois nunca superestima a distância real, garantindo que os caminhos encontrados sejam ótimos.

4. **Formação do grafo completo de POIs:**  
   Cada cidade tem um grafo reduzido em que os vértices são os POIs (ex.: hospitais) e as arestas são ponderadas pelas distâncias calculadas via A\*.

5. **Cálculo da MST (Kruskal):**  
   Com o grafo completo ponderado, aplicou-se `networkx.minimum_spanning_edges`, equivalente ao algoritmo de **Kruskal**, para determinar a **menor soma total de arestas** capaz de conectar todos os POIs.

6. **Reconstrução das rotas reais e visualização:**  
   Cada aresta da MST foi mapeada de volta ao grafo viário original, reconstruindo o caminho real.  
   As rotas foram sobrepostas ao mapa para permitir uma **visualização espacial da conectividade mínima**.

7. **Comparação entre 8 cidades nordestinas:**  
   O pipeline foi executado em **Natal, João Pessoa, Recife, Maceió, Fortaleza, Teresina, São Luís e Aracaju**, com até 10 hospitais por cidade como POIs.

---

## Resultados Obtidos

| Cidade                        | POIs | MST_total_m | Status | Tempo (s) |
|-------------------------------|------|--------------|---------|-----------:|
| Aracaju, Sergipe              | 10   | 10774.997    | ok      | 23.92 |
| Fortaleza, Ceará              | 10   | 17648.124    | ok      | 71.22 |
| Natal, Rio Grande do Norte    | 10   | 20535.259    | ok      | 33.85 |
| João Pessoa, Paraíba          | 10   | 20746.817    | ok      | 29.71 |
| São Luís, Maranhão            | 10   | 21309.475    | ok      | 50.63 |
| Teresina, Piauí               | 10   | 23163.823    | ok      | 55.50 |
| Maceió, Alagoas               | 10   | 25816.122    | ok      | 31.14 |
| Recife, Pernambuco            | 10   | 30893.052    | ok      | 56.82 |

---

## Análise Crítica dos Resultados

As diferenças nos valores da MST entre as capitais refletem a **estrutura urbana** e o **grau de conectividade da malha viária** de cada cidade.  
Cidades mais compactas e bem conectadas, como **Aracaju (≈10,8 km)** e **Fortaleza (≈17,6 km)**, apresentaram **menores distâncias totais**, indicando que seus POIs estão mais próximos e acessíveis por rotas diretas.  
Já cidades como **Recife (≈30,9 km)** e **Maceió (≈25,8 km)** exibiram valores mais elevados, sugerindo **distribuição mais dispersa dos hospitais** e presença de **barreiras geográficas** (rios, áreas costeiras, pontes e vias sinuosas) que ampliam o trajeto médio.

A **escolha dos POIs** exerce impacto significativo: ao selecionar **hospitais**, o modelo reflete uma distribuição que geralmente cobre toda a cidade, incluindo regiões periféricas, o que aumenta o custo total da MST.  
Se fossem utilizados **POIs mais concentrados**, como escolas ou praças centrais, o valor total diminuiria substancialmente.  
Essa dependência demonstra como o método é sensível à natureza e à localização dos pontos analisados.

Entre as **limitações do método**, destacam-se:
- Dependência da **qualidade e completude dos dados** do OpenStreetMap (nem todos os POIs estão mapeados com precisão uniforme).  
- O modelo considera **apenas distâncias viárias**, ignorando fatores como **trânsito, topografia, sentidos das vias e acessibilidade**.  
- O número de POIs é reduzido (10 por cidade), o que simplifica a realidade e limita a generalização dos resultados.  
- O **A\*** trabalha em grafo planar e não incorpora restrições temporais ou dinâmicas (ex.: congestionamento).

Apesar dessas restrições, os resultados oferecem uma **visão consistente da conectividade urbana**, permitindo comparações entre cidades quanto à eficiência de suas redes viárias.  
O modelo pode ser expandido para estudos de **logística urbana, mobilidade de serviços públicos, transporte de emergência** e até **planejamento energético**, servindo como ferramenta analítica em decisões de infraestrutura.

---

## Conclusão

A combinação entre **A\*** e **MST** provou ser uma ferramenta eficiente para **avaliar a conectividade urbana** de forma quantitativa e espacialmente explícita.  
O estudo evidencia que cidades mais densas e planejadas exigem menor comprimento de vias para interligar serviços essenciais, enquanto cidades com expansão desordenada ou obstáculos naturais apresentam custos maiores.  
Com ajustes e ampliações, este modelo pode evoluir para uma poderosa abordagem de **planejamento urbano baseado em dados abertos**.
