Exercise 1.
Write a move function in Haskell, which will take as arguments a list s of any type that supports comparison for equality, an x element of the same type as the list elements and an integer n and return the list resulting from s with following way:
• if x is not contained in s, then the return list is s.
• if x is contained in s then
	- if n is a positive number, then the return list results from s by moving the first 	occurrence of element x by n positions to the right, or at the end of the list if the 	first occurrence of x in s is followed by less than n elements.
	- if n is a negative number, then the return list is derived from s by moving the first 		appearance of the element x by | n | positions to the left, or at the top of 	the list if in s there are less than | n | elements before the first appearance of x.
	- if n = 0, then the return list results from s by deleting the first appearance of the 	element x. 
The type of the function should be Eq u => [u] -> u-> Int -> [u]. The function should return a result even if its first argument is an infinite list containing the element x.
Use the following values to check:
Main> move [] 3 5
[]
Main> move [1,2,3,4] 0 4
[1,2,3,4]
Main> move [1,2,3,4,3,2,1] 3 3
[1,2,4,3,2,3,1]
Main> move [1,2,3,4,5,6,7,8] 6 7
[1,2,3,4,5,7,8,6]
Main> move "skin" ’k’ 0
"sin"
Main> move "factor.bit." ’.’ (-2)
"fact.orbit."
Main> move "0000.1111.00" ’.’ (-10)
".00001111.00"
Main> move ["one", "two", "three"] "one" (-2)
["one","two","three"]
Main> move ["one", "two", "three"] "one" 1
["two","one","three"]
Main> move ["one", "two", "three"] "three" 5
["one","two","three"]
Main> move ["one", "two", "three"] "three" (-2)
["three","one","two"]
Main> move [True] True 0
[]
Main> move [True] True 3
[True]
Main> move [True] True (-1003)
[True]
Main> head (move [1..] 1 91)
2
Main> head (tail (move [1,5..] 4005 (-1000)))
4005


Exercise 2.
Write a higher order function combine in Haskell, which will accept as arguments two lists s = [a1, a2, . . . , ak] and t = [b1, b2,. . . , b`] with elements of type u and v respectively, two functions f and g of type u-> v-> w and one function h of type Int> Bool and will return as a result the list [c1, c2,. . . , cmin (k, `)] with elements of type w, where
 
The type of the function should be [u] -> [v] -> (u-> v-> w) -> (u-> v-> w) -> (Int-> Bool) -> [w].
Use the following values to check:
Main> combine [5,4,3,2] [7,8,9,10] (*) (^) odd
[35,65536,27,1024]
Main> combine [2,2..] [1..20] (*) (^) (\n -> mod n 5 == 1)
[2,4,8,16,32,12,128,256,512,1024,22,4096,8192,16384,32768,32,131072,262144,524288,
1048576]
Main> combine ["summer","drops","black","white"] ["time","rain","board","snow"]
(++) (\x y -> y++x) odd
["summertime","raindrops","blackboard","snowwhite"]
Main> combine ["summer","drops","black","white","time","rain","board","snow"] [1..]
(\x y -> (x,0)) (\x y -> ("",y)) even
[("",1),("drops",0),("",3),("white",0),("",5),("rain",0),("",7),("snow",0)]


Instructions
1)	To write the functions you need to use the standard Lab2.hs file in which the type statements of the functions you need to construct are ready as well as an equation that defines the functions so that they return a predefined value for all values of the arguments. To answer an exercise you can replace the above equation with the appropriate equations that define the value of the function. You do not need to modify the type or name of the function.
2)	if you use import to embed ready-made code, the corresponding exercise will not be graded.
3)	Each of the functions that you are asked to implement should have the specific name and the specific type that is described in the pronunciation of the corresponding exercise and that exists in the standard file Lab2.hs. If in some exercise the name or type of function does not match the one given in the pronunciation, the exercise will not be graded.
4)	However, if the functions do not return values for some of the control values (eg they cause stack overflow, endless calculation or some runtime error) then the corresponding exercise will not be graded. If the file you submit contains syntax errors, then the entire lab exercise will be reset.


