[[Books]]
#books/programming/hfooad

# CH-1 great software begins here: well-designed apps rock

this book talks about how to write great software, but what is great software to begin with?

## what is great software?

great software:

- does what the customer wants.
- well-designed, well-coded, easy to maintain and modify reuse and extend.
- little dependency between classes (loose coupling).

problem: rick has an inventory system for his guitar shop that doesn't quite work well.

solution: apply the 3 steps to make the app great.

<<link the code to the current state of rick's inventory app>>

## how to write great software?

1. make sure the software does what the customer wants.
2. apply basic OOP principles to add flexibility.
3. make it more maintainable and reuseable.

### functionality

- fix bugs.
- add tests (simple tests to make sure your code works).
- you can do some design here.
- make sure the app works before moving on.

in rick's app, the search function didn't work correctly due to case sensitive string comparisons, we fixed this by using enums instead of strings were applicable, and using case insensitive string comparisons elsewhere.

also rick wanted the system to show all the matching results instead of only one match, we solved this by having the search function return a list of results.

### flexibility

- apply basic object oriented principles (enums, view models, composition through encapsulation).
- remove code design problems (duplication, redundancy, object mis-match, unused properties).
- one way of reducing duplication is following the rule "encapsulate what varies away from what stays the same" by extracting (or encapsulating) common properties used in multiple places to their own class.
- encapsulation (see appendix) allows us to to change data or behavior without changing other classes. It also allows us to hide the inner workings of your application’s parts, but yet make it clear what each part does.
- apply other principles such as polymorphism, abstraction, and inheritance.
- good class design and flexible code make it easier to change or add to it later.

in rick's app we moved the properties used for searching for a guitar into a new class called 'GuitarSpec' and had the search function take an object of that class instead of separate properties, thus applying encapsulation.

### maintainability and reusability

- remove or reduce coupling between classes by introducing delegation and more encapsulation (and design patterns, and solid principles).
- when each class is independent and only cares about its own functionality changes to one class don't require changes ot other classes that use it, resulting in more reusability.
- delegation is when a class does a task and asks another class to perform it or a part of it, this makes each class worry about its own functionality rather than spreading its code across the application.
- delegation allows class to be reused in similar or even different projects later, and makes your application code loosely coupled.

problem: adding a property to the guitar spec class requires modifications to the inventory and guitar classes.

solution: we use delegation and more encapsulation. 

we used delegation by moving the guitar spec comparison from the search method to the guitar spec class, this will reduce the coupling between the inventory class and the spec class, that is when the spec class changes the inventory class doesn't have to change.

we added more encapsulation by making the guitar class take an object of the guitar spec instead of separate properties.

## fragile software vs. robust software

fragile software breaks easily and is hard to upgrade or maintain, and will leave you fixing bugs late at night, while robust software is exactly the opposite as it satisfies the customer and the developer.

Object oriented analysis and design (OOA&D) provides a way to produce well-designed applications that satisfy both the customer and the programmer.

<<link to the final version of the code>>
