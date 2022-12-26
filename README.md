# SeaBattle
1st class dots on the board,
2 class ship on the board,
3 class exclusions,
4 class game board,
5 player classes,
6 main game class.

STEPS

We will solve the problem by consistently implementing the right classes. In many cases, correctly classifying your code into classes makes your code readable and saves a lot of time. Two groups of classes can be distinguished:

Internal game logic - ships, game board and all logic associated with it.
External game logic - user interface, artificial intelligence, game controller, which counts beaten ships.
At the beginning it makes sense to write exception classes to be used by our program. For example, when a player tries to shoot at a square outside the field, corresponding BoardOutException should be thrown in the internal logic, then caught in the external logic, displaying a message about this error to the user.

Next we need to implement the Dot class - a class of dots on the field. Each dot is described by parameters:

x coordinate .
Coordinate on y axis .
In the program we will often exchange information about points on the field, so it makes sense to create a separate data type for them. It would be very convenient to implement __eq__ method in this class to be able to check points for equality. Then, in order to check if a point is in the list, just use the in operator, just like we did with numbers.

Next is the Ship class - a ship on the playing field, which is described by parameters:

Length.
The point where the bow of the ship is located.
Ship direction (vertical/horizontal).
Number of lives (how many dots the ship has not hit yet).
And has a dots method that returns a list of all ship's dots.

The most important class in internal logic is Board class - game board. The board is described by parameters:

A two-dimensional list that stores the states of each of the cells.
A list of ships on the board.
Parameter hid of bool type - information whether to hide ships on the board (for output of enemy board) or not (for own board).
The number of live ships on the board.
And has methods:

The add_ship method, which puts the ship on the board (if no ship is put, throw out exceptions).
Method contour, which outlines the ship. It will be useful during games and in arranging ships (mark adjacent points, where the rules can not be a ship).
Method that outputs board to console based on hid parameter.
Method out, which for a point (object of class Dot) returns True if the point leaves the field, and False if it doesn't.
A shoot method which shoots the board (if there is an attempt to shoot out of bounds and into a used point, exceptions must be thrown).
Now we need to deal with the external logic: the Player class is the class of the player in the game (both AI and user). This class will be the parent for the AI and user classes. The Player is described by parameters:

Own Board (object of the Board class).
Enemy Board.
And has the following methods:

ask - a method that "asks" the player which square he is taking a shot at. While we make a common AI and user class, we can't describe this method. Let's leave this method blank. By doing so, we denote that the descendants must implement this method.
Move is the method that makes a move in the game. Here we call the ask method, take a shot at the enemy board (Board.shot method), catch exceptions, and if there are any, try to repeat the move. The method should return True if that player needs to retry (for example, if they hit a ship with a shot).
It now remains for us to inherit the AI and User classes from the Player and redefine the ask method in them. For AI, this will select a random point, but for User this method will ask the coordinates of the point from the console.

After that we create our main class - the Game class. The game is described by parameters:

Player-user, object of class User.
User board.
Player-computer, object of class AI.
Computer board.
And has methods:

random_board - method generates a random board. To do this, we simply try to place ships into random squares of initially empty board (in infinite loop, try to place ship into random board until our attempt is successful). It is better to arrange long ships first, and then short ships. If there are many (a few thousand) attempts to place a ship and it fails, then the board is unsuccessful and there is no chance to add a ship to it. In that case, start generating a new board.
greet - a method that greets the user in the console and tells about the format of the input.
loop - a method with the game loop itself. There we simply sequentially call the mode method for players and make a check on how many alive ships are left on the boards to determine victory.
start - start the game. First we call greet and then loop.
And we just need to create an instance of the Game class and call the start method.

As you write code, it's useful to check your progress by testing the classes you've written individually. To do this, you can simulate different situations, for example, create a list of ships, add them to the board and try to make a shot at different points. To test the functionality
*** Translated with www.DeepL.com/Translator (free version) ***


