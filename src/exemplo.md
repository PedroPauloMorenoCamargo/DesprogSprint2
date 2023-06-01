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

**OBS 1: a fronteira é o conjunto de pontos que está à mesma distância de dois ou mais sítios**

**OBS 2: As resposta são apenas uma aproximações da realidade, não contendo proporções exatas**

![Questao3](parab1.png)



:::Gabarito
Como só existem dois pontos na figura, e esses possuem o mesmo valor de x, a fronteira será uma reta no ponto médio deles. Observa-se isso na figura a seguir:

![Questao3_Gab](pgab1.png)

:::
???

???Exercicio 4

Quando adicionamos mais um sítio como ficam a(s) fronteira(s) entre eles?

**OBS: As resposta são apenas uma aproximações da realidade, não contendo proporções exatas**

![Questao4](parab2.png)

:::Gabarito

![Questao4_Gab](pgab2.png)

:::
???

???Exercicio 5

Repita o processo a fim de praticar.

**OBS: As resposta são apenas uma aproximações da realidade, não contendo proporções exatas**

![Questao4](parab3.png)

:::Gabarito

![Questao4_Gab](pgab3.png)

:::
???

???Exercicio 6

Por fim tente fazer a mesma coisa para a figura abaixo:

**Dica: como a figura está espelhada a geometria será a mesma para ambos os lados** 

**OBS: As resposta são apenas uma aproximações da realidade, não contendo proporções exatas**

![Questao4](parab4.png)

:::Gabarito

![Questao4_Gab](pgab4.png)

:::
???

???Exercicio 7

A partir dos exercícios feitos é possível perceber a formação de um elemento geométrico conforme vamos a adicionando sítios sob a Linha de Varredura. Qual é esse elemento?

:::Gabarito
O elemento formado é uma parábola ou arco.
:::
???

Dessa maneira, caso um número infinito de pontos fossem adicionados sob a Linha de Varredura, teríamos uma fronteira parabólica. Dentro dessa parábola todos os pontos estão mais próximos ao sítio do que da Linha de Varredura. Podemos ver essa párabola mais claramente na figura abaixo:

![Parabs](q4.png)

Podemos concluir que esse arco é capaz de estimar a região de influência de um sítio para um momento qualquer da varredura. Vale ressaltar, que a parábola (ou arco) é apenas uma aproximação da área de influência, sendo que a área final pode acabar sendo maior que essa estimativa  intermediária. 
   
## Evento de Inserção

Agora sabemos como estimar a região de influência de um sítio em relação a posição da Linha de Varredura. Mas como isso nos ajuda?

???Exercicio 8

Tente esboçar a área de influência do ponto de interesse em relação a Linha de Varredura em cada uma das situações abaixo:

**OBS: As resposta são apenas uma aproximações da realidade, não contendo proporções exatas**

:insertion

:::Gabarito 1

Como o ponto não foi varrido ainda somos incapazes de estimar sua área de influência.

![Insertion1](insertiongab1.png)

:::

:::Gabarito 2

Ao ser escaneado ocorre a inserção da parábola na figura. Como o foco da parábola incide sobre a 
linha de varredura, nesse passo a parábola é uma linha vertical para cima.

![Insertion2](insertiongab2.png)

:::

:::Gabarito 3

Como podemos ver, com o distanciamento da Linha de Varredura há o aumento da área de influência estimada do ponto, isso é, "a parábola cresce". REFAZER IMAGEM, LEMBRAR DEPOIS

![Insertion3](insertiongab3.png)

:::

:::Gabarito 4

Com um distanciamento ainda maior há um aumento proporcional da parábola. REFAZER IMAMGEM, LEMBRAR DEPOIS

![Insertion4](insertiongab4.png)

:::
???

Como vimos nos esboços anteriores, quando um ponto é escaneado surge uma parábola que estima sua região de influência na figura. Tendo isso em mente, podemos tratar de um dos eventos principais do Algoritmo de Fortune, o **Evento de Inserção**.  

:insertion1

Esse evento ocorre quando qualquer sítio é escaneado pela Linha de Varredura, nesse momento ocorre a inserção de uma parábola (arco). Essa parábola  delinea a região de pontos que estão mais próximos a esse sítio do que à Linha de Varredura. Isso faz com que a área da parábola aumente com o distanciamento da linha após o evento.

Contudo o algoritmo não analisa apenas um sítio, sendo necessário a análise de vários pontos de interesse simultâneamente.

## Intersecções

???Exercicio 9

