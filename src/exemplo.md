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

O evento de inserção ocorre quando um ponto é recém escaneado pela Linha de Varredura. Ao ser escaneado ocorre a inserção de uma parábola (arco), essa parábola é a mesma que vimos anteriormente, ou seja, delinea a região de pontos que estão mais próximos do sítio do que da Linha de Varredura, isso faz com que a área da parábola aumente com o distanciamento da linha. Isso pode ser visto a partir das imagens simplificadas abaixo:

:insertion1

**OBS: A Imagem acima é apenas uma aproximação não contendo proporções exatas**

???Exercicio 4
O caso acima nos mostra o que acontece para apenas um sítio o que nos leva a seguinte questão: O que aconteceria se dois arcos se intersectassem?
s
**OBS: Lembre que os arcos são uma aproximação da região de influência de um sítio**
:::Gabarito
Ocorreria uma divisão, o ponto de intersecção das equações dos arcos em um momento qualquer divide as áreas de influência entre os sítios  das respectivas parábolas , ou seja, esses pontos acúmulados conforme a Linha de Varredura passam a formar uma das parte da divisa das regiões de influência. Como evidenciado abaixo pela parte laranja da figura:

:insertion2

:::
???

Agora é possível entender como são desenhadas partes das regiões de influências, porém o funcionamento que nós vimos só funciona para um caso de intersecção de dois arcos, o que nos gera a seguinte dúvida o que acontece na intersecção entre três arcos? Isso será demonstrado no próximo tópico no próximo tema.
## Evento de Circulo

Fontes: 
* <https://demonstrations.wolfram.com/VoronoiDiagrams/>
* <https://demonstrations.wolfram.com/VoronoiDiagramsForEuropeanCities/>
