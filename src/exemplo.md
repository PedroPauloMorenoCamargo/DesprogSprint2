<h1>Algoritmo de Fortune e diagramas de Voronoi</h1>
<h2>Diagramas de Voronoi</h2>


Para primeiro entender o que o algoritmo de fortune faz, precisamos primeiro entender a razão pela qual ele existe. Suponha que você é um piloto, e no caso de uma pousagem de emergência, precisa saber qual o aeroporto mais próximo de você, independente de onde esteja. Para isso, você pega um mapa, e desenha um ponto (ou site, lembre desse nome) em cima de cada aeroporto. Após fazer isso, você desenha uma célula em volta de cada ponto, de forma que, para qualquer lugar dentro dessa célula, o aeroporto dentro dela esta mais próximo do que qualquer outro. Com isso você teria algo mais ou menos assim:


![Imagem_Voronoi_Mapa](ItalyVoronoiMap.png)


Agora, você tem no seu mapa, todas as regiões conhecidas como "áreas de influência" de cada ponto, ou seja, a região em que, para qualquer ponto dentro dela, o site mais próximo é o que está envolto na mesma célula.


Aplicando essa ideia para qualquer plano finito, com um número finito n de pontos, temos a idéia do diagrama de Voronoi. Ou seja, o que o diagrama de Voronoi nos dá é e área de influência dos sites contidos em um plano (podemos também extrapolar essa ideia para n dimensões, mas não tocaremos nisso). 

![Imagem_Voronoi_Plano_Genérico](VoronoiGenérico.png)



???Agora, esboçe um diagrama de voronoi para o seguinte plano
![Questao1](questao1.png)
:::Gabarito


O seu resultado deve ter saido parecido com algo assim: 


![Questao1](gab1.png)


:::
???

Mas como fazemos para sair do esboço e conseguir uma representação real de um diagrama de Voronoi?


Com o exercício, você deve ter percebido algo interessante sobre as fronteiras das células do diagrama. Por definição, elas são equidistantes dos sites das células com que fazem fronteira.


Com isso, conseguimos uma definição para as fronteiras das células. Assim, temos um norte para encontrar essas fronteiras, e consequentemente, as nossas células do diagrama.

<h2>O algoritmo de Fortune</h2>



Fontes: 
* <https://demonstrations.wolfram.com/VoronoiDiagrams/>
* <https://demonstrations.wolfram.com/VoronoiDiagramsForEuropeanCities/>
