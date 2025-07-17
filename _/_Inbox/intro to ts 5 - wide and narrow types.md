#video_script/typescript_intro


- unions are a collection of types where the type can be either one
- most popular are literal unions
- e.g. document event types

- we have wide and narrow types
- wide types can have many values like unions
- narrow types can have less values

- a narrow type can be assigned to a wide type but not vice versa
- string is wide, "hello" is narrow
- number is wide, "42" is narrow
- unions are wider than their members, the above rules still apply
- we can only use wide types in a way that is compatible with all the members

## Narrowing

- the idea of telling typescript that this variable is narrower than what it is originally
- by narrowing we can use the type to its full extent like calling type specific methods
- we can use many tools
	- typeof
	- in
	- &&
	- instance of class
	- throwing errors
	- early returns
	- truthy checks against null and undefined
	- type guards
	- type assertions
	- using discriminated unions
	- using as const
	- assignment

## Unknown and never

- unknown is the widest type in ts
- anything can be assigned to unknown
- can be assigned to nothing
- represents somethings that we don't know like fetching from an api
- can be used for input agnostic functions such as type guards 
- can be used as a fall back

- never is the narrowest type in ts
- can be assigned to anything
- can't be assigned nothing
- used for conditional types and exhaustive checks
- object keys with never type get dropped automatically 

- any is not a type
- it is a compiler macro to opt out of the type checking
- any can behave like the narrowest and widest type at the same time
- can be assigned anything and can be assigned to anything