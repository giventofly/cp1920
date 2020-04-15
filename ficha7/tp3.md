
# ficha 7

## Resoluções por Renato Neves


### Index

-  [Exercicio 1](#ex1)
-  [Exercicio 3](#ex3)
-  [Exercicio 9](#ex9)

  

### <a id="ex1"></a> Exercicio 1

A ideia é também provar uma propriedade de um catamorfismo, neste caso `(for f i)`. Relembrem que `(for f i)` é uma função recursiva que aplica a  função `f` n-vezes a _`i`_, em que n é o número que damos como argumento a `(for f i)`.

Neste caso a equação que queremos provar diz que: aplicar a função `f (n+1`)-vezes a `i` é a mesma coisa que aplicar a função `f` n-vezes a `f i`.

Para este exercício, teremos que tirar partido do functor associado aos números naturais e à lei da fusão-cata.

`f . (for f i) = for f (f i)`  
`≡ { Definiçao 'for f i' e 'for f (f i)'}`  
`f . ⦇ [i̲, f] ⦈ = ⦇ [f̲ ̲i̲, f] ⦈`  
`<= { Lei fusão-cata, functor dos Naturais }`  
`f . [i̲, f] = [f̲ ̲i̲, f] . (id + f)`  
`≡ { Lei fusão-+, absorpção-+}`  
`[f . i̲, f . f] = [f̲ ̲i̲, f . f]`  
`≡ { Fusão-constante}`  
`[f̲ ̲i̲, f . f] = [f̲ ̲i̲, f . f]`  
`≡`  
`True`


### <a id="ex3"></a> Exercicio 3

O exercício 3 apresenta funções **mutuamente recursivas** i.e. funções que se chamam uma à outra (relembrem que uma função **recursiva** é uma função que se chama a ela própria).

O objectivo do exercício é mostrar que funções **mutuamente recursivas** também podem ser capturadas na forma de um catamorfismo. E para tal, é bastante útil usar a lei de Fokkinga.


O exercício procede em duas partes: primeiro temos que converter as definições de 'impar' e 'par' no sistema de equações

    impar . in = h . F <impar,par>  
    par . in = k . F <impar,par>

para um dado h e k, e em que F é o functor dos números naturais. Isto vai-nos permitir aplicar a lei de Fokkinga para obter <impar,par> na forma de um catamorfismo. A segunda parte, é simplificar este catamorfismo usando as leis usuais de cálculo de programas.

O processo de converter funções mutuamente recursivas (sejam elas sobre números naturais, listas, ou árvores) vai ser sempre análogo ao processo que acabei de descrever.

Então para este exercício específico, temos que chegar ao sistema,  

    impar . in = h . F <impar,par>  
    par . in = k . F <impar,par>

1a)

`impar 0 = False`  
`impar (n+1) = par n`  
`≡ { Definição composição, Definição 0̲, F̲a̲l̲s̲e̲, e succ.}`  
`impar . 0̲ x = F̲a̲l̲s̲e̲ (x)`  
`impar . succ n = par n`  
`≡ { Igualdade extensional}`  
`impar . 0̲ = F̲a̲l̲s̲e̲`  
`impar . succ = par`  
`≡ { Lei Eq-+}`  
`[impar . 0̲, impar . succ] = [F̲a̲l̲s̲e̲, par]`  
`≡ { Lei Fusão-+ }`  
`impar . [0̲,succ] = [F̲a̲l̲s̲e̲, par]`  
`≡ { Definição in}`  
`impar . in = [F̲a̲l̲s̲e̲, par]`  
`≡ { Lei cancelamento-x}`  
`impar . in = [F̲a̲l̲s̲e̲, p2 . <impar,par>]`  
`≡ { Lei natural-id, lei absorpção-+}`  
`impar . in = [F̲a̲l̲s̲e̲, p2] . (id + <impar,par>)`

1b)

