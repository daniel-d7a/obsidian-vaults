# CH-4 analysis, taking your software into the real world

analysis helps you make sure your app works in the real world.

identify the problem > plan a solution > update the use cases > add new requirements & use cases > update the code.


problem: the bark recognizer opens the door whan it hears any bark,not just the owner's dog's bark.

solution: the bark recognizer should open the door only when it hears the owner's dog's bark.

we need a new use case to store a dog's bark.

Now that we have the requirements and use cases updated we can start working on our code, we need a way to compare barks using the recognize method.

one way could be to store a bark as a string and compare strings, another would be to store a bark as an object from the the new Bark class and add an 'equals' method to delegate bark comparisons to it.

the correct way however is to create a Bark class and an equals method, but to store multiple barks inside the bark recognizer, as the dob may sound a little different each time he barks based on his mood or state.

to get to that conclusion we needed to apply some textual analysis and draw some UML diagrams.

## textual analysis

you need to pay attention to nouns and verbs in the use cases to know what to focus on. our system focuses on the dog no matter how it sounds, not a single bark.

looking at nouns and verbs in the use case to figure out classes and methods is called textual analysis.

nouns are candidates for classes, and verbs are candidates for methods. not every noun is a class nor every verb is a method.

nouns that are outside the system (like user and manager) don't get turned into classes, unless we need to interact with it or store information about it.

a good use case clearly explains what the system does, making textual analysis quick and easy.

## UML diagrams

we can represent associations using solid arrows with triangle heads, association is when 2 classes are connected by a reference (e.g. inheritance, extension, ...etc.).

association arrows have a multplicity number that shows how many of each class contributes to the association, where (*) means any number.

UML diagrams give us a bird-eye view of the classes we have, how they relate to each other, what data and methods they have, this allows us to see the system from afar and communicate our ideas more clearly.
However, they omit many implementation details, such as constructors, method bodies, type details, ...etc.

<<uml of the correct solution>>
<<code for the final version>>