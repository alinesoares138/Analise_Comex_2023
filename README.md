# Exportações brasileiras (2023)

As exportações do Brasil desempenham um papel fundamental na economia do país, sendo uma importante fonte de divisas e contribuindo significativamente para o crescimento econômico. O Brasil é um dos maiores exportadores globais, com produtos como soja, café, carne, minério de ferro, petróleo e produtos agrícolas dominando seus embarques internacionais. O agronegócio brasileiro, em particular, tem se destacado pela competitividade e pela presença em mercados-chave, como a China, Estados Unidos e União Europeia. Além disso, as exportações brasileiras são um reflexo da diversidade de sua produção, abrangendo tanto commodities quanto produtos manufaturados, o que fortalece sua posição no comércio global.

A presente análise contempla o volume exportado do Brazil no ano de 2023. Estes valores estão em US$ FOB (<i>Free on Board</i>). Segundo o IPEA, FOB dizer que o exportador é responsável pela mercadoria até ela estar dentro do navio, para transporte, no porto indicado pelo comprador. E "free" porque a mercadoria já deve ter sido desembaraçada na alfândega de partida e estar livre para ser levada.

**Cobertura temporal**: 2023
**Fonte**: Comexstat (https://comexstat.mdic.gov.br/pt/home)
### Extração dos dados
```
#Importar as bibliotecas
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

#Acessar o banco de dados
df = pd.read_excel('EXP2023.xlsx')
df = df.dropna()

#Renomear coluna
df = df.rename(columns={'2023 - Valor US$ FOB':'2023','UF do Produto':'UF'})

# Dividir a coluna 'volume' por 1.000.000
df['2023'] = df['2023'] / 1000000000
df.head()

```
## Processamento dos dados
```
**Renomear coluna
df = df.rename(columns={'2023 - Valor US$ FOB':'2023','UF do Produto':'UF'})

Dividir a coluna 'volume' por 1.000.000
df['2023'] = df['2023'] / 1000000000
df.head()

Localizar os 5 maiores importadores do Brazil em 2023
Agrupar os dados por Países e somar os valores de exportação em 2023
maiores_importadores = df.groupby('Países')['2023'].sum()

Ordenar os países pela exportação de 2023, de forma decrescente
maiores_importadores = maiores_importadores.sort_values(ascending=False)

Selecionar os 5 maiores importadores
top_5_importadores = maiores_importadores.head(5)

Exibir os 5 maiores importadores
print(top_5_importadores)

Plotar os 5 maiores importadores do Brazil em 2023
Plotar com o gráfico de barras vertical
plt.figure(figsize=(8,6)) 
top_5_importadores.plot(kind='bar', color='skyblue') 

Adicionar título e rótulos aos eixos
plt.title('Top 5 Países Importadores em 2023', fontsize=16)
plt.xlabel('Países', fontsize=0)
plt.ylabel('Em bilhões USD', fontsize=14)

Adicionar as labels ao eixo X e girando para melhor visualização
plt.xticks(rotation=45, ha='right', fontsize=14)
plt.yticks(fontsize=14)

Exibir o gráfico
plt.tight_layout()  # Ajusta o layout para evitar sobreposição de textos
plt.show()

```

</span>

<div align="left">
<a href="https://colab.research.google.com/drive/1zR6yncMGbNFfSP9CrptXc99f-I5Kojy0?usp=sharing"><img src="https://github.com/user-attachments/assets/24a397f4-9cc8-490f-932a-ecd1d095f217" width="700px" />
</div>

<span align="left"> 

```
Localizar os 5 maiores estados exportadores do Brazil em 2023
Agrupar os dados por Países e somar os valores de exportação em 2023
maiores_uf_exp = df.groupby('UF')['2023'].sum()

Ordenar os países pela exportação de 2023, de forma decrescente
maiores_uf_exp = maiores_uf_exp.sort_values(ascending=False)

Selecionar os 5 maiores estados exportadores (caso haja mais de 10)
top_5_uf_exp = maiores_uf_exp.head(5)

Exibir os 5 maiores estados exportadores
print(top_5_uf_exp)

Plotar os 5 maiores importadores do Brazil em 2023
Plotar com o gráfico de barras vertical
plt.figure(figsize=(8,6))  
top_5_uf_exp.plot(kind='bar', color='purple') 

Adicionar título e rótulos aos eixos
plt.title('Top 5 Maiores Estados Exportadores em 2023', fontsize=16)
plt.xlabel('UFs', fontsize=0)
plt.ylabel('Em bilhões USD', fontsize=12)

Adicionar as labels ao eixo X e girando para melhor visualização
plt.xticks(rotation=45, ha='right', fontsize=14)
plt.yticks(fontsize=14)

Exibir o gráfico
plt.tight_layout()  
plt.show()

```
</span>

<div align="left">
<a href="https://colab.research.google.com/drive/1zR6yncMGbNFfSP9CrptXc99f-I5Kojy0?usp=sharing"><img src="https://github.com/user-attachments/assets/02eba240-03cd-409f-b0a3-899354829c76" width="700px" />
</div>

<span align="left"> 

### Análise dos dados


Em 2023, as exportações brasileiras continuaram a mostrar um forte vínculo com seus principais estados produtores e parceiros internacionais. A dinâmica das exportações também refletiu as relações comerciais estratégicas que o Brasil mantém com diversos países.

Estados brasileiros e seus principais produtos exportados:

* São Paulo: São Paulo, o estado mais industrializado do Brasil, é responsável por exportações de produtos manufaturados e também de commodities como açúcar. A indústria paulista também exporta máquinas, equipamentos e produtos químicos, sendo um elo importante nas relações comerciais com os Estados Unidos e a União Europeia.
* Rio de Janeiro: Dentre os produtos mais exportados pelo estado do Rio de Janeiro, destaca-se: petróleo, produtos semiacabados, óleos combustíveis, motores/máquinas não elétricos e outros. E sua maior parceira foi a China, que representou 39% das exportações totais do estado.
* Mato Grosso: Este estado é um dos maiores exportadores do Brasil, especialmente em produtos agrícolas. A soja, milho e algodão são os principais itens exportados por Mato Grosso, sendo grandes responsáveis pelo crescimento das exportações brasileiras. O estado também lidera a exportação de carnes, principalmente para mercados asiáticos.

Países parceiros e sua forte demanda:
* A China continua sendo o maior parceiro comercial do Brasil. Em 2023, a demanda chinesa por soja, carne (bovina e de frango), minério de ferro e outros produtos agrícolas continuou em alta, consolidando a relação estratégica entre os dois países. A China, com seu enorme mercado e crescente demanda por alimentos e recursos naturais, permanece central para as exportações brasileiras.
* Estados Unidos: Os Estados Unidos também são um dos principais destinos das exportações brasileiras, principalmente de produtos manufaturados, como máquinas, equipamentos, e produtos químicos. Além disso, o Brasil também exporta para os EUA grandes volumes de café, carnes e açúcar.
* Argentina: Embora não tenha o volume das exportações para a China ou os EUA, a Argentina é um parceiro estratégico para o Brasil na América Latina, com destaque para a exportação de veículos, máquinas e equipamentos, além de produtos agrícolas. A proximidade geográfica e as relações comerciais estreitas favorecem esse intercâmbio.

Esses mercados continuam a ser essenciais para a sustentação das exportações, com o Brasil mantendo sua posição de destaque no comércio global.
