
# ficha 4

## Resoluções por Renato Neves

### Index
- [Exercicio 1](#ex1)
- [Exercicio 2](#ex2)
- [Exercicio 3](#ex3)
- [Exercicio 4 a)](#ex4a)

### Introdução

Nesta ficha vamos começar por estudar um novo combinador, de forma a termos acesso a formas mais poderosas de compor programas. Nomeadamente, vamos começar por estudar o condicional de McCarthy que nos permite escrever expressões "if-then-else".

Olhando para a ficha, notem que p -> f,g representa um programa que dado um x, retorna f(x) ou g(x), dependendo se p envia x para f ou para g respectivamente. Podem pensar que p é uma espécie de controlador de  
carris numa bifurcação que direciona um comboio (o input x) ou para a esquerda ou para a direita. Em cada lado da bifurcação estarão o f e o g à espera do dito comboio.

mais tecnicamente 'p' representa um predicado

### <a id="ex1"></a> Exercicio 1

O exercício 1 pede para provar a equação:
    `(p -> f,g) . h = (p . h) -> (f . h), (g . h)`
 
##
Como de costume, sugiro que começem pelo lado "mais complicado da equação" e tentem chegar ao lado "mais simples" usando as leis de cálculo de programas. Vou-vos dar uma ajuda:

`(p . h ) -> (f . h), (g . h)`  
`= { Lei (30) }`  
`[f . h, g . h] . (p . h)?`  
`= { Lei (22) }`  
`[f, g] . (h + h) . (p. h)?`  
`= { Lei (29) }`  
`[f,g] . p? . h`  
`= { Lei (30) }`  
`(p -> f,g) . h`

### <a id="ex2"></a>Exercicio 2

No ex. 2, vamos começar por tentar provar a equação (F3).

`<(p → f , h), (p → g, i )> = p → <f , g>, <h, i> (F3)`

##
`<(p -> f,h) (p -> g,i)>`  
`= { Lei (30) }`  
`<[f,h] . p?, [g,i]. p?>`  
`= { Lei (9) }`  
`<[f,h], [g,i]> . p?`  
`= { Lei (28) }`  
`[<f,g>, <h,i>] . p?`  
`= { Lei (30) }`  
`p -> <f,g>, <h,i>`

##

provar F4
`<f, (p → g, h)> = p → <f, g>, <f, h> (F4)`

`p -> <f,g>, <f,h>`  
`= { Lei (30) }`  
`[<f,g>,<f,h>]. p?`  
`= { Lei (28) }`  
`<[f,f], [g,h]> . p?`  
`= { Lei (9) }`  
`<[f,f] . p?, [g,h] . p?>`  
`= { Lei (F1) e lei (30) }`  
`<f, p -> g,h>`


### <a id="ex3"></a>Exercicio 3

O exercício 3 é semelhante ao exercício 1 da ficha nº3: temos que **derivar/obter** um programa (out) a partir de um conjunto de condições. Neste caso a única condição é que out . in = id. Notem a  
beleza e rigor disto: estamos a **calcular** um programa que nós desejamos que cumpra certas condições; de forma semelhante ao engenheiro civil que **calcula** o cimento que vai ser necessário para construir uma ponte.

Resolução:

`out . in = id`  
`= { Definição in }`  
`out . [0̲, succ] = id`  
`= { Lei fusão-+ }`  
`[out . 0̲, out. succ] = id`  
`= { Lei universal-+ }`  
`out . 0̲ = i1`  
`out . succ = i2`  
`= { Igualdade extensional}`  
`out . 0̲ () = i1 ()`  
`out . succ n = i2 n`  
`= { Definição 0̲, definição succ }`  
`out 0 = i1 ()`  
`out (n+1) = i2 n`

### <a id="ex4a"></a>Exercicio 4

Vamos então ao exercício 4, que incide sobre as operações curry e uncurry. Como já falado nas teóricas, estas operações permitem-nos transformar um programa de dois argumentos num programa de um só  
argumento e vice-versa. Estas funções estão, por exemplo, por detrás da elegância do Haskell (se quiserem saber mais detalhes sobre este último facto pm me).

Das aulas teóricas, sabemos que quando aplicamos a operação curry a um programa f : A x B -> C de dois argumentos obtemos um programa (curry f) : A -> C^B que dado um elemento do tipo A devolve-nos uma programa  
do tipo B -> C. Podemos experimentar isso por exemplo em Haskell, e é isso que vos convido a fazer agora.

Quem tiver o ghci pode escrever: `mysum (x,y) = x + y`

Esta função vai ter dois argumentos, facto que vocês podem verificar pedindo ao ghci para nos dar o tipo de mysum:

`> Prelude> :t mysum`  
`> mysum :: Num a => (a, a) -> a`

E claro podem testa-la

`> Prelude> mysum (2,3)`  
`> 5`

Ao usar a operação curry sobre o mysum obtemos:

`> Prelude> :t (curry mysum)`  
`> (curry mysum) :: Num c => c -> (c -> c)`

i.e. uma função que dado um número x devolve-nos a função (x+). Por sua vez, quando a função (x+) recebe um número y ela devolve x+y.

Podemos testar isto fazendo por ex.

`> Prelude> ((curry mysum) 2) 3`  
`> 5`

A função `curry mysum` é igual a qual função em Haskell ? 
(+)
Podem experimentar fazendo: `(+) 2 3`
vai dar o mesmo resultado que `curry mysum 2 3`
e a função `uncurry (+)` é igual a qual função ?
volta a ser `mysum`
Portanto vamos obter que `uncurry (curry mysum) = mysum`
O que sugere que uncurry e curry são inversas uma da outra, e de facto é isso que acontece

### a)
O objectivo é começarem com `f k = ap . (k ⨯ id)` e chegarem a `(f k) (a,b) = k a b` , em que este último passo é precisamente a definição da função uncurry.

`f k = ap . (k ⨯ id)`  
`≡ { Igualdade extensional (adição de variáveis) }`  
`(f k) (a,b) = ap . (k ⨯ id) (a,b)`  
`≡ { def-comp, def-x, def-id}`  
`(f k) (a,b) = ap (k a, b)`  
`≡ { def-ap }`  
`(f k) (a,b) = k a b`

Para esclarecer: no fim, trocando o símbolo f por uncurry e o símbolo k por f, obtemos:

`(uncurry f) (a,b) = f a b`



