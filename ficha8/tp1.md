  

# ficha 8

  

## Resoluções por Olga Pacheco

  
  

### Index

-  [Exercicio 1](#ex1)
- [Exercicio 2](#ex2)
- [Exercicio 3](#ex3)
- [Exercicio 4](#ex4)
- [Exercicio 5](#ex5)



### <a id="ex1"></a> Exercicio 1

Um bifunctor B é um functor binário

    f: A -> D
    g: C -> E

`B(f,g): B(A,C) -> B(D,E)`  tal que : `B(id,id)) = id e B(f.g , h.k) = B(f,h) . B(g,k)`

Queremos provar que:

`B(X,Y ) = X + Y e B(X,Y ) = X + Y x Y` são bifunctores

Comecemos por:

`B(X,Y ) = X + Y`

Temos então de provar que: `B(id,id)) = id e B(f.g , h.k) = B(f,h) . B(g,k)` para este caso

Ora:

    B(id,id)
    = {def. deste bifunctor }

como fica?

    B(id,id)
    = {def. do bifunctor }
    id + id
    ={26}
    id

Temos agora que provar: `B(f.g , h.k) = B(f,h) . B(g,k)`

    B(f.g , h.k)
    = {def. do bifunctor}
    f.g + h.k x h.k
    = {14}
    f.g + (h x h) . (k x k)
    = {25}
    (f + h x h) . (g + k x k)
    = {def do bifunctor}
    B(f,h) . B(g,k)


### <a id="ex2"></a> Exercicio 2

Analise o diagrama genérico de um catamorfismo de gene g sobre o tipo paramétrico `T X =B (X,T X)` cuja base é o `bifunctor B`

Relembre a propriedade universal dos catamorfismos reescrita usando o bifunctor base `B:k=(| g |) <=> k .in = g . B(id,k)` (note que: `F k = B(id,k)` )

Relembre a definição genérica de map associado ao tipo T (lei 48): `T f = (| in . B(f,id) |)`

Queremos provar que o map de sequências finitas (listas) é a função: 

    f* [] = []
    f* (h:t) = f h : f* t

(nota: map f = f* para listas)

Para listas temos: i`n=[nil,cons]` e `B(f,g)=id + f x g`

Vamos partir então da definição genérica de `map` como catamorfismo (48)

    T f = (| in . B(f,id) |)
    <=> {instância para listas: def in e B(f,id)=id + f x id}
    f* = (| [nil,cons].(id + f x id) |)
    <=> {22}
    f* = (| [nil, cons.(f x id)] |)
    <=> {43}
    f* . in = [nil, cons.(f x id)] . B(id, f*)
    <=> {def in, def. B(id, f*) }
    f* . [nil, cons] = [nil, cons.(f x id)] . (id + id x f*)
    <=> { 20, 22, 1}
    [f*.nil, f*.cons] = [nil, cons.(f x id).(id x f*)]
    <=> {27, 14, 1}
    f*.nil = nil
    f*.cons = cons . (f x f*)
    <=> {69, 70, def nil, 75}
    f* [] =[]
    f*.cons (h,t) = cons (f h, f* t)
    <=> {def cons}
    f* [] =[]
    f* (h:t) = f h : f* t QED



### <a id="ex3"></a> Exercicio 3


Estamos com `LTree: data LTree a = Leaf a | Fork (LTree a, LTree a)`

`T X = LTree Xin = [Leaf, Fork]`
`B(X,Y) = X + Y x Y e B(f,g) = f + g x g`

vamos usar a função depth definida como catamorfismo

`depth = (| [one, succ . umax] |)`
para: `one=(const 1)` e `umax (a,b) = max a b`

Queremos provar, usando absorção-cata (49) : `depth . LTree f = depth`

ou seja, a profundidade de uma árvore não é alterada quando aplicamos uma função f a todas as suas folhas.

Note que `LTree f `é o `map para LTree`

queremos partir de `depth . LTree f` para chegar a `depth`

    depth . LTree f
    = {def. depth}
    (| [one, succ . umax] |) . LTree f
    = {49}
    (| [one, succ . umax] . B(f,id) |)
    = {def B(f,id) para LTree}
    (| [one, succ . umax] . (f + id x id) |)
    = {22, 15, 1}
    (| [one.f, succ.umax] |)
    = {3}
    (| [one, succ . umax] |)
    ={def. depth}
    depth




### <a id="ex4"></a> Exercicio 4

Relembre a função

    unzip: [(a,b)] -> ([a],[b])
    unzip xs = (map p1 xs, map p2 xs)

pega numa lista de pares e gera um par de listas com a primeira e a segunda componente a versão de unzip que efectua o cálculo numa única travessia da lista: `unzip [ ] = ([ ], [ ])`

    unzip ((a, b) : xs) = (a:as, b:bs)
    	where (as, bs) = unzip xs (edited)

Queremos derivar a segunda versão a partir da primeira usando a lei banana-split (51): 

`< (|i|) , (|j|) > = (| (i x j).<F  p1,  F  p2> |)`

note que por (11) é equivalente a:

`< (|i|) , (|j|) > = (| <i  .  F  p1,  j  .  F  p2> |)`

Então a prova

    unzip xs = (map p1 xs, map p2 xs)
    <=> {74, 69}
    unzip = < map p1 , map p2 >
    <=> {48}
    unzip = < (|in.B(p1,id)|), (|in.B(p2,id)|)) >
    <=> { 51,11}
    unzip = (|<in  .  B(p1,id)  .  F  p1  ,  in  .  B(p2,id)  .  F  p2 >|)
    <=> {F k = B(id,k)} *
    unzip = (|<in  .  B(p1,id)  .  B(id,p1)  ,  in  .  B(p2,id)  .  B(id,p2) >|)
    <=> {def. bifunctor, 1}
    unzip = (|<in  .  B(p1,p1)  ,  in  .  B(p2,p2) >|)
    <=> {para listas temos: B(f,g) = id + f x g e in=[nil.cons]}
    unzip = (| < [nil,cons].(id + p1xp1) , [nil,cons].(id + p2xp2) > |)
    <=> {22,1}
    unzip = (| < [nil,cons. (p1xp1)] , [nil,cons.(p2xp2)] > |)
    <=> {43}
    unzip . in =< [nil,cons. (p1xp1)] , [nil,cons.(p2xp2)] > . B(id,unzip)
    <=> {def in, def B(id,unzip) para listas
    unzip.[nil,cons] = < [nil,cons. (p1xp1)] , [nil,cons.(p2xp2) >.(id + id x unzip)
    <=> {20, 28}
    [unzip . nil, unzip. cons] = [<nil,nil>, <cons.(  p1xp1),  cons.(p2xp2) >] . (id + id x unzip)
    <=> { 22,27,11,1}
    unzip . nil= <nil,nil>
    unzip. cons = (cons x cons).< p1xp1, p2xp2>.(id x unzip)
    <=> { 69, 70, def. nil, 75, 71}
    unzip [] = ([],[])
    unzip ((a,b):t) = (cons x cons).< (p1xp1), (p2xp2)> ((a,b), unzip t)
    <=> {seja (as,bs)=unzip t}
    unzip [] = ([],[])
    unzip ((a,b):t) = (cons x cons).< (p1xp1), (p2xp2)> ((a,b), (as,bs))
    <=> {70,74}
    unzip [] = ([],[])
    unzip ((a,b):t) = (cons x cons) ((p1xp1) ((a,b), (as,bs)) , (p2xp2) ((a,b), (as,bs)) )
    <=> {75}
    unzip [] = ([],[])
    unzip ((a,b):t) = (cons x cons) ( (p1 (a,b), p1 (as,bs)) , (p2 (a,b), p2 (as,bs)) )
    <=> {77}
    unzip [] = ([],[])
    unzip ((a,b):t) = (cons x cons) ((a, as) , (b,bs))
    <=> {75}
    unzip [] = ([],[])
    unzip ((a,b):t) = (cons (a, as) , cons (b,bs))
    <=> {def cons}
    unzip [] = ([],[])
    unzip ((a,b):t) = ((a:as) , (b:bs)) where (as,bs) = unzip t QED


### <a id="ex5"></a> Exercicio 5


Considere a seguinte função que calcula a média de uma lista não vazia: `average = ratio . <sum,  length>` onde ratio `(n,d)=n/d`

Usando a lei "banana-split" queremos derivar uma versão de average que calcule a média numa única travessia: 

    average l = x/y where
	    (x,y)= aux l
	    aux [] = (0,0)
	    aux (h:t) = (h+x, y+1) 
		    where (x,y) = aux t

repare que `average = ratio.aux`

Relembre a definição de somatório de uma lista como catamorfismo: `sum=(| [zero, add] |)` e de comprimento de uma lista como catamorfismo: `length = (| [zero, succ.p2] |)` sendo: `zero=(const 0)` e `add=uncurry (+)`

Partindo então de `aux=<sum,length>` queremos chegar à versão recursiva acima apresentada.

    aux=<sum,length>
    <=> {def. sum e length }
    aux=< (| [zero, add] |) , (| [zero, succ.p2] |) >
    <=> {51, 11}
    aux = (| <[zero, add] . F p1 , [zero, succ.p2] . F p2> |)
    <=> {F k = id+id x k}
    aux = (| <[zero, add] . (id + id x p1) , [zero, succ.p2] . (id + id x p2)> |)
    <=> {22, 1}
    aux = (| <[zero, add.(id x p1)] , [zero, succ.p2.(id x p2)]> |)
    <=> {13}
    aux = (| <[zero, add.(id x p1)] , [zero, succ.p2.p2]> |)
    <=> {28}
    aux = (| [<zero,  zero>, <add.(id  x  p1)  ,succ.p2.p2>] |)
    <=> {43}
    aux.in = [<zero,  zero>, <add.(id  x  p1)  ,  succ.p2.p2>] . (id + id x aux)
    <=> {def in, 20, 22, 1}
    [aux.nil, aux.cons] = [<zero,  zero>, <add.(id  x  p1)  ,  succ.p2.p2>.(id x aux)]
    <=> {27}
    aux.nil = <zero,  zero>
    aux.cons = <add.(id  x  p1)  ,  succ.p2.p2>.(id x aux)
    <=> {69, 70, 75, def nil, def zero, 74, 71 }
    aux [] = (0,0)
    aux (cons (h,t)) = <add.(id  x  p1)  ,  succ.p.p2> (h, aux t)
    <=> {seja (x,y)= aux t}
    aux [] = (0,0)
    aux (cons (h,t)) = <add.(id  x  p1)  ,  succ.p2.p2> (h, (x,y))
    <=> {74, def cons}
    aux [] = (0,0)
    aux (h:t) = ( add.(id x p1) (h,(x,y)) , succ.p2.p2 (h, (x,y)) )
    <=> {70, 77, 75 }
    aux [] = (0,0)
    aux (h:t) = ( add (h, x) , succ y )
    <=> def add e def succ}
    aux [] = (0,0)
    aux (h:t) = ( h+ x) , y+1 ) where (x,y)=aux t QED


