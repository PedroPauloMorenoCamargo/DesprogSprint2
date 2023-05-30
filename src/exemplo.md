<h1>Algoritmo de Fortuna e diagramas de Voronoi</h1>

## Diagramas de Voronoi


Para primeiro entender o que o algoritmo de fortune faz, precisamos primeiro entender a razão pela qual ele existe. Suponha que você é um piloto, e no caso de uma pousagem de emergência, precisa saber qual o aeroporto mais próximo de você, independente de onde esteja. Para isso, você pega um mapa, e desenha um ponto (ou sítio, lembre desse nome) em cima de cada aeroporto. Após fazer isso, você desenha uma célula em volta de cada ponto, de forma que, para qualquer lugar dentro dessa célula, o aeroporto dentro dela esta mais próximo do que qualquer outro. Com isso você teria algo mais ou menos assim:


![Imagem_Voronoi_Mapa](ItalyVoronoiMap.png)


Agora, você tem no seu mapa, todas as regiões conhecidas como "áreas de influência" de cada ponto, ou seja, a região em que, para qualquer ponto dentro dela, o site mais próximo é o que está envolto na mesma célula.


Aplicando essa ideia para qualquer plano finito, com um número finito n de pontos, temos a idéia do diagrama de Voronoi. Ou seja, o que o diagrama de Voronoi nos dá é e área de influência dos sites contidos em um plano (podemos também extrapolar essa ideia para n dimensões, mas não tocaremos nisso). 

![Imagem_Voronoi_Plano_Genérico](VoronoiGenérico.png)

## O algoritmo de Fortuna

Primeiramente, para entender a ideia do Algoritmo de Fortune é necessário entender o seguinte conceito:  **Linha de Varredura ("Sweep Line")**.

O algoritmo de Fortuna utiliza um método de varredura para construir o diagrama de voronoi. Um método de varredura consiste em dividir um plano em duas partes: a *"suja"* e a que já foi *"varrida (limpa)"*. Esse esquema é criado para que possamos identificar o acionamento de eventos do algoritmo, esses que serão discutidos futuramente no handout.
\
\
Desse modo, no nosso caso precisamos de algo capaz de dividir um plano 2D em duas partes. Isso é uma tarefa perfeita para a geometria de uma **RETA** . Sendo assim, surge o conceito de  *"Linha de Varredura"*, uma linha que gradativamente vai "varrendo" o plano inteiro. 
\
\
Nesse handout, utilizaremos a linha de varredura conforme a imagem abaixo, sendo assim, ela é uma reta que começa na parte superior da imagem e faz a varredura do eixo y dela (De cima para baixo). 

![Gif_SweepLine](Scan.gif)

Além do mais, vale ressaltar que é possível utilizar diferentes convenções da Linha de Varredura. Um exemplo é varrer dividindo o eixo x (Da esquerda pra direita). Sendo assim, com os conhecimentos adquiridos sobre a Linha de Varredura que tal fazer alguns exercicíos.

???Exercicio 1
Como no algoritmo utilizamos a Linha de Varredura como referência, em um momento qualquer só temos conhecimento dos sítios que já foram varridos para esboçar o diagrama de voronoi.
\
\
Sendo assim, a partir da figura abaixo tente esboçar as áreas de influência dos sítios já varridos utilizando como fronteira do voronoi as dimensões do retângulo e a linha de varredura.  
![Questao1](q1.png)
:::Gabarito

Como no momento só existe um sítio que foi escaneado pela linha, só haverá ele no voronoi, dessa maneira, a área de influência dele é o diagrama por completo, uma vez que por definição não há nenhum ponto que é mais próximo de outro sítio do que ele mesmo. Dessa maneira, seu esboço deve ter ficado como a imagem abaixo:

![Questao1](q1gab.png)
:::
???

???Exercicio 2

