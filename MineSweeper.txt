#include <iostream>
#include <bits/stdc++.h>
using namespace std;

//Using 'define' Preprocessor Directive to allot constant values to various level and Mines
#define EASY 1
#define NORMAL 2
#define HARD 3
#define MAXSIDE 16
#define MAXMINES 40
#define MOVESIZE 216

int SIDE ; 
int MINES ;

/*Function to check whether the enter row and column number (space) given by user are
 valid or not i.e they are within the size of board*/
bool isValid(int row, int col)
{
	return (row >= 0) && (row < SIDE) &&
		(col >= 0) && (col < SIDE);
}

//Function to check whether the chosen space has mine or not
bool mine(int row, int col, char board[][MAXSIDE])
{
	if (board[row][col] == '*')
		return (true);
	else
		return (false);
}

//Function to take input Co-ordinates from the user
void makeMove(int *x, int *y)
{
    // Take the input move
    printf("Enter your move, (row, column) -> ");
    scanf("%d %d", x, y);
    return;
}

//Function do display MineSweeper Game Board
void Board(char myBoard[][MAXSIDE])
{
	//Declaring two loop control variables in order to print rows and columns of the minesweeper board
    int i, j;
	cout<<" ";
    // Using for loop to traverse the side-row of board from it's starting space to end one and print them
	for (i=0; i<SIDE; i++)
		cout<<i;
	cout<<"\n\n";
   // Using for Loop to traverse the side-columnn of board from it's starting space to end one and print them
	for (i=0; i<SIDE; i++)
	{
		cout<<i;

		for (j=0; j<SIDE; j++)
			cout<<myBoard[i][j];
		cout<<"\n";
	}
	return;
}

/* When selected a space in the minesweeper board the selected space displays no of mines in it's vicinity
 */




// A Function to count the number of mines in the adjacent space
int countAdjacentMines(int row, int col, int mines[][2],
					char realBoard[][MAXSIDE])
{

	int i;
	int count = 0;

	// Checking all mines present in 8 spaces around the selected space
    /*      left-up  up  right up
                   \  |  /
					\ | /
                left-Space-right
					/ | \
				   /  |  \
        left down   down  right down */
    
    /* Co-ordinates:
    selected Space (x, y)
			up (x-1, y)
			down (x+1, y)
			right (x, y+1)
			left (x, y-1)
			right up (x-1, y+1)
			left up (x-1, y-1)
			right down (x+1, y+1)
            left down (x+1, y-1)
     */
     
      //Up
        if (isValid (row-1, col) == true)
        {
               if (mine (row-1, col, realBoard) == true)
               count++;
        }
 
    // Down
        if (isValid (row+1, col) == true)
        {
               if (mine (row+1, col, realBoard) == true)
               count++;
        }
 
    // Right
        if (isValid (row, col+1) == true)
        {
            if (mine (row, col+1, realBoard) == true)
               count++;
        }
 
    //Left
        if (isValid (row, col-1) == true)
        {
               if (mine (row, col-1, realBoard) == true)
               count++;
        }
 
    // Right-Up
        if (isValid (row-1, col+1) == true)
        {
            if (mine (row-1, col+1, realBoard) == true)
               count++;
        }
 
     // Left-Up
        if (isValid (row-1, col-1) == true)
        {
             if (mine (row-1, col-1, realBoard) == true)
               count++;
        }
 
  // Right-Down
        if (isValid (row+1, col+1) == true)
        {
               if (mine (row+1, col+1, realBoard) == true)
               count++;
        }
 
    // Left-Down
        if (isValid (row+1, col-1) == true)
        {
            if (mine (row+1, col-1, realBoard) == true)
               count++;
        }
     
	return (count);
}

// A Recursive Function to play the Minesweeper Game
bool playMinesweeperUtil(char myBoard[][MAXSIDE], char realBoard[][MAXSIDE],
			int mines[][2], int row, int col, int *movesLeft)
{

	// Base Case of Recursion
	if (myBoard[row][col] != '-')
		return (false);

	int i, j;

	// When opened a mine You are going to lose
	if (realBoard[row][col] == '*')
	{
		myBoard[row][col]='*';

		for (i=0; i<MINES; i++)
			myBoard[mines[i][0]][mines[i][1]]='*';

		Board (myBoard);
		cout<<"\nYou lost!\n";
		return (true) ;
	}

	else
	{
		// Calculate the number of adjacent mines and put it on the board
		int count = countAdjacentMines(row, col, mines, realBoard);
		(*movesLeft)--;

		myBoard[row][col] = count + '0';

		if (!count)
		{
			

			// Up
			if (isValid (row-1, col) == true)
			{
				if (mine (row-1, col, realBoard) == false)
				playMinesweeperUtil(myBoard, realBoard, mines, row-1, col, movesLeft);
			}

			// Down
			if (isValid (row+1, col) == true)
			{
				if (mine (row+1, col, realBoard) == false)
					playMinesweeperUtil(myBoard, realBoard, mines, row+1, col, movesLeft);
			}

			// Right
			if (isValid (row, col+1) == true)
			{
				if (mine (row, col+1, realBoard) == false)
					playMinesweeperUtil(myBoard, realBoard, mines, row, col+1, movesLeft);
			}

			// Left
			if (isValid (row, col-1) == true)
			{
				if (mine (row, col-1, realBoard) == false)
					playMinesweeperUtil(myBoard, realBoard, mines, row, col-1, movesLeft);
			}

			// Right-Up
			if (isValid (row-1, col+1) == true)
			{
				if (mine (row-1, col+1, realBoard) == false)
					playMinesweeperUtil(myBoard, realBoard, mines, row-1, col+1, movesLeft);
			}

			//Left-Up
			if (isValid (row-1, col-1) == true)
			{
				if (mine (row-1, col-1, realBoard) == false)
					playMinesweeperUtil(myBoard, realBoard, mines, row-1, col-1, movesLeft);
			}

			// Right-Down
			if (isValid (row+1, col+1) == true)
			{
				if (mine (row+1, col+1, realBoard) == false)
					playMinesweeperUtil(myBoard, realBoard, mines, row+1, col+1, movesLeft);
			}

			// Left-Down
			if (isValid (row+1, col-1) == true)
			{
				if (mine (row+1, col-1, realBoard) == false)
					playMinesweeperUtil(myBoard, realBoard, mines, row+1, col-1, movesLeft);
			}
		}

		return (false);
	}
}

