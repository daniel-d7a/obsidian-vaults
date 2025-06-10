## Interfaces

- can only represent objects and functions
- intersections and extension 
- interfaces can be extended 
- interfaces can extend multiple interfaces 
- can represent functions as an object's call signature 

## Types

- best candidates are fn types and objects
- are like typescript variables
- Are aliases for other types
- types can extend each other
- types can extend multiple other types

## Types vs interfaces

- interface extends is cached so it is faster
- interfaces with the same name collapse to one (declaration merging)
- usefull for overriding global types like window
- types with the same name cause errors
- both support optionals
- both support 2 function ways
- interface extends is faster than type intersection