Vamos analisar uma figura que possui dois pontos de interesse.

Tente esboçar as parábolas dos pontos de interesse em relação a Linha de Varredura em cada um dos instantes abaixo:

**OBS: As resposta são apenas uma aproximações da realidade, não contendo proporções exatas**

:insertion2

:::Gabarito 1

Como os pontos ainda não foram varridos somos incapazes de estimar suas área de influência.

![Insertion2](insertion21.png)

:::

:::Gabarito 2

Conforme os pontos são escaneados ocorre a inserção das parábolas na figura.

![Insertion2](insertiongab21.png)
:::

:::Gabarito 3

Com o distanciamento da Linha de Varredura há o aumento das parábolas.

![Insertion2](insertiongab22.png)
:::

:::Gabarito 4

Com um distanciamento ainda maior, é possível verificar uma intersecção entre os arcos.

![Insertion2](insertiongab23.png)

:::
???

Mas o que significa a intersecção de dois arcos? Quando consideramos o fato de que as parábolas representam a área de influência de seus pontos correspondentes, a intersecção representa uma **fronteira** entre essas áreas. (lembrando, uma fronteira é o conjunto de pontos que estão equidistantes a dois ou mais pontos de interesse).

:insertion3

Observe que as intersecções entre os arcos geram uma reta conforme a Linha de Varredura se distancia. Essa linha é a fronteira entre as regiões de influência dos sítios. Porém, o que acontece quando três parábolas se intersectam?


???Exercicio 10

Para descobrir a resposta, analise a figura a seguir:

Tente esboçar as parábolas dos pontos de interesse em relação a Linha de Varredura em cada um dos instantes abaixo:

**OBS: As resposta são apenas uma aproximações da realidade, elas não possuem proporções exatas**

:insertion4

:::Gabarito 1

Como os pontos ainda não foram varridos somos incapazes de estimar suas área de influência.

![Insertion4](insertiongab41.png)

:::

:::Gabarito 2

Ocorre a inserção da parábola do primeiro ponto de interesse.

![Insertion4](insertiongab42.png)
:::

:::Gabarito 3

Ocorre a inserção das parábolas restantes.


![Insertion4](insertiongab43.png)
:::

:::Gabarito 4

Com o distanciamento da Linha de Varredura, as parábolas laterais intersectam a parábola do sítio central

![Insertion2](insertiongab44.png)

:::
:::Gabarito 5

A parábola central é completamente consumida pelas laterais.

![Insertion2](insertiongab45.png)

:::
???

Retomando o conceito de que as parábolas estimam uma região de influência, o ponto resultante da intersecção de três arcos é equidistante aos três sítios. Esse ponto encontrado é denominado Vértice de Voronoi e ele provém da intersecção de três ou mais áreas de influência.

![Insertion1](ex2.png)

Isso é ótimo, pois descobrindo todos os bértices de Voronoi somos capazes de formar o Diagrama, basta apenas ligar esses vértices.  Tendo isso em mente, torna-se imperativo encontrar um jeito de, à partir da linha de varredura, determinar a posição de todos os vértices de Voronói.


???Exercicio 11

Vamos observar a figura anterior, é possível criar uma forma geométrica conhecida à partir dos pontos dados?

**OBS: Lembre da Equidistância entre o Vértice e os Sítios**

:::Gabarito 1

Sim, é possível formar um círculo com seu centro sendo o Vértice de Voronoi e seus sítios incidindo na circunferência. Podemos observar esse fato na imagem abaixo:


![Insertion1](ex3.png)
:::
???

Agora somos capazes de calcular as coordenadas dos Vértices de Voronoi, apenas com uma simples equção de círculo. Porém, ainda falta achar uma maneira de indentificar esse evento. Felizmente, a geometria dos arcos torna isso possível, visto que no exato momento em que ocorre a intersecção dos três arcos, a parte inferior do círculo tangencia a Linha de Varredura. Chamamos isso de **Evento de Círculo**, toda vez que detectamos um evento dessa natureza somos capazes de calcular um vértice de Voronói.

![Insertion1](ex4.png)

## Evento de Circulo

Juntando as ideias reunidas, um **Evento de Círculo** ocorre quando há a intersecção de três parábolas. O círculo é formado por três sítios distintos e tangencia, em sua parte inferior, a Linha de Varredura. Como o Vértice de Voronoi se localiza no centro dessa geometria podemos calcula-lo nesse instante. 

???Exercicio 12
Vamos fixar esse conceito. Quai(s) das imagens abaixo representa(m) um Evento de Círculo:

