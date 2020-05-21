  

# ficha 12


## Resoluções por Renato Neves


### Index

-  [Exercicio 1](#ex1)
-   [Exercicio 2](#ex2)
-   [Exercicio 3](#ex3)


### <a id="ex1"></a> Exercicio 1

Vamos começar por resolver o exercício 1 (sobre hilomorfismos) da ficha 12. Após este exercício vamos concentrar inteiramente em mónades.

Lembrem-se dos vídeos que um hilomorfismo `_h_` nada mais é que um anamorfismo `[( g1 )]` seguido de um catamorfismo `⦇ g2 ⦈`:`⦇ g2 ⦈ . [( g1 )]`

Intuitivamente, o anamorfismo **gera** informação que depois o catamorfismo **processa**.

O exercício 1 diz-nos que certas funções `f` podem ser caracterizadas como hilomorfismos. Especificamente, funções `f` que fazem o seguinte diagrama comutar: (edited)

      T <---- in ----    FT  
      |                  |  
      |                  |  
      f              F(<id,f>)  
      |                  |  
      V                  V  
      A <---- g  ---- F(T x A)

Mais, o exercício diz que a função `factorial` é uma tal função `f`. Vamos instanciar o diagrama acima com a função `factorial` a ver se  
é mesmo verdade. Neste caso, o functor F associado é o functor dos números naturais.

    Nat0 <---- in ----   1 + Nat0  
      |                    |  
      |                    |  
     fac                id + <id,fac>  
      |                    |  
      V                    V  
    Nat0 <--- [g1,g2] -- 1 + Nat0 x Nat0


A minha primeira pergunta para vocês é: quais são as funções `g1` e `g2` pretendidas ?

Por outras palavras quais são as `g1` e `g2` que fazem o diagrama comutar, conhecendo nós o comportamento da função factorial ?

a `g2` recebe dois números naturais: `n` e `fac n` e nós queremos devolver `fac (n + 1)`

`fac (n + 1) = (n+1) * (fac n)` portanto...

`g2(n, fac n) = (n+1) * (fac n)`

em geral

`g2(n, m) = (n+1) * m`

Como é que `g2` fica em pointfree ?

 `g2 = mul. (succ x id)`

Então dado que o diagrama do `fac` comuta, o exercício diz-nos que `fac` pode ser visto como um hilomorfismo. Mas antes de conseguirmos ver isto, vamos ter que resolver os passos em falta.

Para isso é importante lembrarem uma lei de hilomorfismos que foi dada na ficha anterior, nomeadamente,  

`h = f . F h . g ≡ h = ⦇ f ⦈ .〖g〗 (*)`

Então o primeiro passo é:

`Lei isomorfismos in/out (2.19 dos apontamentos), absorpção-x, Functor-F`

portanto o segundo passo é: `(*)`

Seguindo os passos do exercício para `fac`

`[fac.in](https://slack-redir.net/link?url=http%3A%2F%2Ffac.in&v=3)` `= [g1,g2] . F <id, fac>`  
`≡ { Definição Functor dos naturais }`  
`fac = [g1,g2] . (id + <id, fac>)`  
`≡ { Exercício 1 }`  
`fac = ⦇ [g1,g2] ⦈ .〖 (id + <id,id>) . out 〗`

Falta descobrir qual é a _estrutura virtual intermédia_ i.e. a estrutura de dados que está entre o catamorfismo e o anamorfismo acima. Neste caso o functor G é o 'representante' da estrutura virtual intermédia i.e. se soubermos a definição de G sabemos qual é a estrutura virtual. Então...

`G f`  
`= { Por definição }`  
`F (id x f)`  
`= { Definição functor naturais }`  
`id + (id x f)`

Qual é a estrutura de dados associada ao functor `G` tal que `G f = id + (id x f)` ?

Então a estrutura virtual intermédia é a das listas


Admito, o exercício é interessante mas é preciso algum tempo para o digerir

Portanto como TPC, eu sugiro que desenhem o diagram correspondente a`fact = ⦇ [g1,g2] ⦈ .〖 (id + <id,id>) . out 〗`sabendo que a estrutura virtual intermédia é a das listas.


### <a id="ex2"></a> Exercicio 2

Este exercício é do mesmo estilo que o anterior: queremos pegar numa definição que usa composição monádica • e converter a definição para uma definição a la Haskell.

Relembrem que `for b i` é um catamorfismo de naturais que dado um número natural `n` aplica a função `b` `n`-vezes ao valor `i`.

`k = ⦇ [const (u i), g • id] ⦈`  

`≡ { Universal-cata , F f = id + f }`  
`k . in = [const (u i), g • id] . (id + k)`  

`≡ { in = [zero,succ] }`  
`k . [zero,succ] = [const (u i), g • id] . (id + k)`  

`≡ { Fusão-+, Absorção-+ Eq-+ }`  
`k . zero = const (u i)`  
`k . succ = (g • id) . k`  

`≡ { zero = const 0 e Lei (66) }`  
`k 0 = u i`  
`k . succ = g • k`  

`≡ { Igualdade extensional e u = return }`  
`k 0 = return i`  
`k(n+1) = (g • k) n`  

`≡ { (F3) }`  
`k 0 = return i`  
`k(n+1) = do { b <- k n; g b }`

### <a id="ex3"></a> Exercicio 3

O exercício 3 resume-se a provar propriedades sobre o monadic binding `(>>=)` que é muito usado em Haskell. O monadic binding pode ser  definido via composição monádica da seguinte maneira:

`(>>= f) = f • id (F4)`

Isto vai ajudar a provar as igualdades desejadas: como se nota que vocês estão cansados, eu faço a primeira e a segunda, vocês fazem a última. Vou fazer as versões pointfree porque os cálculos ficam muito mais fáceis de perceber.

___
`(>>= id)`  
`≡ { (F4) }`  
`id • id`  
`≡ { μ vs. • (68) }`  
`μ`

___
`(>>= g) . f`  
`≡ { (F4) }`  
`(g • id) . f`  
`≡ { Associatividade •/. (66) e natural-id }`  
`g • f`

___
`(>>= g) . (>>= f)`  
`= { (F4) }`  
`(g • id) . (f • id)`  
`= { Associatividade •/. (66) e natural-id }`  
`g • (f • id)`  
`= { Associatividade • (64) }`  
`(g • f) • id`  
`= { (F4) }`  
`(>>= (g • f))`








