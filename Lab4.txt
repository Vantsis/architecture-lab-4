-- exercise 1

insertAt :: [u] -> u -> Int -> [u]
insertAt [] e _     = [e]
insertAt xs e 0     = e:xs
insertAt (x:xs) e n = x : insertAt xs e (n-1)

move :: Eq u => [u] -> u -> Int -> [u]
move xs x' n =
    let
        -- very useful indexed list, perfect for splitting
        -- our original list.
        indexedList = zip xs [0..]
    -- we check if the element is in the list
    in case lookup x' indexedList of
        -- if it is, then split the list like:
        -- first half, element, second half
        Just index -> 
            let
                (first,x:rest) = splitAt index xs
            -- once splitted:
            --  - if n is 0, we return first half + second half
            --    without the element
            --  - if n is possitive, we insert the element at the index n
            --  - if n is negative,  we insert the element at n to the left
            --    which is equivalent to reversing the list, inserting the element
            --    at -n and then reversing the list again
            in if n == 0 then first ++ rest else
                if n > 0 then first ++ insertAt rest x n else
                    reverse (insertAt (reverse first) x (-n)) ++ rest
        -- If it isn't we return the same list.
        Nothing    -> xs

-----------------------------------------

-- exercise 2

combine :: [u] -> [v] -> (u->v->w) -> (u->v->w) -> (Int -> Bool) -> [w]
-- zipWith3 does exactly what we need to provided we feed it a list
-- of indexes. The power of Prelude
combine as bs f g h = zipWith3 m as bs [1..]
    where
        -- The definition of the function provided in the pdf.
        m a b i
            | h i       = f a b
            | otherwise = g a b