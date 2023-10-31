# Minesweeper Game in C++
This repository contains a classic implementation of the Minesweeper game using the C++ programming language. The game allows players to navigate a minefield, strategically flagging mines and uncovering safe tiles. It features different difficulty levels, including easy, normal, and hard, with varying board sizes and mine distributions.


## Code Structure

- `main.cpp`: The main source code file containing the game logic and user interface.
- `Board()`: Function to display the Minesweeper game board.
- `makeMove()`: Function to take input coordinates from the user.
- `mine()`: Function to check if a selected space has a mine.
- `countAdjacentMines()`: Function to count the number of mines in adjacent spaces.
- `playMinesweeperUtil()`: Recursive function to play the Minesweeper game.
- `placeMines()`: Function to randomly place mines on the board.
- `initialise()`: Function to initialize the game board and mine placement.
- `replaceMine()`: Function to replace a mine from a given location and put it in a vacant space.
- `chooseDifficultyLevel()`: Function to select the difficulty level of the game.
- `playMinesweeper()`: Function to start the Minesweeper game.

## Usage

1. Choose the difficulty level of the game (easy, normal, or hard).
2. The game board will be displayed, initially showing all hidden tiles.
3. Enter your moves by providing the row and column numbers.
4. If you uncover a mine, you lose the game.
5. If you successfully uncover all non-mine tiles, you win the game.

Feel free to explore the code and enhance the game with additional features or optimizations.
