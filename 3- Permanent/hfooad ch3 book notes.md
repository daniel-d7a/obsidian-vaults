[[Books]]
#books/programming/hfooad
# CH-3 I Love You, You’re Perfect...Now Change: requirements change

the one constant in software is change.

- requirements change.
- new need come up.
- new solutions come up.
- languages change.
- new languages.
- new ideas.

## the customer is always right

the customer is always right, even if they want to change something they requested before. If the customer requested it then it must be done. However, if you have good use cases the change should be easy to implement.

now Todd and Gina keep losing the remote or sometimes they don't hear Fido barking, they want the dog door to open when Fido barks at it (via a bark recognizer).

## Use cases revisited

- the use case should make sense to you as it is here to help you.
- you can write it in the formal format or the non formal format as you like.
- the main path should be the the most common path the system takes.
- anytime the use case changes you must go back and change your requirements.

Now the use case has 2 paths, either Todd and Gina hear Fido and press the button, or the newly installed bark rcognizer hears Fido and sends a request to open the door. We have also set the bark recognizer path is the main path as it is the most common.

we have also added these 2 requirements regarding the bark recognizer:- 

4. A bark recognizer must be able to tell when a dog is barking.
5. The bark recognizer must open the dog door when it hears barking.

<<code for the new system>>

### scenarios

scenario: A complete path through a use case, from the first step to the last.

most use cases have different scenarios, but they must share the same goal.

## final notes on changes

Sometimes a change in requirements reveals problems with your system that you didn’t even know were there.

when we tested the code we found out that when the door is opened using the bark recognizer it doesn't close automatically. that was because the code to close the door automatically was inside the remote class, to solve this we could have duplicated the code into the bark recognizer class, but instead we moved that code to the door class to remove duplication, and because it is the responsibility of door to close itself after a set amount of time,applying the DRY principle in the process.

Change is constant, and your system should always improve every time you work on it.

<<code for the final system>>