Tomando como base o último exercício, o que aconteceria se adicionassemos um ponto recém varrido, ou seja, que acabou de ser escaneado pela Linha de Varredura como na figura abaixo. Tente novamente esboçar as áreas de influência dos sítios já varridos.

**OBS: Considere como "Recêm Varrido" um ponto que incide exatamente sobre a reta**

![Questao2](q2.png)
:::Gabarito

Com a existência de dois sítios o diagrama será dividido em dois, cada uma dessas partes será a área de influência de um desses sítios.

![Questao2](q2gab.png)
:::
???

O próximo exercício iremos fazer juntos, pois um novo conceito será introduzido. 
\
\
Ao adicionarmos dois sítios recém varridos na figura original obtemos a seguinte imagem como resposta:
\
**OBS: Considere como "Recêm Varrido" um ponto que incide exatamente sobre a reta**

![Questao3](q3gab.png)

A imagem acima faz sentido uma vez que por possuir três pontos será necessário a existência de três regiões de influência. Para casos de diagramas de voronoi com três ou mais regiões de influência, é possível a ocorrência de uma intersecção entre três ou mais áreas em apenas um ponto. Esse ponto é chamado de *Vértice de Voronoi*, esse que aparece como um circulo vermelho na imagem acima. 
\
\

Como dito anteriormente, um Vértice de Voronoi se encontra no local onde há a intersecção de três ou mais áreas de influência, e por ele estar situado nessa intersecção ele possui uma característica peculiar: a distância dele para os sítios das áreas onde ocorrem a intersecção é igual. Ou seja, tomando com exemplo a figura acima e atribuindo aos três sítios as seguintes variáveis (A,B,C) e ao Vértice de Voronoi (V), sabemos que a $\overrightarrow{AV} = \overrightarrow{BV} = \overrightarrow{CV}$.
\
\
Além do mais, o que aconteceria se continuássemos adicionando sítios sob a Linha de Varredura? A imagem a seguir nos mostra a resposta uma resposta para 8 sítos:

![Questao4](q4.png)

???Exercicio 3
A partir da imagem anterior, é possível perceber um padrão formado pelos Vértices de Voronoi. Considerando infinitos sítos recém varridos qual figura é esperada-se que o padrão forme? Podemos relacionar esses sítios infinitamente distribuidos sob a reta por um conceito já aprendido ?

:::Gabarito
O padrão visto deverá criar uma parábola. Sim, a distribuição desses infinitos sítios formam uma reta paralela com o eixo x, já que todos tem a mesma altura. Como todos eles incidem sob a Linha de Varredura eles são equivalentes a mesma.
:::
???

Dessa maneira, a área que essa parábola engloba serve como uma estimativa da área de influência de um único sítio em relação à posição da linha de varredura,desse modo, a parábola acaba por mostrar a região dos pontos que estão mais próximos do sítio que da Linha de Varredura. Valendo apena ressaltar que essa região de influência estimada da parábola pode mudar com o tempo. Essa asserção nos leva ao primeiro evento do nosso algoritmo. 


## Evento de Inserção

O evento de inserção ocorre quando Linha de Varredura encontra um sítio. Ao sítios ser escaneado ocorre a inserção de uma parábola (arco), essa parábola é a mesma que vimos anteriormente, ou seja, delinea a região de pontos que estão mais próximos do sítio do que da Linha de Varredura, isso faz com que a área da parábola aumente com o distanciamento da linha após o evento. Isso pode ser visto a partir das imagens simplificadas abaixo:

:insertion1

**OBS: A Imagem acima é apenas uma aproximação não contendo proporções exatas**

Agora que entendemos o evento de inserção imagine que dois sítios tenham sido captados por esses eventos, como vimos com o distanciamento gradativo da Linha as parábolas deles irão aumentar, assumindo que eles são próximos um do outro o é provável de acontecer quando a Linha de Varredura está distante desses sítios? **Uma Intersecão!**. Isso nos leva ao questionameto abaixo:

???Exercicio 4
Com o distanciamento gradativo da Linha de Varredura o que representaria dois arcos se intersectando?

**OBS: Lembre que os arcos são uma aproximação da região de influência de um sítio**
:::Gabarito
Ocorreria uma divisão, o ponto de intersecção das equações dos arcos em um momento qualquer divide as áreas de influência entre os sítios  das respectivas parábolas , ou seja, esses pontos acúmulados conforme a Linha de Varredura passam a formar uma das parte da divisa das regiões de influência. 
:::
???

Podemos observar essa intersecção abaixo:

:insertion2

## Evento de Circulo

Como visto anteriormente, os arcos são uma aproximação da região de influência, sendo que o encontro de dois deles gera um dos pontos de uma do diagrama de Voronoi e esse encontro continua com a expansão dos arcos. Se você esta sentido que a expansão transmite uma sensação estranhamente familiar você está correto, pois ela é um dos componentes do diagrama de voronoi, sendo esse componente as "Arestas de Voronoi"(ligações entre um vértice a outro).

???Exercicio 5

Como visto se a intersecção de dois arcos determina um ponto de uma Aresta de Voronoi, qual conceito aprendido é possível relacionar com essa situação?

**OBS: Lembre que os arcos são uma aproximação da região de influência de um sítio**

:::Gabarito
Seria um ponto em que há a divisão de três regiões de influência, isso que é exatamente a definição de um Vértice de Voronoi.
:::
???

Então vamos pensar em um plano para prosseguir: calcular as intersecções dos arcos e adicionar todos os pontos (Arestas e Vértices) encontrados a cada incremento da Linha de Varredura.

Esse plano realmente parece razoável? Pode ser que para casos simples não tenha muita diferença, mas com o incremento de sítios analisados o número de checagens de intersecções cresceria de forma absurda e a memória para armazenar todos esses pontos também, tornando essa ideia totalmente imprática. 

Vamos pensar de maneira mais simples, imagine os seguintes pontos da figura abaixo. Como transformar esse pontos distintos em um polígono?

![Poli](polig.png)

Para transformar os pontos em um polígono basta apenas conectá-los conforme a figura abaixo:

![Poli](polig2.png)

E para obtermos como montar o polígono quais informações utilizamos? **Apenas os Vértices do Polígono**. Sendo assim, esse é o "pulo do gato" precisamos saber apenas os vértices de voronoi para desenhar o diagrama.



Então prosseguindo, depois de pelo menos dois eventos de inserção precisamos descobrir se há Vértices de Voronoi no diagrama e suas exatas posições. Isso também lembra algo familiar? Pois é porque lembra mesmo, o momento que um Vértice de Voronoi se forma é exatamente na intersecção de três parábolas distintas. 

Utilizando a figura abaixo deve haver alguma maneira mais simples de descobrir o vértice do que checar todas as possíveis combinações de arco e checar exatamente a posição onde as três se encaixam. 

???Exercicio 6

Lembrando a propriedade de que um Vértice de Voronoi possui a mesma distância para os sítios das áreas em que ocorre a intersecção, existe alguma figura geometrica que podemos relacionar?

**Dica: Qual figura tem um centro que todos os pontos possuem a mesma distância dela?**

:::Gabarito
É um circulo sendo que o centro é o Vértice de Voronoi, e os sítios estão na circunferência dele.
:::
???

A imagem abaixo demonstra a relação evidenciada anteriormente:

![Circle](circulo1.gif)

Apesar de estarmos avançando ainda temos que determinar no algoritmo quando que ocorre essa intersecção. É agora que o algoritmo fica ainda mais interessante, por todos os arcos estarem em função da distância de seus respectivo sítios à Linha de Varredura, essa intersecção só é possível ocorrer quando a Linha de Varredura tangencia o Vértice, ou seja, ocorre quando o ponto com menor valor de y da circunferência incide na reta de escaneamento. Podemos ver isso a partir da seguinte figura:

