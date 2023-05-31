<h1>Algoritmo de Fortune e Diagramas de Voronoi</h1>

## Diagramas de Voronoi

Imagine o seguinte cenário:

Você é um piloto de avião da renomada companhia aérea *DESPROG AIRWAYS*. Durante uma noite longa de um voo rotineiro, de repente, o avião sofre uma **falha técnica letal**, sendo necessário realizar um pouso forçado nos próximos 15 minutos. Infelizmente essa falha afetou o sistema de localização da aeronave tornando-o inútilizável. Contudo, você lembra que possui um mapa da região que contém os aeroportos mais próximos. Como um piloto experiente você é capaz de usar a posição das estrelas a fim de descobrir a sua posição atual. Você marca a sua posição no papel e obtém o seguinte mapa:

![Imagem_Aviao](ex1.png)

???Exercicio 1
A partir do mapa acima como você determinaria o aeroporto mais próximo?
:::Gabarito
Uma das maneiras possíveis além do "olhômetro", seria descobrir a distância euclidiana do avião para cada aeroporto como na figura abaixo:

![Imagem_Aviao2](gabex1.png)    
:::
???

Você como um bom piloto descobriu a menor distância euclidiana a tempo e foi capaz de pousar o avião em segurança. Todavia, a companhia área determinou que no caso de outra emergência o piloto não pode ficar responsável por calcular tudo no momento começou a desenvolver um sistema de segurança para catástrofes similares.

???Exercicio 2
O primeiro desafio da companhia é a criação de um sistema que, para cada ponto no mapa, diga qual é o aeroporto mais próximo. De forma que, no momento de uma catástrofe basta o piloto conferir esse sistema e pousar.

:::Gabarito
Uma maneira possível é colorir o primeiro mapa de forma que cada aeroporto possuí uma cor específica e todo conjunto de pontos mais próximos a um aeroporto assume essa mesma cor:

![Imagem_Aviao2](gabex2.png)  
:::
???
A companhia criou o que chamamos de Diagrama de Voronoi. No "jargão de Voronói" os aeroportos são os pontos de interesse ("sites") e as áreas coloridas são as **regiões de influência**. Em uma região de influência **Todos os pontos dessa zona são mais próximos do sítio interno à ela do que qualquer outro**.

Para colorir o mapa a empresa tentou inicialmente calcular para cada metro quadrado no mapa a distância à todos aeroportos. Entretanto, logo a companhia percebeu que para mapas grandes e com vários aeroportos esse método torna-se computacionalmente muito caro.


![Imagem_aeroportos](airports.png)


A seguir veremos o algoritmo de Fortune, que está dentre os algoritmos mais eficientes na criação desse tipo de diagrama. 

## Algoritmo de Fortune

O Algoritmo de Fortune tem o seguinte objetivo: criar um Diagrama de Voronoi a partir dos pontos de interesse (os aeroportos) fornecidos como entrada.

Primeiramente, para entender a ideia do Algoritmo de Fortune é necessário entender o seguinte conceito:  *Linha de Varredura ("Sweep Line")*.

## Linha de Varredura

O algoritmo de Fortuna utiliza um método de varredura para construir o Diagrama de Voronoi. Um método de varredura consiste em dividir um plano em duas partes: a "suja" e a que já foi "varrida (limpa)". Esse esquema é criado para que possamos acionar os eventos do algoritmo, que serão discutidos futuramente no handout.

Precisamos de algo capaz de dividir um plano 2D em duas partes. Isso é uma tarefa perfeita para a uma **RETA**. Assim surge o conceito de "Linha de Varredura", uma linha que gradativamente vai "varrendo" os eventos do algoritmo.

Para essa reta varrer o plano inteiro ela tem que seguir apenas uma direção desde seu inicio até o fim. Nesse handout será utilizado uma reta que faz a varredura do eixo y, começando na parte superior até chegar a parte inferior (de cima pra baixo). As figuras abaixo demonstram o funcionamento de uma Linha de Varredura:

:linha


Para que a Linha siga a direção proposta os eventos a serem tratados primeiro são os que possuem o maior valor da coordenada y. Desse modo, o alogoritmo utiliza uma **fila de prioridade** para tratar a ordem dos eventos. 

Vale também ressaltar que é possível utilizar diferentes convenções da Linha de Varredura. Um exemplo é varrer dividindo o eixo x (Da esquerda pra direita).

## Arcos

Conforme o mapa é varrido pela linha, é necessário obter a região de influência de um sítio para um momento qualquer da varredura. É crucial obter uma resposta para essa pergunta, uma vez que com ela conseguiriamos ter um esboço do Diagrama de Voronoi para qualquer instância do algoritmo. Para descobrir essa resposta que tal colocarmos a mão na massa?

???Exercicio 3
A partir da figura abaixo tente esboçar na região já varrida a fronteira entre os seus sítios. Considere que um ponto que incide na Linha de Varredura já tenha sido varrido.

**OBS 1: Considere como fronteira um ponto que está a mesma distância de dois ou mais sítios**


![Questao3](parab1.png)

:::Gabarito
Como só existem dois pontos na figura, e esses possuem o mesmo valor de x a fronteira será exatamente um reta no ponto médio deles. Isso é demonstrado pela seguinte figura:

![Questao3_Gab](pgab1.png)

:::
???

???Exercicio 4

Com mais um sítio adicionado na figura tente novamente esboçar a fronteira entre os sítios.

![Questao4](parab2.png)

:::Gabarito

![Questao4_Gab](pgab2.png)

:::
???

???Exercicio 5

Com outro sítio adicionado, faça outra tentativa esboçar a fronteira entre os sítios da figura abaixo.

![Questao4](parab3.png)

:::Gabarito

![Questao4_Gab](pgab3.png)

:::
???

???Exercicio 6

Por fim tente fazer a mesma coisa para a figura abaixo:

**Dica: como a figura está espelhada a geometria será a mesma para ambos os lados** 

![Questao4](parab4.png)

:::Gabarito

![Questao4_Gab](pgab4.png)

:::
???

???Exercicio 7

A partir dos exercícios feitos é possível perceber a formação aproximada de um elemento geométrico conforme vamos a adicionando sítios sob a Linha de Varredura. Qual é esse elemento?

:::Gabarito
O elemento formado é uma parábola ou arco.
:::
???

Dessa maneira, caso adicionemos um número infinito de pontos sob a Linha de Varredura, teriamos uma parábola que nos mostra a região na qual todos os pontos estão mais próximos do sítio analisado à Linha de Varredura. Essa párabola pode ser evidenciada de maneira mais clara pela figura abaixo:

![Parabs](q4.png)

Sendo assim, esse arco é capaz de estimar a região de influência de um sítio para um momento qualquer da varredura. Vale ressaltar, que a parábola é apenas uma aproximação da área de influência, sendo que a área final pode acabar sendo maior que essa estimativa. 
   
## Evento de Inserção

## Evento de Circulo

## Complexidade

## Fontes:
* <https://demonstrations.wolfram.com/VoronoiDiagrams/>
* <https://demonstrations.wolfram.com/VoronoiDiagramsForEuropeanCities/>
* <https://users.cs.fiu.edu/~giri/teach/UoM/7713/f98/CYImage1.gif>
* <https://jacquesheunis.com/post/fortunes-algorithm/>
* <http://www.bitbanging.space/posts/voronoi-diagram-with-fortunes-algorithm>
* <https://iq.opengenus.org/content/images/2021/11/vor29.png>
* <https://www2.cs.sfu.ca/~binay/813.2011/Fortune.pdf>