Imagem 1:

![Circle](circle3.png)

Imagem 2:

![Circle](circle4.png)

Imagem 3:

![Circle](circle5.png)

:::Gabarito
Apenas a imagem dois por ela ser a única em que o círculo tangencia a Linha de Varredura.
:::
???

Contudo, ainda há mais uma faceta a ser explorada em relação aos Eventos de Círculo.


???Exercicio 13

Quando os três arcos se intersectarem na figura abaixo, o que ocorre com a parábola do sítio superior direito?

![Circle](circle2.png)

:::Gabarito
Podemos observar pela representação da linha pontilhada que ela é totalmente **consumida** pelos outros arcos.
:::
???

Mas o que significa uma parábola ser **consumida**? Observe a imagem novamente:

![Circle](circle2.png)

Podemos ver que quando um arco é consumido,  toda a região de influência de seu sítio já foi calculada. Ou seja, a partir desse momento não precisamos mais considerar esse sítio em eventos futuros.

???Exercicio 14
Precisamos checar a ocorrência de novos Eventos de Circulo para um sítio cujo arco já foi consumido? 

:::Gabarito
Não, pois não haverá mais Vértices de Voronoi no limite da área de influência desse ponto, uma vez que toda sua região já foi calculada. Sendo necessário apenas remover esse sítio da fila de eventos para não gastar poder computacional.
:::
???

Porém, há casos nos quais o arco ainda não foi consumido completamente na intersecção entre as três parábolas. Observe o caso abaixo:

:consume

Na sequência acima é possível observar que o sítio superior esquerdo não tem seu arco consumido por completo na intersecção das três parábolas, mas apenas sua parte direita. A parte esquerda do arco ainda continua existindo e em expansão, dessa maneira, esse sítio ainda não pode ser removido da fila de prioridade uma vez que sua área de influência ainda não está completamente calculada.

## Complexidade

O cálculo da complexidade é relativamente simples. Para que a linha de varredura percorra os sítios de cima para baixo, é necessário ordenar esses pontos em relação a y.   

A ordenação tem uma complexidade de $O(nlog(n))$ (no melhor caso) e percorrer todos os Eventos possui complexidade $O(n)$. Dessa maneira, utilizando a propriedade da soma de complexidades obtemos no final uma complexidade $O(nlog(n))$.

![Circle](ex5.png)

## Fechamento:

    Seguem curiosidades sobre a implementação do algoritmo:

Primeira curiosidade, **não existe linha de varredura**. Isso mesmo, nas implementações mais comuns desse algoritmo não há linha de varredura, ela é um artifício visual para ilustrar a ordem conforme os vértices de Voronói vão sendo computados.

Segunda curiosidade, **as parábolas não existem**. Como a linha de varredura, as parábolas também não são computadas o tempo todo, elas são uma representação visual de como as regiões de influência evoluem conforme percorremos o plano e à partir desse conceito podemos derivar os eventos de círculo.

Finalmente, o algoritmo em sua essência consiste de percorrer os sítios em ordem descendente de ordenada e averiguar para cada evento de inserção (cada novo sítio percorrido), se houve um evento de círculo. Caso um evento de círculo aconteça, o vértice obtido é adicionado à uma lista de Vértices de Voronói e os sítios que se tornaram irrelevantes são deletados da fila de prioridade. Uma vez que todos os sítios foram inseridos podemos projetar os **Vértices de Voronói** sobre os planos e ligá-los uns aos outros e o produto é o nosso querido diagrama.



## Fontes:
* <https://demonstrations.wolfram.com/VoronoiDiagrams/>
* <https://demonstrations.wolfram.com/VoronoiDiagramsForEuropeanCities/>
* <https://users.cs.fiu.edu/~giri/teach/UoM/7713/f98/CYImage1.gif>
* <https://jacquesheunis.com/post/fortunes-algorithm/>
* <http://www.bitbanging.space/posts/voronoi-diagram-with-fortunes-algorithm>
* <https://iq.opengenus.org/content/images/2021/11/vor29.png>
* <https://www2.cs.sfu.ca/~binay/813.2011/Fortune.pdf>
* <https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTg6M_j8lSFkm0PsVelP6PBW1U3HXpNHx2mSwikLpJWYhpTrtYIXg4E--M59JtYRCiQTUc&usqp=CAU>
* <https://www.codeproject.com/KB/recipes/413452/Voronoi_diagram_section.png>
* <https://adrianmejia.com/images/time-complexity-examples.png>
