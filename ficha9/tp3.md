  

# ficha 9

  

## Resoluções por JNO

  
 
### Index

-  [Exercicio 1](#ex1)
- [Exercicio 2](#ex2)
- [Exercicio 3](#ex3)
- [Exercicio 4](#ex4)



### <a id="ex1"></a> Exercicio 1


|T   | Descr.     | in  |  B(g,f)  | B(X,Y) | F f   | T f 
|--|--| --|--|--|--|--
|  BTree A | Arv. bin. de A  |  [empty, Node] | id+gxf² |1+XxY² |  id+idxf² |⦇in.id+fxid⦈   
| LTree A| Arv.bin.(folhas)  |[Leaf,Fork]   |g+f² |  X+Y² | id+f²  | ⦇in.(f+id)⦈    
| A* |Seq. finitas de A |[nil,cons]  | id+gxf | 1+XxY  | id+idxf  |map f   
| Nat  |Nrs naturais    |[zero,succ]   | -- |-- |  id+f  | --


### <a id="ex2"></a> Exercicio 2

    sum = ⦇ [ zero ,  add ] ⦈  
    length = ⦇ [ zero , succ . π2 ] ⦈  
    B(g,f) = id + g x f  
    T f = map f

A partir daqui é aplicar a lei de absorção para listas, depois outras leis mais básicas que já conhecem. 

Vamos a isso: 

`length = sum . map one`  
`≡ { definições }`  
`⦇ [zero, succ.π2] ⦈ = ⦇ [zero,add] ⦈ . T one`  
`≡ { (49) }`  
`⦇ [zero, succ.π2] ⦈ = ⦇ [zero,add] . B(one,id) ⦈`  
`≡ { (B(g,f) = id + g x f }`  
`⦇ [zero, succ.π2] ⦈ = ⦇ [zero,add . (one x id)] ⦈`


A partir daqui precisamos da aritmética e isso faz-se introduzindo variáveis. Lado esquerdo:  
`(succ.π2)(a,b)=?` 
`succ x = 1 + x` etc)
E, no lado direito, `add.(one>< id)(a,b)=?`

1+b num dos lados; e no outro 1+b também

Logo `succ.π2 = add . (one x id)` e os dois catas são iguais pois têm o mesmo gene.

Era o que queríamos mostrar, `⦇ [zero, succ.π2] ⦈ = ⦇ [zero,add . (one x id)] ⦈`

Vou dar um “empurrão” na (F2) que é parecida com a anterior:  

`length = length . map f`  
`≡ { definições }`  
`⦇ [zero, succ.π2] ⦈ = ⦇ [zero,succ.π2] ⦈ . T f`  
`≡ { (49) }`  
`⦇ [zero, succ.π2] ⦈ = ⦇ [zero,succ.π2] . B(f,id) ⦈`  
`≡ { ….. }`  

Podem pf simplificar-me o lado direito e dizer-me como fica?

`B(f,id) = ?`

      length = length . map f  
    ≡ { definições }  
        ⦇ [zero, succ.π2] ⦈ = ⦇ [zero,succ.π2] ⦈ . T f  
    ≡ { (49) }  
        ⦇ [zero, succ.π2] ⦈ = ⦇ [zero,succ.π2] . B(f,id) ⦈  
    ≡ { (B(g,f) = id + g x f }  
        ⦇ [zero, succ.π2] ⦈ = ⦇ [zero,succ.π2] . (id + f x id) ⦈  
    ≡ { absorção + }
      ⦇ [zero, succ.π2] ⦈  = cata ( [zero . id , succ.p2 .( f * id) ] ) 



### <a id="ex3"></a> Exercicio 3


    length [] = 0  
    length [a] = 1  
    length (x++y) = length x + length y

Queremos provar  

    length · concat = sum · map length
(gene do sum:  `sum = ⦇ [ zero ,  add ] ⦈`)
absorçao cata,e def de sum 
Fusão-cata e def F length=id+id*length
fusão +,absorção + e por Eq +
introdução de variáveis e def de conc
Se introduzirem as variáveis `(x,y)` na cláusula que falta obtêm o 3º axioma acima, logo está feito.  `conc(x,y)=x++y` etc etc

### <a id="ex4"></a> Exercicio 4

    B(f,g) = id + f x g²  
    count = ⦇[zero,succ·add·π2]⦈  
       count · (BTree f) = count  
    ≡ { ........................ }

NB: `BTree f` é o `T f` deste tipo, que mapeia f em todos os nós de uma árvore

absorção cata
cata([zero,succ.add.p2.f*id^2])

vamos aqui

       count · (BTree f) = count  
    ≡ { definição de count e absorção cata }  
       ⦇[zero,succ·add·π2]⦈ · (BTree f) = count  
    ≡ { absorção cata }  
       ⦇[zero,succ·add·π2].(id + f x id) ⦈ = count  
    ≡ { absorção + }  
       ⦇[zero,succ·add·π2.(f x id)]⦈ = count  
    ≡ { ........................ }

id . p2 ? natural p2
⦇[zero,succ·add·p2]⦈ = count
count = count