`par 0 = True`  
`par (n+1) = impar n`  
`≡ { Definição composição, Definição 0̲, T̲r̲u̲e̲, e succ.}`  
`par . 0̲ x = T̲r̲u̲e̲ (x)`  
`par . succ n = impar n`  
`≡ { Igualdade extensional}`  
`par . 0̲ = T̲r̲u̲e̲`  
`par . succ = impar`  
`≡ { Lei Eq-+}`  
`[par . 0̲, par . succ] = [T̲r̲u̲e̲, impar]`  
`≡ { Lei Fusão-+ }`  
`par . [0̲,succ] = [T̲r̲u̲e̲, impar]`  
`≡ { Definição in}`  
`par . in = [T̲r̲u̲e̲, impar]`  
`≡ { Lei cancelamento-x}`  
`par . in = [T̲r̲u̲e̲, p1 . <impar,par>]`  
`≡ { Lei natural-id, absorpção-+}`  
`par . in = [T̲r̲u̲e̲, p1] . (id + <impar,par>)`

Portanto, conseguimos chegar ao sistema de equações pretendido, nomeadamente:

`impar . in = [F̲a̲l̲s̲e̲, p2] . (id + <impar,par>)`  
`par . in = [T̲r̲u̲e̲, p1] . (id + <impar,par>)`

com base em 1a. e 1b.

Agora temos que efectuar o **2º passo usando a lei de Fokkinga**

`impar . in = [F̲a̲l̲s̲e̲, p2] . (id + <impar,par>)`  
`par . in = [T̲r̲u̲e̲, p1] . (id + <impar,par>)`  
`≡ { Fokkinga }`  
`<impar,par> = ⦇ <[F̲a̲l̲s̲e̲, p2],[T̲r̲u̲e̲, p1]> ⦈`

e agora podemos simplificar a equação resultante:

`<impar,par> = ⦇ <[F̲a̲l̲s̲e̲, p2],[T̲r̲u̲e̲, p1]> ⦈`  
`≡ { Lei da troca }`  
`<impar,par> = ⦇ [<F̲a̲l̲s̲e̲,T̲r̲u̲e̲>, <p2,p1>] ⦈`  
`≡ { Definição swap, definição constante }`  
`<impar,par> = ⦇ [(̲F̲a̲l̲s̲e̲,̲T̲r̲u̲e̲)̲, sw] ⦈`  
`≡ { Definição for }`  
`for sw (False,True)`


### <a id="ex9"></a> Exercicio 9


O objectivo é provarmos que espelhar uma árvore duas vezes é equivalente a fazer nada.

Este exercício **procede de forma análoga** aos anteriores. Só que agora em vez de listas e números naturais, iremos trabalhar com a estrutura algébrica (tipo de dados) 'Leaf trees'. Como vamos proceder de forma  
análoga aos exercícios anteriores, convém então relembrar a definição do functor associado às 'Leaf trees': F f = id + f^2.  
Lembrem-se também que teremos que usar a lei fusão-cata.

`mirror . mirror = id`  
`≡ { Definição mirror, reflexão-cata}`  
`mirror . ⦇ in . (id + sw) ⦈ = ⦇ in ⦈`  
`<= { Fusão-cata, functor das Leaf trees }`  
`mirror . in . (id + sw) = in . (id + mirror^2)`  
`≡ { Definição in }`  
`mirror . [Leaf,Fork] . (id + sw) = [Leaf,Fork] . (id + mirror^2)`  
`≡ { Definição Absorpção-+ }`  
`mirror . [Leaf,Fork . sw] = [Leaf,Fork . mirror^2]`  
`≡ { Definição Fusão-+ }`  
`[mirror . Leaf, mirror . Fork . sw] = [Leaf,Fork . mirror^2]`  
`≡ { Lei Eq-+ }`  
`mirror . Leaf = Leaf`  
`mirror . Fork . sw = Fork . mirror^2`  
`≡ { Lei isomorfismos }`  
`mirror . Leaf = Leaf`  
`mirror . Fork . sw . sw = Fork . mirror^2 . sw`  
`≡ { sw . sw = id }`  
`mirror . Leaf = Leaf`  
`mirror . Fork = Fork . mirror^2 . sw`  
`≡ { Igualdade extensional }`  
`mirror (Leaf a) = Leaf a`  
`mirror (Fork (x,y)) = Fork . mirror^2 (y,x)`  
`≡ { Lei composição }`  
`mirror (Leaf a) = Leaf a`  
`mirror (Fork (x,y)) = Fork (mirror y, mirror x)`  
`≡ { Definição mirror }`  
`True`



