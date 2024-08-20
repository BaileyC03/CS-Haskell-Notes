## CHAPTER 1:
**FEATURES OF HASKELL:**
- Concise programs
	- Usually 2-10x shorter line-wise than other languages. 
	- This is because it is specialised for a few use cases, and so has few keywords.
- Powerful Type System
	- A better type system than many other languages
	- Automatic polymorphism and overloading in some situations
- List Comprehensions
	- List-based functions can be carried out without recursion 
- Recursive Functions
	- Haskell loops through recursion
	- Recursive functions - Functions which are defined in terms of themselves
- High-Order functions
	- Functions can take functions as arguments and return functions as results.
	- this means you can have a function that is actually 2 functions slapped together
- Effectful Functions
	- Functions in Haskell are pure functions that take all their inputs as arguments and produce all their outputs as results
	- Many programs have a "side effect" that also happens during the function's runtime. 
		- Haskell allows this, without compromising purity, via the use of monads and applicatives
- Generic Functions
	- Most languages allow generic functions which take in a range of simple types. 
	- Haskell generics are able to take in much more. Any type that is either:
			- Functorial
			- Applicative
			- Monadic
			- Foldable
			- Traversable
- Lazy Evaluation
	- Haskell programs use "lazy evaluation"
		- No computation should be performed until the result is actually needed
- Equational Reasoning
	- Haskell programs are pure functions. 
		- This means equational reasioning techniques can be used to execute, transform or prove given properties of said program.
		- You can also calculate the entire program from the specifications and the intended behaviour mathematically
			- This can be used alongside induction to reason about recursive functions

**CHAPTER 1 EXERCISES**
- Give another possible calculation for the result of double (double 2)
	- double(2) + double(2)
	- (2+2) + double (2)
	- (2 + 2) + (2 + 2)
	- (4) + (2+2)
	- 4+4
	- 8
- Show that sum[x] = x for any number x
	- sum[] = 0
	- Sum[l : ln] = l + sum[ln]
	- sum [x] = sum[x:]
	- sum[x] = x + sum[]
	- sum[x] = x + 0
	- = x
- How should the definition of the function qsort be modified so that it produces a rverse sorted function of a list?
	- Change smaller and larger to be the other ways around
	- qsort larger ++ [x] ++ qsort smaller
- What would the effect of replacing <= with < be on the qsort algorithm?
	- The equal numbers would not be sorted into a list and would cause issues
## CHAPTER 2:
**STANDARD PRELUDE:**
 - Haskell has some built-in functions in a library file known as the standard prelude
 - It has functions like +, -, / etc and also a lot of list functions
 - Lists are defined in haskell by [] 
 - Some common library functions:
	 - Select the first element of a non-empty list:
		 - head [1,2,3,4,5]
	- Remove the first element from a non empty list
		- tail[1,2,3,4,5]
	- Select the nth element of a list (index from 0)
		- [1,2,3,4,5] !! 2 
	- Select the first n elements of a list:
		- take 3 [1,2,3,4,5]
	- Remove the first n elements of a list:
		- drop 3 [1,2,3,4,5]
	- Calculate the length of a list:
		- length[1,2,3,4,5]
	- Calculate the sum of a list of numbers:
		- sum[1,2,3,4,5]
	- Calculate the product of a list of numbers:
		- product[1,2,3,4,5]
	- Append 2 lists: 
		- [1,2,3,4,5] ++ [6,7,8]
	- Reverse a list: 
		- reverse[1,2,3,4,5
		- ]
**FUNCTION APPLICATION:**
	- In math, function application words by denoting the arguments in () while multiplication is denoted silently, such as - f(a,b) + cd
		- In haskell, this would be f a b + c * d
	- Function application has higher priority than any other operator.  a + b is (f a)+b

| Math       | Haskell   |
| ---------- | --------- |
| f(x)       | f x       |
| f (x,y)    | f x y     |
| f (g(x))   | f (g x)   |
| f (x,g(y)) | f x (g y) |
| f(x)g(y)   | f x * g y |

