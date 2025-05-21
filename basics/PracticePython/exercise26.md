Check Tic Tac Toe Solutions  
Exercise 26
This exercise is Part 2 of 4 of the Tic Tac Toe exercise series. The other exercises are: Part 1, Part 3, and Part 4.

As you may have guessed, we are trying to build up to a full tic-tac-toe board. However, this is significantly more than half an hour of coding, so we’re doing it in pieces.

Today, we will simply focus on checking whether someone has WON a game of Tic Tac Toe, not worrying about how the moves were made.

If a game of Tic Tac Toe is represented as a list of lists, like so:

game = [[1, 2, 0],
	[2, 1, 0],
	[2, 1, 1]]
where a 0 means an empty square, a 1 means that player 1 put their token in that space, and a 2 means that player 2 put their token in that space.

Your task this week: given a 3 by 3 list of lists that represents a Tic Tac Toe game board, tell me whether anyone has won, and tell me which player won, if any. A Tic Tac Toe win is 3 in a row - either in a row, a column, or a diagonal. Don’t worry about the case where TWO people have won - assume that in every board there will only be one winner.

Here are some more examples to work with:

winner_is_2 = [[2, 2, 0],
	[2, 1, 0],
	[2, 1, 1]]

winner_is_1 = [[1, 2, 0],
	[2, 1, 0],
	[2, 1, 1]]

winner_is_also_1 = [[0, 1, 0],
	[2, 1, 0],
	[2, 1, 1]]

no_winner = [[1, 2, 0],
	[2, 1, 0],
	[2, 1, 2]]

also_no_winner = [[1, 2, 0],
	[2, 1, 0],
	[2, 1, 0]]
Sample solutions
There were many strategies for approaching this problem. The important part is to be careful about checking rows, columns, and diagonals for winners. Things like making sure that a row of 0, 0, 0 doesn’t win with player number 0 is important, and making sure to count the columns and rows at the edges.

A few submitted solutions are below - feel free to comment if you think you have a better one, and I’ll put it up here!

Not using too many functions, but using the numpy library to transpose the game board, turning column-checking into row-checking.
import numpy
game = [
[2,2,1],
[1,1,2],
[1,2,1]]
set_r = ()
set_c = ()
def line_match(game):
	for i in range(3):
		set_r = set(game[i])
		if len(set_r) == 1 and game[i][0] != 0:
			return game[i][0]
	return 0
#transposed column function for future use
#def column(game):
#	trans = numpy.transpose(game)
#	for i in range(3):
#		set_r = set(trans[i])
#		if len(set_r) == 1 and trans[i][0] != 0:
#			return list(set_r)[0]

def diagonal_match(game):
	if game[1][1] != 0:
		if game[1][1] == game[0][0] == game[2][2]: 
			return game[1][1]
		elif game[1][1] == game[0][2] == game[2][0]:
			return game[1][1]			
	return 0
if line_match(game) > 0:			
	print (str(line_match(game)) + str(" row wins!"))
if line_match(numpy.transpose(game)) > 0:
	print (str(line_match(numpy.transpose(game))) + str(" column wins!"))
if diagonal_match(game) > 0:
	print (str(diagonal_match(game)) + str(" diagonal wins!"))
view rawtic_tac_toe_check.py hosted with ❤ by GitHub
Using set() to simplify the counting.
def checkGrid(grid):
	# rows
	for x in range(0,3):
		row = set([grid[x][0],grid[x][1],grid[x][2]])
		if len(row) == 1 and grid[x][0] != 0:
			return grid[x][0]

	# columns
	for x in range(0,3):
		column = set([grid[0][x],grid[1][x],grid[2][x]])
		if len(column) == 1 and grid[0][x] != 0:
			return grid[0][x]

	# diagonals
	diag1 = set([grid[0][0],grid[1][1],grid[2][2]])
	diag2 = set([grid[0][2],grid[1][1],grid[2][0]])
	if len(diag1) == 1 or len(diag2) == 1 and grid[1][1] != 0:
		return grid[1][1]

	return 0

winner_is_2 = [[2, 2, 0],
	[2, 1, 0],
	[2, 1, 1]]
winner_is_1 = [[1, 2, 0],
	[2, 1, 0],
	[2, 1, 1]]

winner_is_also_1 = [[0, 1, 0],
	[2, 1, 0],
	[2, 1, 1]]

no_winner = [[1, 2, 0],
	[2, 1, 0],
	[2, 1, 2]]

also_no_winner = [[1, 2, 0],
	[2, 1, 0],
	[2, 1, 0]]

print(checkGrid(also_no_winner))
view rawtictactoecheck.py hosted with ❤ by GitHub