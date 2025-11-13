
# A* + MST — Conectividade Viária entre Shoppings no Nordeste Brasileiro

Este projeto aplica os algoritmos **A\*** e **Árvore Geradora Mínima (MST)** para analisar a conectividade dos shoppings das **nove capitais do Nordeste**.  
O objetivo é estimar o **menor comprimento total de vias** necessário para interligar todos os centros comerciais de cada cidade, utilizando dados reais do **OpenStreetMap (OSM)** e técnicas de grafos.

---

## 🎯 Objetivos e Fundamentação

O método combina dois algoritmos fundamentais:  
- **A\*** encontra o menor caminho entre dois pontos utilizando heurística **great-circle**, que leva em conta a curvatura da Terra e garante eficiência e otimalidade.  
- **MST**, implementada via algoritmo de **Kruskal**, determina a menor soma total de distâncias capaz de conectar todos os POIs.  

Essa integração permite estudar a **eficiência da malha urbana**, a **distribuição dos centros comerciais** e o custo mínimo necessário para conectá-los.

---

## ⚙️ Estrutura da Solução

1. Obtenção da rede viária (`graph_from_place`).  
2. Conversão da malha para grafo não-direcionado.  
3. Coleta de **todos os shoppings** mapeados (`shop=mall`).  
4. Associação dos POIs ao nó mais próximo da malha.  
5. Construção do grafo completo entre POIs com distâncias via A*.  
6. Cálculo da MST para determinar o menor conjunto de conexões.  
7. Reconstrução das rotas reais na malha urbana.  
8. Comparação detalhada entre as capitais.

---

## 🛠️ Tecnologias Utilizadas

- **Python 3.13+**: Linguagem de programação principal utilizada no projeto.
- **OSMnx**: Biblioteca para obtenção e manipulação de dados do OpenStreetMap.
- **NetworkX**: Biblioteca para criação, manipulação e análise de grafos complexos.
- **Jupyter Notebook**: Ambiente interativo para desenvolvimento e apresentação do projeto.
- **Pandas** - Processamento de dados.
- **Matplotlib** - Visualização de grafos 2D.

---

## 💻 Ferramentas e Ambientes
- [Jupyter Notebook](https://jupyter.org/) - Ambiente interativo de desenvolvimento
- [Google Colab](https://colab.research.google.com/) - Ambiente online gratuito para notebooks
- [Anaconda](https://www.anaconda.com/) - Distribuição Python para ciência de dados
- [Visual Studio Code](https://code.visualstudio.com/) - Editor de código recomendado

---

## 📊 Resultados Obtidos

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

## 🔍 Análise Crítica

**Teresina** apresentou a menor rede viária mínima para conectar seus shoppings, com cerca de **18,4 km**. Isso pode ser explicado pelo **menor número de shoppings (10)** e possivelmente por uma **maior concentração geográfica** desses estabelecimentos.

**Salvador** obteve o maior custo, necessitando de **quase 116 km** de vias para interligar seus **114 shoppings**.  A grande extensão territorial da cidade, sua **geografia acidentada** e o **alto número de POIs** contribuem para esse resultado.

Há uma **tendência clara**: cidades com mais shoppings tendem a ter uma **MST maior**. **São Luís (124 POIs)**, **Fortaleza (122 POIs)** e **Salvador (114 POIs)** ocupam as últimas posições, com as **maiores distâncias totais**. No entanto, essa relação **não é linear**. **Natal (74 POIs)** tem mais que o dobro de shoppings de **Recife (32 POIs)**, mas a diferença na MST é pequena — apenas **cerca de 800 metros**. Isso sugere que, em Natal, os shoppings podem estar **mais densamente agrupados**, ou a **malha viária é mais eficiente** para essas conexões do que em Recife, onde **barreiras geográficas** (como rios) podem aumentar as distâncias.

**Aracaju** e **Maceió**, com valores de MST próximos (**31 km** e **30,5 km**, respectivamente), demonstram uma **conectividade similar** para seus centros comerciais, apesar de Aracaju ter **mais shoppings (31 contra 21)**. Isso pode indicar um **planejamento urbano mais centralizado** em Aracaju.

Por fim, **João Pessoa** destaca-se pela **eficiência**: mesmo com **37 shoppings** (mais que Recife e Aracaju), sua MST é de apenas **25,9 km**, a **segunda menor do estudo**. Isso aponta para uma **excelente distribuição espacial** dos shoppings ou uma **malha viária muito direta**.


Outro aspecto relevante é a qualidade e completude dos dados do **OpenStreetMap**, que pode variar entre regiões, influenciando a quantidade detectada de shoppings e sua geolocalização. Além disso, cidades com maior número de POIs apresentam aumento expressivo no custo computacional, pois o grafo completo cresce quadraticamente. Mesmo com essas limitações, o estudo oferece uma visão robusta da conectividade urbana e permite comparar objetivamente como a geografia, o planejamento urbano e a expansão comercial influenciam o custo mínimo necessário para integrar os principais centros de consumo.

---

## 🏁 Conclusão

A combinação entre **A\*** e **MST** se mostra eficaz para investigar a conectividade urbana e analisar a distribuição espacial de atividades comerciais. Os resultados permitem não apenas compreender as diferenças estruturais entre as capitais nordestinas, mas também fornecer subsídios para estudos de **mobilidade**, **logística urbana**, **localização de serviços**, e **planejamento estratégico** baseado em dados abertos.

---

## 🧑‍💻 Autores  
Lucas Marques dos Santos e Leonardo Pessoa Cavalcanti.

---

## 🔗 Links Úteis

- [Documentação do Python](https://docs.python.org/3/)
- [Documentação do OSMnx](https://osmnx.readthedocs.io/)
- [Documentação do NetworkX](https://networkx.org/documentation/stable/)
- [Jupyter Notebook](https://jupyter.org/)
- [Documentação do Pandas](https://pandas.pydata.org/docs/) 
- [Documentação do Matplotlib](https://matplotlib.org/stable/index.html)
- [Vídeo Sobre o Projeto](https://drive.google.com/file/d/1zHTAW9ncozjCjFKDrhrepqUBXyDiaaqz/view?usp=sharing)