**HASKELL SCRIPTS:**
	- You can also define your own functions. They're defined in a script.
		- Script: text file with a sequence of definitions
		- Haskell scripts usually end in .hs
	- Its worth having 2 windows open when developing in haskell
		- One with text editor
		- One with the GHCi
	 - If you update the .hs file, you must do :reload in the GHCi in order to execute any new definitions. All of the below must begin with a colon (:)
		- load name
			- load script name
		- reload
			- reload current script
		- set editor name
			- set editor to name
		- edit name
			- edit script name
		- edit
			- edit current script
		- type expr
			- show type of expression
		- ?
			- Show all commands
		- quit
			- quit GHCI

**NAMING REQUIREMENTS:**
	- When defining a new function, the names of the functions and arguments must begin with lowercase letters. Anything after that (letters, numbers) are optional and can be caps. The following cannot be used however:
		- case
		- class
		- data
		- default
		- deriving
		- do 
		- else
		- foreign
		- if
		- import
		- in
		- infix
		- infixl 
		- infixr
		- instance
		- let 
		- module 
		- newtype
		- of
		- then
		- type
		- where
	- Arguments in haskell will have the suffix (s) on their name to indicate they may take multiple values. Dimensionality of a list may be denoted by the number of suffix S
		- css (2 dimensonal list)
		- Within a script, each definition within the same level must begin in the same column. This allows it to be possible to determine definitions' grouping by their indentation level.
			- Eg:
				- a = b + c
					- where
					- b = 1
					- c = 2
				- d = a * 2
**COMMENTS:**
- Scripts can also contain comments. Comments can be done like so:
	- -- This is a comment
	- {-
		this is a multi line comment
		-}
## CHAPTER 3:
**BASIC CONCEPTS:**
 - A type is a collection of related values (bool, int, float)
 - Bool has 3 values (True, False)
 - Bool -> Bool contains all functions that map arguments from Bool to results from Bool
	 - Such as "not" as a function
	- We use the notation v :: T to say that v is a value of type T
		- E.g: False :: Bool
		- E.g: True :: Bool
		- E.g: Not :: Bool -> Bool
	- It can also be used to describe the type that will be returned from an expression such as: 
		- not False :: Bool
	- In Haskell, every expression must have a type which is calculated prior to evaluating the expression.
		- This is done by something called type interference.
		- If f is a function that maps types A to results of type B. If e is of type a, then f e is type B 
	- Haskell Programs are type safe, meaning type errors can never occur during evaluation. 
		- In practice, haskell detects a very large class of program errors due to type interference
**BASIC TYPES:**
- Haskell provides a number of basic types, there are the main ones: 
	- Bool - Logical values
		- True, False
	- Char - Single Characters
		- All single characters in the unicode system
		- Alongside some things such as \n and \t 
		- Must be in single quotes
	- String - String of characters
		- Contains all of the sequences of characters. Strings must be in double quotes.
	- Int - Fixed precision integers
		- Type contains integers (-100, 1, 0, 999).
		- - 2^63 to 2^63
	- Integer - Arbitrary precision integers:
		- Type contains all integers, with as much memory as necessary being used for their storage. No limits on how large or small you can go. These are usually processed slower as most computers have native support for "Int" but not these
	- Float - Single precision floating point numbers
		- Numbers with a decimal point
	- Double - double precision floating point numbers
		- Similar to float, but has 2x as much data available to increase precision.
**LIST TYPES:**
-  A list is a sequence of elements of the same type, with the elements being enclosed in square brackets - []. We write [T] for the type of all lists whose elements have type T.
	- [False, True, False] :: [Bool]
	- ['a','b','c','d',] :: [Char]
- Due to lazy evaluation, lists can be infinitely sized and that is both natural and practical :)

**TUPLE TYPES:**
- A tuple is a finite sequence of components of possibly different types, held in brackets ()
- We write (T1, T2, T3) to define their types:
	- (False, True) :: (Bool, Bool)
	- (False, 1, True) :: (Bool, Int, Bool)
- The number of components in a tuple is known as its arity (Note: This is not a typo, its actually arity, not parity or some other shit.) 
	- Arity 0 - The empty tuple
	- Arity 2 - Pairs
	- Arity 3 - Triples
	- etc etc
