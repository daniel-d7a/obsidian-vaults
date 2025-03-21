[[Books]]
#books/programming/hfooad
# CH-2 give them what they want: gathering requirements

to make sure your software does what the customer wants, you must first gather the right requirements.

in this chapter (and few of the upcoming ones) we will use an automatic dog door that is requested from us by Todd and Gina for thier dog Fido as an example. the requirements are very simple, a dog door with a remote that when pressed opens the door.

we build an initial verison of the door that looks <<like this>>, and while it seems fine, the users find many problems with it as soon as they used it, and we need to figure out why.


## requirements


requirement: a specific thing the system has to do to work properly.

- specific: only one thing, a thing you can test.
- system: your software, your application.
- do: be able to perform or be.
- work correctly: work as the customer want.

requirements specify what the system has to do or be, not how.

### gathering requirements

- you must listen to customers to figure out your requirements.
- you must also think beyond what the customer says or wants, as customers don't know what they want exactly or leave out some details.
- customers expect the system to work even when problems occur.
- the best way to gather good requirements is to understand the system and the way it is used, and anticipate problems and add requirements to solve them.
- good requirements = good software, bad requirements = bad software.

the problem with the dog door is that it doesn't close on its own,so it let many other animals such as rabits and rats to enter the ouse,Todd and Gina wanted the door to close automatically.

### requirements list

- requirements lists are just lists of things that the customer wants, they help you define and identify what the system needs to do.
- they can specify the steps in which the system is used in an ordered manner.
- the steps that are most common for the system are called the main path (also called the happy path).
- requirements lists can specify alternate paths (in case of problems or alternate usages).


the requirements list for the dog door:-

1. the door must be 12" tall (so Fido doesn't have to lean).

2. the button on the remote control opens the dog door if the door is closed, and closes the dog door if the door is open.

3.Once the dog door has opened, it should close automatically if the door isn’t already closed.


## use cases

A use case describes what your system does to accomplish a particular customer goal

- what: not how.
- particular: only one goal.
- customer: that is who we are working for an using the system (users outside the system)

a use case should have:

- a clear value: it helps the user achieve something.
- start and stop: something must begin the use case and something else must stop it.
- external initiator: some user (our outside system) that starts the use case.

use cases help us understand the system in order to write code that solves the customer problems, however it mustn't include code details.

### how to use use cases?

use cases have a formal look (with bullet points and all) and an informal look that looks like a story.

requirements and use cases go hand in hand, while use cases are steps for requirements, requirements must cover all the use cases.

talk to the customer > gather requirements > transform requirements to use cases > compare your use case to the requirements to make sure they match > start writing code.

using use cases helps us identify the parts where problems might happen and handle these situations in our code. Thus, when we write our code we must test the alternative paths just like we do the main path.


the use case for the dog door:- 

1. Fido barks to be let out.
2. Todd or Gina hears Fido barking.
3. Todd or Gina presses the button on the remote control.
4. The dog door opens.
5. Fido goes outside.
6. Fido does his business.
6.1. The door shuts automatically.
6.2. Fido barks to be let back inside.
6.3. Todd or Gina hears Fido barking (again).
6.4. Todd or Gina presses the button on the remote control.
6.5. The dog door opens (again).
7. Fido goes back inside.
8. The door shuts automatically.

now since our use case covers our requirements list, we are ready to write the code for the dog door.

<<link to the final version of the dog door>>
