  

# ficha 10


## Resoluções por Renato Neves


### Index

-  [Exercicio 2](#ex2)
-  [Exercicio 3](#ex3)
-  [Exercicio 4](#ex4)

### <a id="ex2"></a> Exercicio 2

Eu disse anteriormente que alguns catamorfismos também pode ser escritos como anamorfismos, e é precisamente isso que o exercício mostra. Em particular isto é verdade para a famosa função length. Notem que, no entanto, o anamorfismo que obtemos é uma anamorfismo de **números naturais** e não um anamorfismo de listas.

A resolução deve começar por remover as "bananas" usando a lei universal-cata. Isto permite-nos "descompactar" a definição de length como cata e depois trabalhar com a versão descompactada. De seguida  temos que trabalhar a versão descompactada até esta ter uma forma que nos permita introduzir as "sananab" ( ou "lentes" [( - )] ) via a lei universal-+. 

Notem também que aqui teremos que trabalhar com duas variantes de in/out. Nomeadamente in/out para números naturais e in/out para listas. A razão é que o ponto de partida é um catamorfismo de **listas**, e o ponto de chegada é um anamorfismo de **naturais**.

`length = ⦇ [zero, succ . p2] ⦈`  

`≡ { Lei universal-cata }`  
`length . in = [zero, succ . p2] . (id + id x length)`  

`≡ { Lei isomorfismo in/out }`  
`length = [zero, succ . p2] . (id + id x length) . out`  

`≡ { Lei absorpção-+ }`  
`length = [zero, succ] . (id + p2) . (id + id x length) . out`  

`≡ { Definição "in" Naturais }`  
`length = in . (id + p2) . (id + id x length) . out`  

`≡ { Lei isomorfismo in/out }`  
`out . length = (id + p2) . (id + id x length) . out`  

`≡ { Lei Functor-+ }`  
`out . length = (id + (p2 . (id x length))) . out`  

`≡ { Lei Natural-p2 }`  
`out . length = (id + (length . p2)) . out`  

`≡ { Lei Functor-+ }`  
`out . length = (id + length) . (id + p2) . out`  

`≡ { Lei Universal-ana }`  
`length = [( (id + p2) . out )]`

Reparem que conseguimos escrever `length` como um catamorfismo e como um anamorfismo !
  
### <a id="ex3"></a> Exercicio 3

O objectivo do exercício é muito semelhante ao anterior: pegar na definição de `suffixes` como um anamorfismo, e converte-la para uma definição a la Haskell. 

`suffixes = [( id + <cons,p2> ) . out )]`  

`≡ { Lei universal-ana }`  
`out . suffixes = (F suffixes) . (id + <cons,p2>) . out`  

`≡ { Lei isomorfismos in/out }`  
`suffixes = in . (F suffixes) . (id + <cons,p2>) . out`  

`≡ { Lei isomorfismos in/out }`  
`suffixes . in = in . (F suffixes) . (id + <cons,p2>)`  

`≡ { Definição functor-F }`  
`suffixes . in = in . (id + (id x suffixes)) . (id + <cons,p2>)`  

`≡ { Definição in }`  
`suffixes . [nil,cons] = [nil,cons] . (id + (id x suffixes)) . (id + <cons,p2>)`  

`≡ { Definição fusão-+ }`  
`[suffixes . nil, suffixes . cons] = [nil,cons] . (id + (id x suffixes)) . (id + <cons,p2>)`  

`≡ { Definição fusão-+ }`  
`[suffixes . nil, suffixes . cons] = [nil,cons . (id x suffixes)] . (id + <cons,p2>)`  

`≡ { Definição absorpção-+ }`  
`[suffixes . nil, suffixes . cons] = [nil,cons . (id x suffixes) . <cons,p2>]`  

`≡ { Lei Eq-+ }`  
`suffixes . nil = nil`  
`suffixes . cons = cons . (id x suffixes) . <cons,p2>`  

`≡ { Lei Fusão-x }`  
`suffixes . nil = nil`  
`suffixes . cons = cons . <cons, suffixes . p2>`  

`≡ { Igualdade extensional, definição composição }`  
`suffixes [] = []`  
`suffixes (h:t) = (h:t) : (suffixes t)`



### <a id="ex4"></a> Exercicio 4

O primeiro objectivo é: pegar numa definição a la Haskell de uma função recursiva, e converte-la para uma definição na forma de um anamorfismo. Notem que em exercícios anteriores fizemos o inverso, i.e. começamos com uma definição na forma de um anamorfismo e convertemo-la ("descompactamo-la") para uma definição a la Haskell.

`mirror (Leaf x) = Leaf x`  
`mirror (Fork (x,y)) = Fork (mirror y, mirror x)`  

`≡ { Igualdade extensional, definição composição }`  
`mirror . Leaf = Leaf`  
`mirror . Fork = Fork . (mirror x mirror) . swap`  

`≡ { Lei eq-+ }`  
`[mirror . Leaf, mirror . Fork] = [Leaf, Fork . (mirror x mirror) . swap]`  

`≡ { Lei fusão-+ }`  
`mirror . [Leaf, Fork] = [Leaf, Fork . (mirror x mirror) . swap]`  

`≡ { Lei absorpção-+ }`  
`mirror . [Leaf, Fork] = [Leaf, Fork] . (id + (mirror x mirror) . swap)`  

`≡ { Definição in-LTree }`  
`mirror . in = in . (id + (mirror x mirror) . swap)`  

`≡ { Lei functor-+ }`  
`mirror . in = in . (id + (mirror x mirror)) . (id + swap)`  

`≡ { Lei isomorfismos in/out }`  
`out . mirror = (id + (mirror x mirror)) . (id + swap) . out`  

`≡ { Lei universal-ana }`  
`mirror = [( (id + swap) . out )]`

Finalmente, na segunda parte do exercício temos que provar que mirror . mirror = id. Para provarmos isto, é bastante útil tiramos partido das leis existentes dos anamorfismos, e é precisamente isso que iremos fazer. 

Tal como nos exercícios anteriores é bastante importante tirar partido das lei dos isomorfismos. Para além disso teremos que tirar partido da lei "Fusão-ana". Esta lei permite provar certas equações que envolvem  anamorfismos com base em assunções mais simples. Notem que no nosso caso nós queremos provar que

`mirror . mirror = id`e isto é de facto uma equação que envolve anamorfismos.

`mirror . mirror = id`  

`≡ { Definição mirror e reflexão-ana }`  
`[( (id + sw) . out )] . mirror = [( out )]`  
`<= { Lei fusão-ana }`  
`(id + sw) . out . mirror = (id + (mirror x mirror)) . out`  

`≡ { Lei isomorfismos in/out }`  
`(id + sw) . out . mirror . in = (id + (mirror x mirror))`  

`≡ { Lei isomorfismos in/out }`  
`out . mirror . in = (id + (mirror x mirror)) . (id + sw)`  

`≡ { Lei isomorfismos in/out }`  
`mirror . in = in . (id + (mirror x mirror)) . (id + sw)`  

`≡ { Lei Functor-+ }`  
`mirror . in = in . (id + (mirror x mirror) . sw)`  

`≡ { Definição in }`  
`mirror . [Leaf, Fork] = [Leaf, Fork] . (id + (mirror x mirror) . sw)`  

`≡ { Ver primeira parte do exercício}`  

`True` 

A resolução baseia-se na primeira parte do exercício, em que já sabiamos que

`mirror . [Leaf, Fork] = [Leaf, Fork] . (id + (mirror x mirror) . sw)`




  
  
