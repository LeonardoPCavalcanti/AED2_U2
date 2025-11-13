
# A* + MST — Conectividade Viária entre Shoppings no Nordeste Brasileiro

Este projeto aplica os algoritmos **A\*** e **Árvore Geradora Mínima (MST)** para analisar a conectividade dos shoppings das **nove capitais do Nordeste**.  
O objetivo é estimar o **menor comprimento total de vias** necessário para interligar todos os centros comerciais de cada cidade, utilizando dados reais do **OpenStreetMap (OSM)** e técnicas de grafos.

---

## Objetivos e Fundamentação

O método combina dois algoritmos fundamentais:  
- **A\*** encontra o menor caminho entre dois pontos utilizando heurística **great-circle**, que leva em conta a curvatura da Terra e garante eficiência e otimalidade.  
- **MST**, implementada via algoritmo de **Kruskal**, determina a menor soma total de distâncias capaz de conectar todos os POIs.  

Essa integração permite estudar a **eficiência da malha urbana**, a **distribuição dos centros comerciais** e o custo mínimo necessário para conectá-los.

---

## Estrutura da Solução

1. Obtenção da rede viária (`graph_from_place`).  
2. Conversão da malha para grafo não-direcionado.  
3. Coleta de **todos os shoppings** mapeados (`shop=mall`).  
4. Associação dos POIs ao nó mais próximo da malha.  
5. Construção do grafo completo entre POIs com distâncias via A*.  
6. Cálculo da MST para determinar o menor conjunto de conexões.  
7. Reconstrução das rotas reais na malha urbana.  
8. Comparação detalhada entre as capitais.

---

## Resultados Obtidos

| Cidade                        | POIs (shoppings) | MST_total_m | Status | Tempo (s) |
|:------------------------------|:----------------:|------------:|:------:|----------:|
| Teresina, Piauí, Brazil       | 10  | 13 830.796 | ok | 48.10 |
| João Pessoa, Paraíba, Brazil  | 37  | 25 865.062 | ok | 502.69 |
| Maceió, Alagoas, Brazil       | 21  | 30 529.684 | ok | 99.17 |
| Aracaju, Sergipe, Brazil      | 31  | 31 061.999 | ok | 29.19 |
| Recife, Pernambuco, Brazil    | 32  | 50 037.275 | ok | 266.38 |
| Natal, Rio Grande do Norte, Brazil | 74  | 50 805.824 | ok | 330.27 |
| São Luís, Maranhão, Brazil    | 124 | 70 152.596 | ok | 215.79 |
| Fortaleza, Ceará, Brazil      | 122 | 98 532.432 | ok | 436.87 |
| Salvador, Bahia, Brazil       | 114 | 115 839.173 | ok | 642.89 |

---

## Análise Crítica

A análise dos resultados revela diferenças marcantes no padrão de urbanização e distribuição comercial entre as capitais nordestinas. Cidades menores e mais compactas, como **Teresina** e **Aracaju**, apresentaram os menores valores de MST, o que indica que seus centros comerciais se concentram em regiões próximas e conectadas por uma malha viária eficiente. À medida que observamos cidades com maior porte populacional e expansão territorial, como **João Pessoa**, **Maceió** e **Recife**, o custo da MST aumenta devido à formação de eixos comerciais secundários e presença de barreiras naturais como rios, estuários e zonas costeiras.  

No caso de **Natal**, apesar de ter uma malha relativamente densa na zona central, a grande quantidade de shoppings distribuídos em regiões periféricas e ao longo do eixo sul eleva o custo total. Já cidades como **São Luís**, **Fortaleza** e principalmente **Salvador** apresentam cenários de urbanização policêntrica, onde múltiplos polos comerciais foram formados ao longo de décadas, espalhando-se por vasta área e exigindo longas conexões viárias entre eles. Essas cidades também possuem acidentes geográficos significativos, como baías, lagoas, dunas e áreas de preservação, que fragmentam a malha urbana e obrigam o algoritmo a percorrer rotas mais extensas.  

Outro aspecto relevante é a qualidade e completude dos dados do **OpenStreetMap**, que pode variar entre regiões, influenciando a quantidade detectada de shoppings e sua geolocalização. Além disso, cidades com maior número de POIs apresentam aumento expressivo no custo computacional, pois o grafo completo cresce quadraticamente. Mesmo com essas limitações, o estudo oferece uma visão robusta da conectividade urbana e permite comparar objetivamente como a geografia, o planejamento urbano e a expansão comercial influenciam o custo mínimo necessário para integrar os principais centros de consumo.

---

## Conclusão

A combinação entre **A\*** e **MST** se mostra eficaz para investigar a conectividade urbana e analisar a distribuição espacial de atividades comerciais. Os resultados permitem não apenas compreender as diferenças estruturais entre as capitais nordestinas, mas também fornecer subsídios para estudos de **mobilidade**, **logística urbana**, **localização de serviços**, e **planejamento estratégico** baseado em dados abertos.

---

## Tecnologias Utilizadas
- Python 3.13+  
- OSMnx  
- NetworkX  
- Pandas  
- Matplotlib  
- Jupyter Notebook  

---

## Autores  
Lucas Marques dos Santos e Leonardo Pessoa Cavalcanti.