![Circle](circle2.png)

Contudo, isso não é tudo sobre o evento. Vamos observar a imagem a seguir:

:circle

Podemos ver uma coisa interessante acontecendo, o ponto mais à esquerda teve sua parte direita da párabola totalmente consumida, isso ocorre por parte formar arestas e outra o vértice. Porém, a sua parte esquerda ainda continua crescendo após o evento. Isso causa a seguinte indagação: e se uma parábola for totalmente consumida como na figura abaixo?

![Circle](circle8.png)

**Ela é consumida por inteira**. Como os arcos são uma aproximação da região de influência de um sítio, ela ser consumida por inteira significa que todas as aresta e pontos  do diagrama que compõe ela estão calculados, ou seja, ela não possuirá nenhum Vértice de Voronoi no futuro. 

???Exercicio 7
Como não haverá Vértice de Voronoi futuramente precisamos mesmo checar se o sítio cuja parábola foi consumida possui uma intersecção de três arcos no futuro? 

:::Gabarito
Não, pois não haverá Vértices de Voronoi no limite da área de influência desse ponto. Sendo necessário apenas remover esse sítio da lista de eventos para não gastar poder computacional
:::
???

Em suma, o Evento de Círculo é um evento que sempre que há um incremento da Linha de Varredura descobre se o centro todos os arranjos de círculos criados assumindo que três sítios validos incidem em sua circunferência. Depois, de descobrir o centro necessitamos apenas descobrir se a Linha de Varredura tangencia o círculo em sua parte inferior,ou seja, dista R da reta, sendo R o raio do círculo. A partir disso, é checado se o arco de um do sítios foi consumido, se posistivo ele se torna um sítio inválido para passar pelo evento.

Tente fazer os seguintes exercícios:

???Exercicio 8
Quais das imagens abaixo representa um envento de Círculo:

Imagem 1:

![Circle](circle3.png)

Imagem 2:

![Circle](circle4.png)

Imagem 3:

![Circle](circle5.png)

:::Gabarito
Apenas a imagem três por ela ser a única em que o círculo tangencia a Linha de Varredura.
:::
???

???Exercicio 8
Em quais das imagens abaixo uma parábola foi consumida por inteiro:

:::Gabarito
Apenas a imagem três por ela ser a única em que o círculo tangencia a Linha de Varredura.
:::
???
## Pseudo-Código:

Juntando todas as ideias precisamos checar se ao incrementar a Linha de Varredura foi acionado algum evento, se esse não for o caso continuamos a varredua, por outro lado caso seja verdadeiro devemos analisar os eventos encontrados. Para o evento de inserção, devemos apenas adicionar o sítio a lista de sítios válidos e criar um arco. Além do mais, não podemos esquecer que precisamos guardar o Vértice de Voronoi dentro de um evento de circulo e checar se algum arco foi consumido, para retirar o sítio que possuia o arco.

???Exercicio 9
A partir das ideias expostas acima, tente criar a representação de um pseudocódigo.
:::Gabarito
``` c
while(Possui Eventos):
    Se occrreu um evento de inserção:
        Adicionar o sítio a lista de sítios válidos
        Criar arco
    Se ocorreu um evento de circulo:
        Obter e guardar Vértice de Voronoi
        Se arco foi consumido:
            Remover o sítio que possuia o arco
```
:::
???

## Fontes:
* <https://demonstrations.wolfram.com/VoronoiDiagrams/>
* <https://demonstrations.wolfram.com/VoronoiDiagramsForEuropeanCities/>
* <https://users.cs.fiu.edu/~giri/teach/UoM/7713/f98/CYImage1.gif>
* <https://jacquesheunis.com/post/fortunes-algorithm/>
* <http://www.bitbanging.space/posts/voronoi-diagram-with-fortunes-algorithm>
* <https://iq.opengenus.org/content/images/2021/11/vor29.png>