- Tuples of arity 1 are not allowed as they conflict with the use of parenthesis to define the evaluation order (1+3)*2
- The type of a tuple conveys its arity
	- (Bool,Char) contains all pairs comprising a Bool 1st component, Char 2nd
	- No limit to what can be a component of a tuple. you can have tuples of tuples, tuples of lists, lists of turples yaddah yaddah 
	Tuples must have a finite arity, to ensure they can always be inferred prior to evaluation

**FUNCTION TYPES:**
- A function is a mapping from arguments of one type to results of another type. 
	- We write T1 -> T2 for the type of all functions that map arguments of type T1 to T2
	- not :: Bool -> Bool
	- even :: Int -> Bool
	- add :: (int, int) -> int
-  No restriction that functions must be (total) on their argument type
	- Some arguments, a result may not be defined (e.g: "head" on an empty list)

**CURRIED FUNCTIONS:** (REVISE ME)
- Functions with multiple arguments may also be handled in another, less obvious way
	- exploiting the fact that functions may return a function as a result
	Observe:
		add' :: Int -> (Int -> Int)
		add' x y = x+y
			- This type states that add' is a function that takes an argument of type Int and returns a result that is a fuction of type Int -> Int. The definition itself states that add' produces the same final result as last add but takes its two arguments one at a time

**POLYMORPHIC TYPES:**
- Library function length calculates the length of a list regardless of size. 
	- To work on any type, use a type variable like so:
		- length :: [a] -> int
			- a must be lowercase and are usually named a,b,c
	- A type that contains 1 or more variables is considered polymorphic
	- 
**OVERLOADED TYPES:**
- + calculates the sum of any 2 numbers.
- The idea that this can be applied to any numeric type is made precise in its type by a class constraint
		- Class constraints are written C a where C is the class and a is the type variable. 
		- (+) :: Num a => a -> (a -> a)
			- for any type a that is an instance of class Num, the function (+) has type a-> a-> a
				- Putting a function in parenthesis curries it, seen in chapter 4.
			- A type that contains one or more class constraints is considered to be overloaded
			- Numbers themselves are overloaded
		
**BASIC CLASSES:**
- A type is a collection of related values.
- A class is a collection of types that support overloaded operations (known as methods)
	- Haskell provides some basic classes which are built into the language. Basic ones:
		- Eq - Equality Types:
			- Types that can be compared for equality and inequality (== or \=)
			- Bool, Char, String, Int, Integer, Float, Double, list, tuples are all Eq
			
		- Ord - Ordered types
			- Contains types that are within equality types, but also those whos values are (linearly) ordered and can be compared with < , <=
				- Bool, Char, String, Int, Integer, Float, Double, list and tuple (assuming their elements are also elements)
				
		- Show - Showable types
			- Class contains values which can be turned into strings of characters using the following method:
				- show :: a -> String
				- Bool, Char, String, Int, Integer, Float, Double are all instances of such
				- Lists and tuples also are, assuming their elements are also showable types
				
		- Read - Readable types
			- Class is types whos values can be converted FROM strings:
				- show :: String -> a
				- Bool, Char, String, Int, Integer, Float, Double are all instances of such
				 Lists and tuples also are, assuming their elements are also showable types
				 - read "[1,2,3]" :: [Int]
					 [1,2,3]
					^ The use of :: i this resolves the type of the result which could not be infered y the interpreter. 
			
		- Num - Numeric Types
			- Types whos values are numerc and can be processed with +,-,*, negate,abs
			- Note: negative numbers must be parenthesised when used as arguments to functions.
			
		- Integral - Integral Types
			- Class contains instances of numeric class num, but who are also integers and support integer division and integer remaintder:
				- div :: a -> a -> a
					- aka div :: a -> (a -> a)
				- mod :: a -> a -> a
			- Integer and Int are integral types
			
		- Fractional - Fractional types
			- Contains types of numeric class Num, but also those who are non-integral
				- They will therefore support the methods of fractional division and reciprocation
				- (/) :: a -> (a -> a)
				- recip :: a -> a
			- Types Float and Double are fractional types

['a','b','c'] :: [Char]
('a','b','c',) :: (Char)
[(False, 'O'), (True,'1')] :: [(Bool, Char)]
([False, True], ['0','1']) :: ([Bool],[Char])

