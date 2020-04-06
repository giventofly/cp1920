
# ficha 6

## Resoluções por Olga Pacheco

### Index

-  [Exercicio 2d e 4](#ex2d4)
-  [Exercicio 5](#ex5)

  

### <a id="ex2d4"></a> Exercicio 2d e 4

  

Relembre árvores de expressão:data Expr v o = Var v | Op (o,[Expr v o])

    T = Expr V O
    F X = V + O x X*
    F f = id + id x map f
    Var: V -> Expr V OOp: O x (Expr V O)* -> Expr V Oin=[Var, Op]

  

![](https://github.com/giventofly/cp1920/blob/master/ficha6/f62d.png)


qual o tipo do gene g?

      g: V + O x (V*)* -> V*
    

      g (i1 v) =?
        g (i2 (o,llv)) = ?

g.i1 recebe uma variável e tem de a transformar numa lista.
g.i2 recebe um par (o,llv) em que o é um valor do tipo O e llv é um valor do tipo lista de listas de variáveis (uma lista de variáveis por cada subexpressão - note que (V*)* é o resultado do map vars aplicado a um valor do tipo `(Expr V O)*)`.

  

Nós queremos pegar apenas na 2.a componente do par e transformar a lista de listas de variáveis numa lista de variáveis.

  

sugestões para g?

  

    g: V + O x (V*)* -> V*g (i1 v) = [v]
    
    g (i2 (o,llv)) = concat llv

  

e em pointfree?

    g=[singl, concat.p2]parasingl:: a -> [a]
    singl x =[x]

  

Então

  

    vars=(| [singl, concat.p2] |)
    <=> {43}   
    vars.in=[singl, concat.p2].(id + id x map vars)    
    <=> {def in, 20, 22,1}    
    [vars.Var,vars.Op]=[singl,concat.p2.(id x map vars)]    
    <=>{27, 13}    
    vars.Var = singl    
    vars.Op=concat.(map vars).p2    
    <=> { 69,70}    
    vars (Var v) = singl v    
    vars (Op (o,le)) = concat ((map vars) (p2 (o,le)))    
    <=> {def. singl, 77}    
    vars (Var v) = [v]    
    vars (Op (o,le)) = concat (map vars le)

  

### <a id="ex5"></a> Exercicio 5

  

    sumprod :: a -> [a] -> a (ignorando restrições de tipo)    
    sumprod a [ ] = 0    
    sumprod a (h : t) = a*h + sumprod a t

  
definida como o catamorfismo de listas:

  

    sumprod a = (| [zero, add.((a*) x id)] |)zero _ = 0
    add (x,y)=x+y

  

Queremos provar:

    sumprod a = (a*).sum

usando fusão-cata (46)
    
    (a*).sum = sumprod a    
    <=> {def. sum, def. sumprod a}    
    (a*).(| [zero, add] |)= (| [zero, add.((a*) x id)] |)    
    <= {46}    
    (a*). [zero, add]= [zero, add.((a*) x id)].(id + id x (a*))    
    <=> { 20, 22, 1}    
    [(a*).zero, (a*).add]=[zero,add.((a*) x id).(id x (a*))]    
    <=> { 27, 14}    
    (a*).zero=zero    
    (a*).add=add.((a*)x(a*))    
    <=> { 69}    
    (a*).zero x =zero x    
    (a*).add (y,z)=add.((a*)x(a*)) (y,z)    
    <=> {70, 75, def zero, def add}    
    a* 0 =0    
    a*(y+z)=a*y+a*z    
    <=>
    true - prop. elemento absorvente da multiplicação    
    true - prop. distributividade da multiplicação em relação à adição

