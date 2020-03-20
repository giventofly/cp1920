
# ficha 4

## Resoluções por Nuno Macedo

### Index

 - [Exercicio 6](#ex6) 

### <a id="ex6"></a> Exercicio 6

É nos dito que `Aᴮ⁺ᶜ` e `Aᴮ x Aᶜ` são isómorficos ou seja, uma função que recebe ou B ou C e dá um A é a mesma coisa que ter duas funções, uma que só recebe Bs e outra que só recebe Cs como é que provamos isto? são nos dadas duas funções `join` e `unjoin` entre esses dois tipos e é nos dito para provar que são isomorfismos, ou seja: `join . unjoin = id` e `unjoin . join = id`.

##

como são funções de ordem superior

`join (f,g)` é pointwise: as funções são as variáveis

se as definições estão em pointwise, temos que começar por introduzir variáveis no exercício

qual é o tipo de `unjoin . join?`

é uma composição como qualquer outra, por isso é o tipo de entrada do `join` para o de saída do `unjoin`

por isso que variáveis é que introduzo? temos de introduzir dos dois lados (f,g)

O `join` recebe um par de funções `Aᴮ x Aᶜ`

então, agora que estamos em pointwise, é só aplicar a definição do join e unjoin, que nos é dada no exercício e as leis do formulário da última secção, que têm das definições pointwise dos operadores por isso, arrancamos com a da composição e do id, que já devem ser triviais nesta fase.


    unjoin . join = id  
    = { introduzir variáveis (69) }  
    	(unjoin . join) (f,g) = id (f,g)  
    = { def-comp (70), def-id (71) }  
    	unjoin (join (f,g)) = (f,g)  
    = { def-join }  
    	unjoin [f,g] = (f,g)  
    = { def-unjoin }  
    	([f,g].i1,[f,g].i2) = (f,g)  
    = { cancelamento-+ (18)}  
    	(f,g) = (f,g)
    
 


