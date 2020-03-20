
# ficha 5

## Resoluções por Nuno Macedo

### Index

 - [Exercicio 1](#ex1) 
 -  [Exercicio 2](#ex2) 
 -  [Exercicio 4](#ex4) 
 - [in=[zero,succ]](#inzerosucc)
 - [Exercicio 5](#ex5) 

### <a id="ex1"></a> Exercicio 1

isomorfismo entre `(Cᴮ)ᴬ e (Cᴬ)ᴮ` ou seja, podemos sempre transformar uma função A -> B -> C em outra B -> A -> C.

então, queremos mostrar que `flip f x y = f y x`

e é-nos dada a def de `flip`
por isso, primeiro passo: aplicar essa def
o curry transforma uma função que recebe pares numa que recebe os argumentos separados
por isso se expandirmos o curry fica...
e agora sim podemos aplicar o comp
agora aparece-nos um `swap`
o `swap` simplesmente troca a ordem dum par
por exemplo, se fores ao ghci e pedires o tipo de curry tens...  
`curry :: ((a, b) -> c) -> a -> b -> c`
ou seja, recebe uma função que recebe pares, e passa a receber separado
o f recebe pares: f (a,b)
quando aplicas o curry ao f
ele passa a receber separados
por isso (curry f) a b
quando olham para a lei  
`(uncurry f) (a,b) = f a b`  
têm que ver que o f original é o do lado direito, e recebe separado
o do lado esquerdo é o transformado: recebe o par
##
Então:

    flip f x y  
    = { def-flip }  
    	curry (uncurry f . swap) x y  
    = { curry (81) }  
    	(uncurry f . swap) (x,y)  
    = { def-comp (70) }  
    	uncurry f (swap (x,y))  
    = { def-swap }  
    	uncurry f (y,x)  
    = { uncurry (82) }  
    	f y x



### <a id="ex2"></a> Exercicio 2

então, se vocês se lembram da última ficha, tínhamos visto que os naturais N eram isomórficos a 1 + N
quando recebíamos um natural ele ou era o zero, e marcávamos do lado esquerdo, ou era um natural n+1 e guardávamos o n do lado direito ora, esta maneira de ir "descronstruindo" naturais

permite-nos escrever funções recursivas, em que só temos que dizer o que fazer no caso de paragem (quando é zero) e como tratar a chamada recursiva (quando não é zero) se calhar para naturais nunca fizeram algo deste género, mas por exemplo, para listas, fartaram-se de fazer em PF e LI1

Ora, este padrão é tão comum, que tem um nome: são os catamorfismos um catamorfismo é um operador novo que nos permite fazer funções recursivas sobre tipos indutivos só temos que lhe passar duas coisas: o que fazer no caso de paragem, e o que fazer no caso recursivo e o tipo indutivo mais básico que vamos ver são os naturais (depois havemos de ver listas, árvores, etc)

então, o exercício 2 da ficha 5 é sobre isso para cada tipo indutivo, existe uma lei universal cata que tem pequenas variações dependendo o tipo concreto no exercício está a versão para naturais o que nos é dito é que podemos usar catas sobre naturais para fazer um ciclo `for`

partir da definição do `for` como um cata e mostrar que conseguimos chegar àquela definição pointwise dum ciclo

	for b i 0 = i  
	for b i (n+1) = b (for b i n)

(quando não é zero vamos aplicando `b` à passo seguinte, quando chegamos a zero devolvemos o valor de paragem `i`) então, tal como nos outros operadores, quando temos uma igualdade deste género geralmente temos que arrancar com a lei universal como é que faço isso aqui? temos a lei universal cata para naturais no exercício

##

    for b i = ⦇[i̲, b]⦈  
    ≡ { universal-cata (43) }  
    	for b i . in = [i̲, b] . (id + for b i)  
    ≡ { absorção-+ (21), natural-id (1) }  
    	for b i . in = [i̲, b . for b i]  
    ≡ { universal-+ (17) }  
    	for b i . in . i1 = i̲   
    	for b i . in . i2 = b . for b i  
    ≡ { def-in }  
    	for b i . [zero, succ] . i1 = i̲   
    	for b i . [zero, succ] . i2 = b . for b i  
    ≡ { cancelamento-+ (18) }  
    	for b i . zero = i̲  
    	for b i . succ = b . for b i  
    ≡ { introduzir variáveis }  
    	(for b i . zero) () = i̲ ()  
    	(for b i . succ) n = (b . for b i) n  
    ≡ { def-zero, def-succ, def-const, def-comp }  
    	for b i 0 = i  
    	for b i (n+1) = b (for b i n)

### <a id="ex4"></a> Exercicio 4

lidar com um catamorfismo concreto: subtrair um natural a um inteiro através de subtrações sucessivas de 1
ou seja...
implementar, por exemplo, o `a⊖3` à custa de `a-1-1-1` a intuição é mais ou menos simples: enquanto o `n` não é zero, vamos subtraindo 1 o que o exercício pede é para definir o cata que faz isto dando a dica de que ele vai ter a forma `⦇[const k, g]⦈` 

(const a é a função constante, seria sublinhado no cálculo)

universal-cata, universal-+ (ou eq-+ como o vosso colega sugeriu) para chegarmos a  

    a ⊖ 0 = a  
    a ⊖ (n + 1) = (a ⊖ n) - 1

vamos olhar para a solução pointwise  

    a ⊖ 0 = a  
    a ⊖ (n + 1) = (a ⊖ n) - 1

quando não temos zero, fazemos a chamada recursiva de depois -1 quando chegamos a zero, devolvemos o `a` ou seja, vamos ter algo do género `a-1-1-1...-1-1` se temos `(a⊖) = ⦇[const k, g]⦈` , o `k` vai ser o valor que é devolvido quando chegamos a zero, e o `g` vai ser a função que aplicamos em cada passo recursivo podemos chegar lá por intuição, mas o mais seguro é ir expandido aquela equação que nos é dada

essa é a tal parte que varia dependendo do tipo em questão para os naturais temos `F T = 1 + N` e `F f = id + f`
então, `k` é o valor q devolvemos no caso de paragem, o `a`
o `g` é o que fazemos ao resultado da chamada recursiva, -1

ou se quiserem, `pred` para bater certo com o `succ`

então, para não nos esquecermos de que tudo isto são programas


##

    (a⊖) = ⦇[const k, g]⦈  
    ≡ { universal-cata (43), F T = 1 + T }  
    	(a⊖) . in = [k̲, g] . (id + (a⊖))  
    ≡ { absorção-+ (21), natural-id (1), def-in naturais }  
    	(a⊖) . [zero,succ] = [k̲, g . (a⊖)]  
    ≡ { universal-+ (17) }  
    	(a⊖) . [zero,succ] . i1 = k̲  
    	(a⊖) . [zero,succ] . i2 = g . (a⊖)  
    ≡ { cancelamento-+ (18) }  
    	(a⊖) . zero = k̲  
    	(a⊖) . succ = g . (a⊖)  
    ≡ { introduzir variáveis }  
    	((a⊖) . zero) () = k̲ ()  
    	((a⊖) . succ) n = (g . (a⊖)) n  
    ≡ { def-comp, def-zero, def-const, def-succ }  
    	a⊖0 = k  
    	a⊖(n+1) = g (a⊖n)

## <a id="inzerosucc"></a> in=[zero,succ]?

para cada tipo indutivo nós temos que saber como o construir e destruir, de certa maneira

nomeadamente, no caso dos naturais temos que saber como andar entre N e 1 + N e isso é feito com as funções `in` e `out` especificas para cada tipo o `in` é o que constrói, o `out` o que destrói o `in` dos naturais recebe um valor 1 + N

ora isto é um either, que trata do lado esquerdo ou do lado direito quando é do lado esquerdo, como já vimos, representa o 0 daí a função `zero` quando é do lado direito, representa o predecessor do natural que estamos a criar então temos que adicionar 1, daí o `succ`

por isso o `in` dos naturais é `[zero,succ]` se escreverem pointwise isto vai dar  

    in (Left ()) = 0  
    in (Right n) = n+1

sim, para naturais é sempre este!

## <a id="ex5"></a> Exercicio 5

o ex 5 pede-nos para codificar catas em haskell as definições dos operadores são-nos dadas só temos que converter aquilo em haskell em particular, temos que ir definir o `out` dos naturais o `out` é o N -> 1 + N e a definição está na ficha 4
    


claro que o ex 4 também pode ser escrito em haskell, e aí não precisas do `for` então, o `out` é o tal que expande os naturais para 1 + N, e é fácil de ver que a definição em haskell é (edited)

vinda da ficha 4, ex 3 tal como o `in` , o `out` é sempre o mesmo para cada tipo

e agora o cata, qual vai ser o tipo dele? olhem para os catas que definimos sobre naturais qual é o tipo daquilo que aparece entre ⦇ ⦈

então? é uma um either que recebe ou 1 ou N e devolve outra coisa qualquer

por isso temos que definir em haskell um operador `cata` , por exemplo que uma função e cria um catamorfismo

se olharem para a def do ex5 já temos o out

o . é nativo em haskell o id também e se usarem a biblioteca de CP também têm o + por isso a tradução é direta

pronto, podem correr o ghci, ver o tipo do `cata`  
e ver que bate com o que estávamos à espera  
`cata :: Integral c => (Either () d -> d) -> c -> d`


recebe uma função que pega num either e dá outro valor qualquer, o `g` do cata depois fica à espera dum natural

e devolve valores do tipo que o `g` produz agora é só codificar o `for`

`for b i = ⦇[i̲, b]⦈`

##
    out 0 = Left ()  
    out (n+1) = Right ncata g = g . (id -|- cata g) . out  
    for b i = cata (either (const i) b)

