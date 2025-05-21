Tic Tac Toe Draw Solutions  
Exercise 27
This exercise is Part 3 of 4 of the Tic Tac Toe exercise series. The other exercises are: Part 1, Part 2, and Part 4.

In a previous exercise we explored the idea of using a list of lists as a “data structure” to store information about a tic tac toe game. In a tic tac toe game, the “game server” needs to know where the Xs and Os are in the board, to know whether player 1 or player 2 (or whoever is X and O won).

There has also been an exercise about drawing the actual tic tac toe gameboard using text characters.

The next logical step is to deal with handling user input. When a player (say player 1, who is X) wants to place an X on the screen, they can’t just click on a terminal. So we are going to approximate this clicking simply by asking the user for a coordinate of where they want to place their piece.

As a reminder, our tic tac toe game is really a list of lists. The game starts out with an empty game board like this:

game = [[0, 0, 0],
	[0, 0, 0],
	[0, 0, 0]]
The computer asks Player 1 (X) what their move is (in the format row,col), and say they type 1,3. Then the game would print out

game = [[0, 0, X],
	[0, 0, 0],
	[0, 0, 0]]
And ask Player 2 for their move, printing an O in that place.

Things to note:

For this exercise, assume that player 1 (the first player to move) will always be X and player 2 (the second player) will always be O.
Notice how in the example I gave coordinates for where I want to move starting from (1, 1) instead of (0, 0). To people who don’t program, starting to count at 0 is a strange concept, so it is better for the user experience if the row counts and column counts start at 1. This is not required, but whichever way you choose to implement this, it should be explained to the player.
Ask the user to enter coordinates in the form “row,col” - a number, then a comma, then a number. Then you can use your Python skills to figure out which row and column they want their piece to be in.
Don’t worry about checking whether someone won the game, but if a player tries to put a piece in a game position where there already is another piece, do not allow the piece to go there.
Bonus:

For the “standard” exercise, don’t worry about “ending” the game - no need to keep track of how many squares are full. In a bonus version, keep track of how many squares are full and automatically stop asking for moves when there are no more valid moves.
Sample solutions
Here is one solution that does not fully complete the exercise, but gives a bit of food for thought. The drawboard function is a general function that can be used to draw the game board with any given inputs.

def drawboard(board):
    print ('    |   |   ')
    print ('' +board[6]+ '    | ' +board[7]+ '  |   ' +board[8] )
    print ('    |   |   ')
    print ('---------------')
    print ('    |   |   ')
    print ('' +board[3]+ '    | ' +board[4]+ '  | ' +board[5] )
    print ('    |   |   ')
    print('-----------------')
    print ('    |   |   ')
    print ('' +board[0]+ '    | ' +board[1]+ '  |' +board[2] )
    print ('    |   |   ')

drawboard(['', '', '', '', '', '', '', '', ''])
view rawtictactoe.py hosted with ❤ by GitHub
Another solution uses lots of functions, and also checks whether the game has ended!

# Python Exercises http://www.practicepython.org/
# Exercise 27 - Tic Tac Toe Draw
# Exercise to draw Tic Tac Toe gameboard the game board getting input from Player 1 and Player 2
# Last updated: 17/02/2016
#
# - gets input from two players
# - checks the input for correctness: row,col
# - exits if board is full or there is a winner


# initialise the game board
gameboard = [(['.']*3) for i in range(3)]

# variables for input and turn count
row_col = [0]
turn = 1

# checks that the input is valid 
# - that it is in the format "row,col"
# - that the position is free
def input_valid(values):
	# input has only two values
    if len(values) != 2:
        print "Input must be two numbers in format row,col e.g.  1,2 "
        return 0
    # input is a number between 1 and 3 (inclusive)
    try:
        if (1 <= int(values[0]) <= 3) and (1 <= int(values[1]) <= 3):
            # checks if the position on the board is alreay filled
            if gameboard[int(values[0])-1][int(values[1])-1] != '.':
                print "Position on board already taken."
                return 0
            return 1
        else:
            print "Input values must be numbers between 1 and 3 (inclusive)"
            return 0
    except ValueError:
        print "Input values must be numbers between 1 and 3 (inclusive)"
        return 0


# draw the board
def draw_board(values, player):
    # changes the value to X or O
    gameboard[int(values[0])-1][int(values[1])-1]=player

    # print the gameboard
    for row in gameboard:
	print row

# calculate if game is over (no more '.' or has winner)
def game_over():
    searcht = '.'
    
    # check win by row
    for i in range(3):
        if len(set(gameboard[i])) == 1:
            if gameboard[i][1] == '.':
                continue
            elif gameboard[i][1] == 'X':
                print "Game over - Player 1 wins"
            #elif gameboard[i][1] == 'O':
            else:
                print "Game over - Player 2 wins"
            return 1

    # check win by column
    for i in range(3):
        if gameboard[0][i] == gameboard[1][i] == gameboard[2][i]:
            if gameboard[0][i] == '.':
                continue
            elif gameboard[0][i] == 'X':
                print "Game over - Player 1 wins"
            else:
                print "Game over - Player 2 wins"
            return 1

    # check win by diagonal
    if (gameboard[0][0] == gameboard[1][1] == gameboard[2][2]) or (gameboard[0][2] == gameboard[1][1] == gameboard[2][0]): 
        if gameboard[1][1] == 'X':
            print "Game over - Player 1 wins"
        elif gameboard[1][1] == 'O':
            print "Game over - Player 2 wins"
        else:
            return 0
        return 1

    # check board is full
    for sublist in gameboard:
        if searcht in sublist:
            return 0

    print "Game over - the board is filled"
    return 1




# main function that runs the game while board is not full
while not game_over():
    piece = '.'

    # Player input - checks for input correctness
    while not input_valid(row_col):
        player = turn % 2
        if player == 0:
         	player = 2
          	piece = 'O'
        else:
            piece = 'X'
        p1 = raw_input('Player ' + str(player) +' input: ')
        row_col = p1.split(",")

    draw_board(row_col, piece)

    row_col = [0]
    turn += 1

view rawgistfile1.txt hosted with ❤ by GitHub