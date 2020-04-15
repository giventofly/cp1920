
# ficha 6

## Resoluções por Renato Neves


### Index

-  [Exercicio 5](#ex5)


  

### <a id="ex5"></a> Exercicio 5

 O exercício 5, em particular,  mostra-nos que a função `sumprod` pode ser optimizada de forma a não chamar tantas vezes a operação de multiplicação (a*): notem que `sumprod` chama a operação (a*) n-vezes em que n é o tamanho da lista.  

**Usando cálculo de programas**, vamos converte-la numa função que chama (a*) apenas uma vez. 

Para dar mais algumas intuições, notem que enquanto a função _sumprod_ multiplica cada elemento da lista por 'a' e retorna o somatório destas multiplicações, a função _sum_ (que é função a qual nós queremos chegar), soma primeiro todos os elementos da lista e depois multiplica o somatório resultante por 'a'.

Para este exercício convém relembrar o functor F associado às listas: é definido como 

    F f = id + id x f.

`(a*) . sum = sumprod a`  
`≡ { Definição de sum e de (sumprod a)}`  
`(a*) . ⦇[zero, add]⦈ = ⦇[zero, add . ((a*) x id)]⦈`  
`<= { Lei fusão-cata, definição functor F das listas}`  
`(a*) . [zero, add] = [zero, add . ((a*) x id)] . (id + (id x (a*)))`  
`≡ { Fusão-+, Absorpção-+}`  
`[(a*) . zero, (a*) . add] = [zero . id, add . ((a*) x id) . (id x (a*))]`  
`≡ { Natural-id, Functor-x}`  
`[(a*) . zero, (a*) . add] = [zero, add . ((a*) x (a*))]`  
`≡ { Eq-+ }`  
`(a*) . zero = zero`  
`(a*) . add = add . ((a*) x (a*))`  
`≡ { Lei elemento absorvente e distributividade (a*0 = 0 e a*(x+y) = a*x + a*y) }`  
`True`