// A Function to place the mines randomly on the board
void placeMines(int mines[][2], char realBoard[][MAXSIDE])
{
	bool mark[MAXSIDE*MAXSIDE];

	memset (mark, false, sizeof (mark));

	// Continue until all random mines have been created.
	for (int i=0; i<MINES; )
	{
		int random = rand() % (SIDE*SIDE);
		int x = random / SIDE;
		int y = random % SIDE;

		// Add the mine if no mine is placed at this position on the board
		if (mark[random] == false)
		{
			// Row Index of the Mine
			mines[i][0]= x;
			// Column Index of the Mine
			mines[i][1] = y;

			// Place the mine
			realBoard[mines[i][0]][mines[i][1]] = '*';
			mark[random] = true;
			i++;
		}
	}

	return;
}

// A Function to initialise the game
void initialise(char realBoard[][MAXSIDE], char myBoard[][MAXSIDE])
{
	// Initiate the random number generator so that the same configuration doesn't arises
	srand(time (NULL));

	// Assign all the cells as mine-free
	for (int i=0; i<SIDE; i++)
	{
		for (int j=0; j<SIDE; j++)
		{
			myBoard[i][j] = realBoard[i][j] = '-';
		}
	}

	return;
}

// A function to replace the mine from (row, col) and put it to a vacant space
void replaceMine (int row, int col, char board[][MAXSIDE])
{
	for (int i=0; i<SIDE; i++)
	{
		for (int j=0; j<SIDE; j++)
			{
				// Find the first location in the board which is not having a mine and put a mine there.
				if (board[i][j] != '*')
				{
					board[i][j] = '*';
					board[row][col] = '-';
					return;
				}
			}
	}
	return;
}

// A Function to play Minesweeper game
void playMinesweeper ()
{
	// Initially the game is not over
	bool gameOver = false;

	// Actual Board and My Board
	char realBoard[MAXSIDE][MAXSIDE], myBoard[MAXSIDE][MAXSIDE];

	int movesLeft = SIDE * SIDE - MINES, x, y;
	int mines[MAXMINES][2]; // stores (x,y) coordinates of all mines.

	initialise (realBoard, myBoard);

	// Place the Mines randomly
	placeMines (mines, realBoard);

	// You are in the game until you have not opened a mine So keep playing untill you hit one

	int currentMoveIndex = 0;
	while (gameOver == false)
	{
		cout<<"---------------------------------------------------------\n";
        cout<<"\n\nCurrent Status of Board : \n\n";
		Board (myBoard);
		makeMove (&x, &y);

		// This is to guarantee that the first move is always safe
		// If it is the first move of the game
		if (currentMoveIndex == 0)
		{
			// If the first move itself is a mine then we remove the mine from that location
			if (mine (x, y, realBoard) == true)
				replaceMine (x, y, realBoard);
		}
		currentMoveIndex ++;
		gameOver = playMinesweeperUtil (myBoard, realBoard, mines, x, y, &movesLeft);

		if ((gameOver == false) && (movesLeft == 0))
		{
			cout<<"\nYou won!\n";
			gameOver = true;
		}
	}
	return;
}

// A Function to choose the difficulty level of the game
void chooseDifficultyLevel ()
{
// Declaring a variable to store difficulty level option
	int level;
    cout<<"                           -MINESWEEPER GAME!-"<<endl;
    cout<<"__________________________________________________________________________";

	cout<<"\n                 Enter the Difficulty Level\n\n\n\n\n";
	cout<<"1. EASY Level     - 6 * 6 Board and 7 Mines\n";
	cout<<"2. NORMAL Level   - 12 * 12 Cells and 20 Mines\n";
	cout<<"3. HARD Level     - 16 * 16 Board and 40 Mines\n\n\n";
	cin>>level;
	if (level == EASY)
	{
		SIDE = 6;
		MINES = 7;
	}
	if (level == NORMAL)
	{
		SIDE = 12;
		MINES = 20;
	}
	if (level == HARD)
	{
		SIDE = 16;
		MINES = 40;
	}
	return;
}


int main()
{
	chooseDifficultyLevel ();
	playMinesweeper ();
	return (0);
}
