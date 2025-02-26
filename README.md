# Exportações brasileiras (2023)

As exportações do Brasil desempenham um papel fundamental na economia do país, sendo uma importante fonte de divisas e contribuindo significativamente para o crescimento econômico. O Brasil é um dos maiores exportadores globais, com produtos como soja, café, carne, minério de ferro, petróleo e produtos agrícolas dominando seus embarques internacionais. O agronegócio brasileiro, em particular, tem se destacado pela competitividade e pela presença em mercados-chave, como a China, Estados Unidos e União Europeia. Além disso, as exportações brasileiras são um reflexo da diversidade de sua produção, abrangendo tanto commodities quanto produtos manufaturados, o que fortalece sua posição no comércio global.

A presente análise contempla o volume exportado do Brazil no ano de 2023. Estes valores estão em US$ FOB (<i>Free on Board</i>). Segundo o IPEA, FOB dizer que o exportador é responsável pela mercadoria até ela estar dentro do navio, para transporte, no porto indicado pelo comprador. E "free" porque a mercadoria já deve ter sido desembaraçada na alfândega de partida e estar livre para ser levada.

**Cobertura temporal**: 2023
**Fonte**: Comexstat (https://comexstat.mdic.gov.br/pt/home)
### Extração dos dados
```
#Importar as bibliotecas
import pandas as pd
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

##Localizar os 10 maiores exportadores do Brazil em 2023
# Agrupar os dados por Países e somar os valores de exportação em 2023 em ordem decrescente
top_paises = df.groupby('Pais')['2023'].sum().sort_values(ascending=False).head(10)
print(top_paises)

#Plotar os 10 maiores exportadores do Brazil em 2023
# Plotar com o gráfico de barras vertical
plt.figure(figsize=(6,4))
top_paises.plot(kind='bar', color='skyblue')

# Adicionar título e rótulos aos eixos
plt.title('Top 10 Países Exportadores em 2023', fontsize=12)
plt.xlabel('Países', fontsize=10)
plt.ylabel('Valor FOB (Bilhões USD)', fontsize=10)

# Adicionar as labels ao eixo X e girando para melhor visualização
plt.xticks(rotation=45, ha='right', fontsize=10)
plt.yticks(fontsize=10)

# Exibir o gráfico
plt.tight_layout()  # Ajusta o layout para evitar sobreposição de textos
plt.show()
```

</span>

<div align="left">
<a href="https://colab.research.google.com/drive/1zR6yncMGbNFfSP9CrptXc99f-I5Kojy0?usp=sharing"><img src="https://github.com/user-attachments/assets/7496e3f4-703e-4bfa-a7ca-c0ea24963f4f" width="700px" />
</div>

<span align="left"> 

```
##Localizar os 10 maiores estados exportadores do Brazil em 2023
# Agrupar os dados por Países e somar os valores de exportação em 2023
top_estados = df.groupby('UF')['2023'].sum().sort_values(ascending=False).head(10)
print(top_estados)

#Plotar os 10 maiores exportadores do Brazil em 2023
# Plotar com o gráfico de barras vertical
plt.figure(figsize=(6,4))
top_estados.plot(kind='bar', color='purple')

# Adicionar título e rótulos aos eixos
plt.title('Top 10 Estados Exportadores em 2023', fontsize=12)
plt.xlabel('UFs', fontsize=0)
plt.ylabel('Em bilhões USD', fontsize=10)

# Adicionar as labels ao eixo X e girando para melhor visualização
plt.xticks(rotation=45, ha='right', fontsize=10)
plt.yticks(fontsize=10)

# Exibir o gráfico
plt.tight_layout()
plt.show()

```
</span>

<div align="left">
<a href="https://colab.research.google.com/drive/1zR6yncMGbNFfSP9CrptXc99f-I5Kojy0?usp=sharing"><img src="https://github.com/user-attachments/assets/735c74f3-c8f8-442a-9193-3176e90086f3" width="700px" />
</div>

<span align="left"> 

```
#Ver estatísticas descritivas
descricao = df['2023'].describe()
print("Estatísticas Descritivas das Exportações:")
print(descricao) 

Resultado:
Estatísticas Descritivas das Exportações:
count    3633.000000
mean        0.093503
std         0.658026
min         0.000000
25%         0.000138
50%         0.001643
75%         0.018508
max        18.160606
Name: 2023, dtype: float64

#Cruzar duas fontes diferentes 
df_pib = pd.read_excel('PIB.xlsx')
df_combinado = pd.merge(df, df_pib, on='Pais', how='inner')
print(df_combinado.head())

#Analisar a correlação entre estados e volume de exportação
correlacao = df_combinado[['PIB', '2023']].corr()
sns.regplot(x='PIB', y='2023', data=df_combinado, scatter_kws={'color':'blue'}, line_kws={'color':'red'})
plt.title('Correlação entre PIB e Volume de Exportação', fontsize=16)
plt.xlabel('PIB (Bilhões USD)', fontsize=12)
plt.ylabel('Volume de Exportação (Bilhões USD)', fontsize=12)
plt.show()

```
</span>

<div align="left">
<a href="https://colab.research.google.com/drive/1zR6yncMGbNFfSP9CrptXc99f-I5Kojy0?usp=sharing"><img src="https://github.com/user-attachments/assets/8eb36c9d-9854-4804-8a29-c0a9e82d0219" width="700px" />
</div>

<span align="left"> 

```
#Analisar a Regressão linear para prever exportações com base no ranking
dados = df_combinado[['PIB', '2023']]
slope, intercept, r_value, p_value, std_err = linregress(dados['PIB'], dados['2023'])
print(f"Coeficiente Angular (slope): {slope:.4f}")
print(f"Intercepto: {intercept:.4f}")
print(f"Coeficiente de Correlação (R²): {r_value**2:.4f}")
print(f"Valor p: {p_value:.4f}")

if p_value < 0.05:
    print("A relação entre o PIB e o volume de exportação é estatisticamente significativa.")
else:
    print("Não há evidências estatísticas suficientes para afirmar que o PIB influencia diretamente as exportações.")

Resultado: Coeficiente Angular (slope): -0.0000
Intercepto: 1.1153
Coeficiente de Correlação (R²): 0.0288
Valor p: 0.0050
A relação entre o PIB e o volume de exportação é estatisticamente significativa.

#Representar resultado em gráfico de barras horizontais
df_combinado_sorted = df_combinado.sort_values('PIB', ascending=False)
plt.figure(figsize=(10, 6))
sns.barplot(x='PIB', y='Pais', data=df_combinado_sorted, hue='Pais', palette='viridis', legend=False)
plt.title('PIB por País e Volume de Exportação', fontsize=16)
plt.xlabel('PIB (Bilhões USD)', fontsize=12)
plt.ylabel('Países', fontsize=12)
plt.show()

```
</span>

<div align="left">
<a href="https://colab.research.google.com/drive/1zR6yncMGbNFfSP9CrptXc99f-I5Kojy0?usp=sharing"><img src="https://github.com/user-attachments/assets/d74ac5e7-b624-44a7-9fba-67c527d77ad9" width="700px" />
</div>

<span align="left"> 
```

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
