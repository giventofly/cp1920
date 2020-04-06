
# ficha 7

## Resoluções por Olga Pacheco


### Index

-  [Exercicio 1](#ex1)
-  [Exercicio 3](#ex3)

  

### <a id="ex1"></a> Exercicio 1

 
Queremos provar a propriedadef.

    (for f i)= for f (f i)

Agora estamos no contexto dos naturais:

    F k = id + k

 
Vamos substituir os for por catamorfismos:

    (for f i)=?
    for f (f i)= ?

como escrever?
  

    (for f i)=(| [(const i), f] |)

e

> for f (f i)= (| [(const (f i)),f] |)

  

Então

  

    f. (| [(const i), f] |) = (| [(const (f i)),f] |)    
    <= {46}    
    f. [(const i), f] = [(const (f i)),f] . (id + f)    
    <=>{20,22,1}    
    [f.(const i), f.f] = [(const (f i)),f.f]    
    <=>{27}    
    f.(const i)= (const (f i))    
    f.f=f.f    
    <=>{4}    
    (const (f i))=(const (f i))    
    true    
    <=>    
    true

  
  

### <a id="ex3"></a> Exercicio 3

  

    impar 0 = False    
    impar (n+1)= par nepar 0 = True    
    par (n+1) = impar n

  

queremos provar que estas duas definições são equivalentes a:

    impar . in = h . F<impar,par>    
    par . in = k . F<impar,par>

`in=[zero,succ]` e `F k= id + k` , porque estamos no contexto dos naturais

  

Queremos então provar:

  
    impar . [zero,succ] = h . (id +<impar,par>)    
    par . [zero,succ] = k . (id + <impar,par>)

  

Então

  

    impar 0 = False    
    impar (n+1)= par n    
    <=>{ def. zero, def succ, 70,69 }    
    impar.zero = (const False)    
    impar.succ = par    
    <=> { 7}    
    impar.zero = (const False)    
    impar.succ = p2.<impar,par>    
    <=> {27,20,1}    
    impar.[zero,succ]=[(const False).id, p2.<impar,par>]    
    <=> {def in, 22}    
    impar.in=[(const False), p2].(id+<impar,par>)    
    <=> {F k = id+k}    
    impar.in=[(const False), p2]. F<impar,par>

  

qual o h?

    h = [(const False), p2]

  
Vamos fazer o mesmo para par para encontrar o k

 
O objectivo é chegar a :


    par.in=k. F<impar,par>

  

O cálculo é semelhante ao anterior:

    par 0 = True
    par (n+1) = impar n    
    <=>{def. zero, def succ, 70,69}    
    par.zero =(const True)    
    par.succ = impar    
    <=> {7}    
    par.zero =(const True)    
    par.succ = p1.<impar,par>    
    <=>{27,20,1}    
    par.[zero,succ]=[(const True).id, p1.<impar,par>]    
    <=> {def. in, 22}    
    par.in=[(const True), p1].(id + <impar,par>)    
    <=>{F k = id + k}    
    par.in=[(const True), p1] . F<impar,par>

  
Temos então:

    impar.in=[(const False), p2]. F<impar,par>    
    par.in=[(const True), p1] . F<impar,par>

Queremos agora definir <impar,par> como um for


relembre que `for b i = (| [(const i),b] |)`


    impar.in=[(const False), p2]. F<impar,par>    
    par.in=[(const True), p1] . F<impar,par>    
    <=> {50}    
    <impar,par>=(| <[(const False), p2],[(const True), p1] > |)    
    <=>{28 }    
    <impar,par>=(| [<(const False), (const True)>, < p2, p1>] |)    
    <=> {def. swap }    
    <impar,par>=(| [(const (False, True)), swap] |)

logo:

    <impar,par> = for swap (False, True)



### <a id="ex9"></a> Exercicio 9


Estamos no contexto das LTree:

    data LTree a = Leaf a | Fork (LTree a, LTree a)    
    F X = A + X x X    
    F f = id + f x f

  

    Leaf: A -> LTree A    
    Fork: LTree A x LTree A -> LTree Ain=[Leaf,Fork]

  

a funçãomirror: `LTree A -> LTree A`

    mirror (Leaf x) = (Leaf x)    
    mirror (Fork (e,d)) = Fork (mirror d, mirror e)

  

pode ser definida como um catamorfismo de LTree:

    mirror = (|in.(id+swap)|)


Então

  

    mirror.mirror = id    
    <=> { def mirror, 45 }    
    mirror.(|in.(id+swap)|) = (|in|)    
    <= {46}    
    mirror.in.(id+swap) = in.(id+(mirror x mirror))    
    <=> {def. mirror}    
    (|in.(id+swap)|).in.(id+swap) = in.(id+(mirror x mirror))    
    <=>{44}    
    in.(id+swap).(id+(mirror x mirror)).(id+swap) = in.(id+(mirror x mirror))    
    <=>{25,1}    
    in.(id+swap.(mirror x mirror).swap)=in.(id+(mirror x mirror))    
    <=>{natural swap:(fxg).swap = swap.(gxf) }    
    in.(id+swap.swap.(mirrorxmirror)) = in.(id+(mirror x mirror))    
    <=> {swap.swap=id, 1}    
    in. ((id+(mirror x mirror))= in. (id+(mirror x mirror)    
    <=>    
    true


