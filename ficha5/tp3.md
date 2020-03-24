
## ficha 5

  

### Notas por Renato Neves

 Tirando partidos dos catamorfismos, iremos ver como lidar com recursividade de forma muito mais _estruturada_ e _compacta_ em relação ao que vocês tem visto na programação. Por exemplo, iremos ver que a função,

    length : [a] -> Int
    length [] = 0
    length (x:xs) = 1 + (len xs)

se reduz a,

    length :: [a] -> Int
    length = cataList (either (const 0) ((1+) . p2))

e que a função que agrega listas,
 

    flatt :: [[a]] -> [a]
    flatt [] = []
    flatt (x:xs) = x ++ (flatt xs)

se reduz a,

    flatt :: [[a]] -> [a]
    flatt = cataList (either (const []) (uncurry (++)))

E que a função que soma todos os valores em folhas de árvores,


    summ :: LTree Int -> Int
    summ (Leaf x) = x
    summ (Fork(x,y)) = (summ x) + (summ y)

se reduz a,

    summ :: LTree Int -> Int
    summ = cataLTree (either id (uncurry (+)))


