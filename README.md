# Tic Tac Toe Game

A Tic Tac Toe game built with Python and Tkinter.

## Overview

This project is a graphical Tic Tac Toe game implemented using Python and the Tkinter library for the GUI. The game allows two players to play against each other, and it visually displays the game state and the winner.

## Object-Oriented Programming Principles

### Encapsulation

Encapsulation refers to bundling the data (attributes) and methods (functions) that operate on the data into a single unit, or class, and restricting access to some of the object's components.

**Where it's used:**
1. **Classes and Methods:** 
   - `TicTacToeGame` class encapsulates the logic of the game, including setting up the board, checking for winning combinations, processing moves, and toggling players.
   - `TicTacToeBoard` class encapsulates the graphical user interface (GUI) logic using Tkinter. It handles the creation of the board grid, display updates, and user interactions.
   - The `Player` and `Move` classes (using `NamedTuple`) encapsulate the attributes related to the players and moves respectively.

**Example:**
```python
class TicTacToeGame:
    def __init__(self, players=DEFAULT_PLAYERS, board_size=BOARD_SIZE):
        self._players = cycle(players)
        self.board_size = board_size
        self.current_player = next(self._players)
        self.winner_combo = []
        self._current_moves = []
        self._has_winner = False
        self._winning_combos = []
        self._setup_board()
```

efggg

