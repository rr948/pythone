Draw A Game Board Solutions
Exercise 24
This exercise is Part 2 of 4 of the Tic Tac Toe exercise series. The other exercises are: Part 1, Part 3, and Part 4.

Time for some fake graphics! Let’s say we want to draw game boards that look like this:

 --- --- --- 
|   |   |   | 
 --- --- ---  
|   |   |   | 
 --- --- ---  
|   |   |   | 
 --- --- --- 
This one is 3x3 (like in tic tac toe). Obviously, they come in many other sizes (8x8 for chess, 19x19 for Go, and many more).

Ask the user what size game board they want to draw, and draw it for them to the screen using Python’s print statement.

Remember that in Python 3, printing to the screen is accomplished by

  print("Thing to show on screen")
Hint: this requires some use of functions, as were discussed previously on this blog and elsewhere on the Internet, like this TutorialsPoint link.

Sample solution
Let’s break this task into pieces and use Python 3.

First, the user needs to a numbers that represent the size of the game board (assuming the game board will be n by n). (Bonus exercise: extend the following code to make the game board not square.). The following snippet assumes that the person entered a number and doesn’t do any kind of error checking - for now, that’s OK.

  board_size = int(input("What size of game board? "))
Then, we need to draw each row of the game board. Each row consists of horizontal pieces (---) and vertical pieces (|). Each of these shows up in a pattern, so we can rely on for loops to help with the rendering.

To print a single row, we want to do something like this:

  print(" --- " * board_size)
To print the vertical parts of the row, we want something like this, because we don’t care about trailing whitespace, and because we want one more vertical line than the size of the board:

  print("|   " * (board_size + 1))
For a board of size board_size we want to print that many horizontal pieces and vertical pieces, plus an extra horizontal piece for the bottom. Let’s use functions for this entire operation, since we might want to change the style on the game boards for later use. All together, the program will look like this:

  def print_horiz_line():
    print(" --- " * board_size)

  def print_vert_line():
    print("|   " * (board_size + 1))

  if __name__ == "__main__":
    board_size = int(input("What size of game board? "))

    for index in range(board_size):
      print_horiz_line()
      print_vert_line()
    print horiz_line()
This way, if we ever decide to change the design of the game board by making it bigger, it will be easy to do! All we need to do is change the print_horiz_line() and print_vert_line() functions, and we’re all set!

A few user solutions not using functions
This one is pretty simple, and it is specific to the 3x3 board above. There is no way to change the size. Additionally, writing out the a and b lists in the print statement are tedious and can be improved with a list comprehension or for loop.

a = '---'.join('    ')
b = '   '.join('||||')
print('\n'.join((a, b, a, b, a, b, a)))
view rawtrivial solution hosted with ❤ by GitHub
The author chose to use a while loop instead of a for loop to do the printing, which was an interesting choice. But it works!
def drawboard(kamal):
    kamal = int(kamal)
    i = 0
    ho = "--- "
    ve = "|   "
    ho = ho * kamal
    ve = ve * (kamal+1)
    while i < kamal+1:
        print ho
        if not (i == kamal):
            print ve
        i += 1
    
view rawgistfile1.txt hosted with ❤ by GitHub