# Unions, Literals, and Narrowing

## Unions and Literals

### Union Types

a union type means the type can be this or that (or that, or that, …etc)

it is defined using the pipe ' | ' operator between the types (member of the union)

### Literal Types

types that represent literal values ('Yes', 'No', 1, 2, 3, true, false, …etc)

like the type of event in 'document.addEventListener'

### Combining Unions With Unions

if we made a union type whose members are union types we get the union of all the types involved.

## Narrowing

### Wider vs Narrower Types

the idea of a super and a sub type, where a sub (narrow) type can be used in place of the super (wide) type but not vice verca.

string is wider than 'small', and 'small' is narrower than string, because string can represent any string, but 'small' only represents 'small'.

### Unions Are Wider Than Their Members

if we have a variable of type 'string | number' we can pass it a string or a number, because it is wider, but if we have a variable of type number we can't pass it a 'string | number'.

### What is Narrowing?

converting the type of a variable from the wide type to the narrow type, using run time code. 

used to handle different types differently.

### Narrowing with typeof

if we have a type of 'string | number | boolean' we can use the 'typeof' operator within an if statement to narrow it to whatever we want (that is included in the union).

if (typeof data === "string") { /* data here is a string*/ } 
else {/* data here is number | boolean (aka the rest of the union)*/}

by narrowing the type we can us it to its full extent, like calling member functions like toUpperCase.

the narrowing happens only inside the if statement, type of data here is still 'string | number | boolean'

### Other Ways to Narrow

we can use other operators to narrow down the types such as 
- '&&', ' || ', ternaries, 
- instanceof: checks if the variable is an instance of a class e.g. Error, Regex, File 
- in: checks if a key exists inside an object ('data' in value)
- throwing errors
- early returns
- truthy checks to narrow against null and undefined (but that can fall to falsy values like empty strings, so testing with typeof is better here, unless you are also avoiding falsy values.)
- using type guards: a type guard is an if statement that ensures something is of a certain type, and returns a type predicate, that means if this succeeds then the data is of this type.

## unknown and never

### The Widest Type: unknown

this is the widest type in TS, meaning every other type can be assigned to it.

it represents something that we don't know what it is.

an example of using unknow would be when fetching data from an api or a websocket.

#### What's the Difference Between unknown and any?

any isn't a type, any opt out of type checking, it is the widest and the narrowest type at the same time, it can be assigned to anything and anything can be assigned to it.

unknown is a type, and it is the widest type in TS, everything can be assigned to it but it cannot be assigned to anything.

### The Narrowest Type: never

never represents something that will never happen e.g. a function that will never return (throws an error)

never is the narrowest type, nothing can be assigned to it, but it can be assigned to everything

## Discriminated Unions

they are unions that are discriminated using a common property of a literal type that is unique to every member of the union.

### The Problem: The Bag Of Optionals

example: a data fetching library

it could be in one of 3 states, loading, success, error

in success there should be data, in error there should be error.

if it was all in one, flat type we would have impossible cases, and we would have many optionals.

### The Solution: Discriminated Unions

we refactor the type to be a union of 3 types: {"loading"}, {"success", data}, {"error", error}

TS can narrow the type of the other properties based on the discriminator (in this case the status) using any of the techniques shown above.

if we destructure a discriminated union, the properties lose thier connection to the discriminator.

to allow destructuring we must do it inside the narrowing condition.

a common way of narrowing a discriminated union is using a switch statement on the discriminator.

we can have discriminated tuples, that do not lose the connection between the properties and the discriminator after destructuring.

to add defaults to a discriminated union condition we must first handle all known cases, then leave the default case for the else / default clause.









