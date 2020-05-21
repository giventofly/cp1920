  

# ficha 11


## Resoluções por Renato Neves


### Index

-  [Exercicio 1](#ex1)
- [Exercicio 3a](#ex3a)
- [Exercicio 3b](#ex3b)
- [Exercicio 4](#ex4)
- [Exercicio 5](#ex5)


### <a id="ex1"></a> Exercicio 1

> Vão haver vários casos em que vão ficar supreendidos, pois vocês irão  
> ver que funções que processam elementos de uma estrutura de dados  
> também podem ser vistas como funções que geram elementos de uma  
> estrutura de dados :-). Por outras palavras, a mesma função pode ser  
> representada tanto como um catamorfismo ou como um anamorfismo.

Em particular, nós vimos o caso em que a função _length_ que calcula o comprimento de listas pode ser vista tanto como um catamorfismo (de **listas**) ou um anamorfismo (de **números naturais**). O exercício 1 mostra-nos como generalizar esta "descoberta".

`≡ { Lei universal-cata }`  
`≡ { Leis dos isomorfismos in/out ((2.18) e (2.19) dos apontamentos),`  
`propriedade grátis }`  
`≡ { Lei universal-ana }`

`Notem que começamos com um catamorfismo de listas com o functor F associado. Como estamos a falar de um catamorfismo de listas o functor F tem que ser o functor das listas, e por associação T1 tem que ser o conjunto das listas` 


`Por fim, nós acabamos com um anamorfismo de números naturais, e portanto G tem que ser o functor dos números naturais e T2 terá que ser o conjunto de números naturais por associação.` 

`Falta-nos a descobrir qual é a função alpha : 1 + A x X ---> 1 + X. Para isto basta lembrarem-se da aula passada. Na aula passada nós vimos que length = [( (id + p2) . out_1 )]` `, olhando para o nosso caso aqui identificamos alpha = (id + p2)`

### <a id="ex2"></a> Exercicio 2

O exercício aborda um tipo de dados que nós ainda não vimos na cadeira, nomeadamente o tipo de dados das **listas infinitas**. O functor e bifunctor associados são definidos como: (edited)

`F f = id x f`  
`B(f,g) = f x g`

O exercício pede-nos para provar uma propriedade acerca do anamorfismo de listas infinitas _repeat_. Dado um valor, o anamorfismo retorna uma lista infinita cujos elementos são esse mesmo valor. A propriedade que o exercício nos pede para provar é que dar um valor _f(a)_ à função _repeat_ é a mesma coisa que dar um valor _a_ à função _repeat_ e depois aplicar a função _f_ a cada elemento da lista que foi gerada. 

Notem que isto é uma propriedade de optimização: usar a função _f_ infinitas vezes no "fim" é a mesma coisa que aplicar a função _f_ apenas uma vez no "início".

`repeat . f = map f . repeat`  

`≡ { Definição map f e repeat }`  
`repeat . f = T f . [( <id,id> )]`  

`≡ { Absorpção-ana }`  
`repeat . f = [( B(f,id) . <id, id> )]`  

`≡ { Definição functor listas infinitas }`  
`repeat . f = [( (f x id) . <id, id> )]`  

`≡ { Absorpção-x }`  
`repeat . f = [( <f, id> )]`  

`≡ { Definição repeat }`  
`[( <id, id> )] . f = [( <f, id> )]`  
`<= { Fusão-ana }`  
`<id,id> . f = F f . <f, id>`  

`≡ { Fusão-x }`  
`<f,f> = F f . <f, id>`  

`≡ { Definição functor listas infinitas }`  
`<f,f> = (id x f) . <f, id>`  

`≡ { Absorpção-x }`  
`<f,f> = <f, f>`  

`≡ True`

### <a id="ex3a"></a> Exercicio 3a

Este exercício usa a noção de **hilomorfismo** para expressar **while-loops**. Lembrem-se dos vídeos que um hilomorfismo _h_ nada mais é que um anamorfismo [( g1 )] seguido de um catamorfismo ⦇ g2 ⦈:  

`⦇ g2 ⦈ . [( g1 )]`

Intuitivamente, o anamorfismo **gera** informação que depois o catamorfismo **processa**. Um hilomorfismo é geralmente expresso na forma `[| g2, g1 |]` que se desdobra em

`⦇ g2 ⦈ . [( g1 )]`

N.B. A estrutura de dados associada ao hilomorfismo dos ciclos while é a dos números naturais.

Os ciclos while que vamos aqui considerar são representados como `while p f g`. O `p` é um predicado que controla o ciclo, a função `f` expressa o comportamento dentro de cada ciclo, e a função `g` dita o comportamento após o ciclo `while` terminar.

(*) `(while p f g) (x)` pode-se ler como: "aplica `f` a `x` enquanto `p` for verdade para `x`; logo que deixe de ser verdade aplica `g` a `x`".

(relembrem também que p é um predicado)

Este exercício é o mais complexo da ficha, portanto vamos com calma (e espero que tenham visto o vídeo correspondente :))

A primeira alínea do exercício pede para convertemos o hilomorfismo correspondente ao `while` numa definição a la Haskell. Esta definição deve corresponder a (*) claro. 

`while p f g`  
`= { Definição while p f g }`  
`tailr (( g + f ) . (not . p)?)`  
`= { Definição tail recursion }`  
`[| [id,id], ( g + f ) . (not . p)? |]`  
`= { h = f . F h . g (dado na alínea) }`  
`[id,id] . F (while p f g) . ( g + f ) . (not . p)?`  
`= { Definição F }`  
`[id,id] . (id + (while p f g)) . ( g + f ) . (not . p)?`  
`= { Absorpção-+ }`  
`[id, (while p f g)] . ( g + f ) . (not . p)?`  
`= { Absorpção-+ }`  
`[g, (while p f g) . f] . (not . p)?`

Introduzindo variáveis,

`[g, (while p f g) . f] . (not . p)? (x)`  
`= { Definição composição e eithers }`  
`if not (p x) then (g x) else (while p f g (f x))`  
`≡ { Definição not e if-then-else }`  
`if (p x) then (while p f g (f x)) else (g x)`

Comparem com a descrição textual que tinhamos anteriormente

> (*) `(while p f g) (x)` pode-se ler como: "aplica `f` a `x` enquanto `p` for verdade para `x`; logo que deixe de ser verdade aplica `g` a `x`".

Ok, para este caso o que precisamos de saber é que para um predicado `p` isto é uma função

`p : X --> Bool` que retorna true ou false

nós podemos sempre construir uma função `p? : X --> X + X` tal que

`p? (x) = i1(x) se p(x) = True` (edited)

`p? (x) = i2(x) se p(x) = False`

Agora dado um either `[f,g] : X + X --> Y`

nós podemos compo-lo com `p? : X --> X + X` ficando com

`[f,g] . p? : X --> Y`

`[g, (while p f g) . f] . (not . p)? (x)`  
`= { Definição composição e eithers }`  
`if not (p x) then (g x) else (while p f g (f x))`  
`≡ { Definição not e if-then-else }`  
`if (p x) then (while p f g (f x)) else (g x)`

### <a id="ex3b"></a> Exercicio 3b

A segunda alínea do exercício pede-nos para provar uma propriedade que é em geral bastante útil para mostrar que dois ciclos while são iguais.

O primeiro passo consiste essencialmente em desenrolar a definição `tailr` por outras palavra

portanto só podemos aplicar a definição de `tailr` (dos doils lados da equação)

`[| g2, g1 |]` que se desdobra em `⦇ g2 ⦈ . [( g1 )]`

`≡ { Definição tailr (dos dois lados), definição hilomorfismo }`
`<= { f = g => h . f = h . g }`
`<= { Fusão-ana }`

Eu usei `f = g => h . f = h . g`

isto é fácil de provar

`h . f (x)`  
`= h (f x)`  
`= h (g x) (porque f x = g x)`  
`= h . g (x)` 

portanto `h . f = h . g`


### <a id="ex4"></a> Exercicio 4

O exercício 4 introduz o conceito de mónade, i.e. functores com certas propriedades especiais que são muito úteis na programação. Vamos apenas provar umas propriedades acerca de mónades para aquecer, e na aula seguinte vamos estudar o conceito mais a fundo.

As propriedades que vamos provar são acerca da composição monádica  Vamos provar (F5), que diz que u é o "elemento neutro" da composição monádica.

No F5 temos duas equações para provar, eu provo a primeira; vocês provam a segunda

`f • u`  
`= { Definição composição monádica }`  
`μ . T f . u`  
`= { Propriedade grátis (T f . u = T u . f) }`  
`μ . T u . f`  
`= { μ . T u = id }`  
`f`





### <a id="ex5"></a> Exercicio 5

O objectivo deste exercício é mostrar o poder de expressividade da composição monádica. Em particular, o objectivo é "descompactar" a  
definição de `discollect` via composição monádica para uma definição a la Haskell. Irão ver que a segunda definição é muito mais extensa que a primeira!


`discollect = lstr • id`  

`≡ { composição monádica (63) }`  
`discollect = μ . T lstr . id`  

`≡ { μ = concat = ⦇[nil,conc] ⦈ }`  
`discollect = ⦇[nil,conc] ⦈ . T lstr`  

`≡ { Absorpção cata, B(f,g)=id+f x g }`  
`discollect = ⦇[nil,conc] . (id + lstr x id)⦈`  

`≡ { Absorção + }`  
`discollect = ⦇[nil,conc . (lstr x id)]⦈`  

`≡ { Universal cata }`  
`discollect . in = [nil,conc . (lstr x id)] . (id + id x discollect)`  

`≡ { Absorpção-+, Functor-x }`  
`discollect . in = [nil,conc . (lstr x discollect)]`  

`≡ { Fusão-+, Eq-+ }`  
`discollect . nil = nil`  
`discollect . cons = conc .(lstr x discollect)`  

`≡ { Igualdade extensional, definição composição }`  
`discollect [] = []`  
`discollect(cons(h,t)) = conc (lstr h, discollect t)`  

`≡ { Definição de conc e cons }`  
`discollect [] = []`  
`discollect(h:t) = lstr h ++ discollect t`  

`≡ { Definição lstr (a,x)=[(a,b)|b ← x]. Assumimos que h := (a,x) }`  
`discollect [] = []`  
`discollect((a,x):t) = [(a,b)|b ← x] ++ discollect t`

