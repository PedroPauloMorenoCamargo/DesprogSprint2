<h1>Algoritmo de Fortuna e Diagramas de Voronoi</h1>

## Diagramas de Voronoi

Imagine o seguinte cenário:

Você é um piloto de avião da renomada companhia aérea *DESPROG AIRWAYS*. Durante uma noite longa de um voo rotineiro, de repente, o avião sofre uma **falha técnica letal**, sendo necessário realizar um pouso forçado nos próximos 15 minutos. Infelizmente essa falha afetou o sistema de localização da aeronave tornando-o inútilizável, contudo, você lembra que possui um mapa da região que contém os aeroportos mais próximos. Além do mais, como um piloto experiente você é capaz de usar a posição das estrelas a fim de descobrir a sua posição atual. Você marca a sua posição no papel e obtém o seguinte mapa:

![Imagem_Aviao](ex1.png)

???Exercicio 1
A partir do mapa acima como você descobriria qual dos três aeroportos é o mais próximo?
:::Gabarito
Uma das maneiras possíveis além do "olhômetro", seria descobrir a distância euclidiana do avião para cada aeroporto e descobrir qual deles está mais próximo como na figura abaixo:
![Imagem_Aviao2](gabex1.png)    
:::
???

Sendo assim, você como um bom piloto descobriu a menor distância euclidiana a tempo e foi capaz de pousar o avião em segurança. Todavia, a situação o afetou profundamente e questões as seguintes questões começaram a infiltrar seus pensamentos:  E se existissem muitos aeroportos na região, como eu poderia realizar tantos calculos? E se meu tempo fosse ainda mais limitado? 

Diante das seguintes questões você se sentiu aliviado por seu problema ter tido condições tão simples, porém a fim de evitar futuros acidentes você se propôs a criar uma solução mais efetiva para alguém que se encontre na mesma situação.

???Exercicio 2
Utilizando o mesmo mapa acima, existe uma maneira de representar as distâncias para os aeroportos de forma visual, para que não seja necessário o calculo da distância euclidiana?
:::Gabarito
Uma maneira possível é criar um mapa que divida as regiões que são mais próximas de um aeroporto do que outro (Áreas de influência). Isso pode ser explicitado pela figura abaixo:
![Imagem_Aviao2](gabex2.png)  
:::
???

Dessa maneira você criou o que chamamos de Diagrama de Voronoi. Esse diagrama utiliza os pontos de interesse (sites) para dividir o plano em diversas regiões de influência,sendo que essas áreas possuem a seguinte lei: **Todos os pontos de uma região de influência são mais próximos do site dentro dela do que qualquer outro. No nosso cenário utilizamos os pontos de interesse (aeroportos) para calcular suas áreas de influência a fim de resolver o problema dado. Um outro exemplo de um Diagrama de Voronoi é a figura abaixo que utiliza os jogadores em campo como ponto de interesse:

![Imagem_Tebas](exemplo.jpeg)  

Os Diagramas de Voronoi possuem diversas aplicações, uma delas é na área de geometria computacional. Desse modo, nessa aula será estudado o Algoritmo de Fortune, um dos algoritmos capaz de criar um desses diagramas.

## Algoritmo de Fortune

O Algoritmo de Fortune tem o seguinte objetivo: criar um Diagrama de Voronoi a partir dos pontos de interesse fornecidos como entrada.

Primeiramente, para entender a ideia do Algoritmo de Fortune é necessário entender o seguinte conceito:  *Linha de Varredura ("Sweep Line")*.


## Linha de Varredura


## Fontes:
* <https://demonstrations.wolfram.com/VoronoiDiagrams/>
* <https://demonstrations.wolfram.com/VoronoiDiagramsForEuropeanCities/>
* <https://users.cs.fiu.edu/~giri/teach/UoM/7713/f98/CYImage1.gif>
* <https://jacquesheunis.com/post/fortunes-algorithm/>
* <http://www.bitbanging.space/posts/voronoi-diagram-with-fortunes-algorithm>
* <https://iq.opengenus.org/content/images/2021/11/vor29.png>
* <https://www2.cs.sfu.ca/~binay/813.2011/Fortune.pdf>
