<h1>Algoritmo de Fortune e Diagramas de Voronoi</h1>

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
Uma maneira possível é criar um mapa que divida as regiões que são mais próximas de um aeroporto do que outro (Áreas de influência). Isso pode ser explicitado pela figura abaixo, em que só de ve-la somos capazes de saber o aeroporto mais próximo:

![Imagem_Aviao2](gabex2.png)  
:::
???

Dessa maneira você criou o que chamamos de Diagrama de Voronoi. Esse diagrama utiliza os pontos de interesse (sites) para dividir o plano em diversas regiões de influência,sendo que essas áreas possuem a seguinte lei: **Todos os pontos de uma região de influência são mais próximos do site dentro dela do que qualquer outro**. No nosso cenário utilizamos os pontos de interesse (aeroportos) para calcular suas áreas de influência a fim de resolver o problema dado. Um outro exemplo de um Diagrama de Voronoi é a figura abaixo que utiliza os jogadores em campo como ponto de interesse:

![Imagem_Tebas](exemplo.jpeg)  

Os Diagramas de Voronoi possuem diversas aplicações, uma delas é na área de geometria computacional. Desse modo, nessa aula será estudado o Algoritmo de Fortune, um dos algoritmos capaz de criar um desses diagramas.

## Algoritmo de Fortune

O Algoritmo de Fortune tem o seguinte objetivo: criar um Diagrama de Voronoi a partir dos pontos de interesse fornecidos como entrada.

Primeiramente, para entender a ideia do Algoritmo de Fortune é necessário entender o seguinte conceito:  *Linha de Varredura ("Sweep Line")*.

## Linha de Varredura

O algoritmo de Fortuna utiliza um método de varredura para construir o Diagrama de Voronoi. Um método de varredura consiste em dividir um plano em duas partes: a "suja" e a que já foi "varrida (limpa)". Esse esquema é criado para que possamos acionar os eventos do algoritmo, esses que serão discutidos futuramente no handout.

Desse modo, no nosso caso precisamos de algo capaz de dividir um plano 2D em duas partes. Isso é uma tarefa perfeita para a geometria de uma **RETA**. Sendo assim, surge o conceito de "Linha de Varredura", uma linha que gradativamente vai "varrendo" os eventos do algoritmo.

Para essa reta varrer o plano inteiro ela tem que seguir apenas uma direção desde seu inicio até o fim. Nesse handout será utilizado uma reta que faz a varredura do eixo y, começando na parte superior até chegar a parte inferior (de cima pra baixo). As figuras abaixo demonstram o funcionamento de uma Linha de Varredura:

:linha


Além do mais, para que a Linha siga a direção proposta os eventos a serem tratados primeiro são os que possuem o maior valor da coordenada y. Desse modo, o alogoritmo utiliza uma fila de prioridade a fim de tratar a ordem dos eventos. 

Vale também ressaltar que é possível utilizar diferentes convenções da Linha de Varredura. Um exemplo é varrer dividindo o eixo x (Da esquerda pra direita).

## Arcos

Com conhecimentos adquiridos anteriormente, surge a seguinte pergunta: Será que é possível estimar a região de influência de um sítio para um momento qualquer da varredura? Obter a resposta para essa pergunta é crucial, uma vez que com ela conseguiriamos ter um esboço do Diagrama de Voronoi para qualquer instância do algoritmo. Para descobrir essa resposta que tal colocarmos a mão na massa?

???Exercicio 3
A partir da figura abaixo tente esboçar na região já varrida a fronteira entre os seus sítios. Considere que um ponto que incide na Linha de Varredura já tenha sido varrido.

**OBS 1: Considere como fronteira um ponto que esta a mesma distância de dois ou mais sítios**


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

## Fontes:
* <https://demonstrations.wolfram.com/VoronoiDiagrams/>
* <https://demonstrations.wolfram.com/VoronoiDiagramsForEuropeanCities/>
* <https://users.cs.fiu.edu/~giri/teach/UoM/7713/f98/CYImage1.gif>
* <https://jacquesheunis.com/post/fortunes-algorithm/>
* <http://www.bitbanging.space/posts/voronoi-diagram-with-fortunes-algorithm>
* <https://iq.opengenus.org/content/images/2021/11/vor29.png>
* <https://www2.cs.sfu.ca/~binay/813.2011/Fortune.pdf>
