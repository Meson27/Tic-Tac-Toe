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
 ### Abstraction
 

Abstraction involves hiding the complex implementation details and exposing only the necessary parts. This is done by providing a clear interface for the interaction.

**Where it's used:**
1.**Methods:** The methods like `process_move`, `toggle_player`, `is_valid_move`, and `reset_game` in TicTacToeGame provide a clear interface for manipulating the game's state without exposing the underlying data structures directly.
2.**GUI Methods:** Methods in TicTacToeBoard such as `_create_menu`, `_create_board_display`, and `_create_board_grid` abstract the complexity of creating the GUI components and provide a simple interface to interact with.

**Example**
```python
1) def toggle_player(self):
    """Return a toggled player."""
    self.current_player = next(self._players)
2) def process_move(self, move):
    """Process the current move and check if it's a win."""
    row, col = move.row, move.col
    self._current_moves[row][col] = move
    for combo in self._winning_combos:
        results = set(self._current_moves[n][m].label for n, m in combo)
        is_win = (len(results) == 1) and ("" not in results)
        if is_win:
            self._has_winner = True
            self.winner_combo = combo
            break
```

### Inhertiance

Inheritance is a mechanism where a new class inherits the properties and behaviors (methods) of an existing class.


**Where it's used:**

1.**Tkinter Inheritance:** The TicTacToeBoard class inherits from tk.Tk, which is a class provided by the Tkinter library. This allows TicTacToeBoard to inherit the functionality of a Tkinter window.

**Example**
```python
class TicTacToeBoard(tk.Tk):
    def __init__(self, game):
        super().__init__()
        self.title("Tic-Tac-Toe Game")
        self._cells = {}
        self._game = game
        self._create_menu()
        self._create_board_display()
        self._create_board_grid()
```
### Polymorphism
Polymorphism allows methods to be used interchangeably based on the object that is invoking them, enabling the same method to perform different tasks.
**Where it's used:**
1. **Method Overriding:** While this example does not explicitly override methods from parent classes, polymorphism can be seen in how different buttons (cells) in the grid react to the same `play` method call, updating based on the current player's move.

**Example**
```python
def play(self, event):
    """Handle a player's move."""
    clicked_btn = event.widget
    row, col = self._cells[clicked_btn]
    move = Move(row, col, self._game.current_player.label)
    if self._game.is_valid_move(move):
        self._update_button(clicked_btn)
        self._game.process_move(move)
        if self._game.is_tied():
            self._update_display(msg="Tied game!", color="red")
        elif self._game.has_winner():
            self._highlight_cells()
            msg = f'Player "{self._game.current_player.label}" won!'
            color = self._game.current_player.color
            self._update_display(msg, color)
        else:
            self._game.toggle_player()
            msg = f"{self._game.current_player.label}'s turn"
            self._update_display(msg)
```
### Summary
- **Encapsulation:** The code uses classes to encapsulate game logic `(TicTacToeGame)` and GUI logic `(TicTacToeBoard)`, bundling data and methods together.
- **Abstraction:** The classes provide clear interfaces through methods, hiding the complexity of their internal implementations.
- **Inheritance:** `TicTacToeBoard` inherits from `tk.Tk`, reusing and extending functionality from the Tkinter library.
- **Polymorphism:** Different GUI elements (buttons) respond differently to the same event handler (`play` method), showcasing method versatility based on the object context.







