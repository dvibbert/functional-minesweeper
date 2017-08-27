# FunctionalMinesweeper
A Minesweeper game implemented in F# for Dallas Functional Dojo. My intention is to learn functional concepts, not necessarily complete the game.

I used https://github.com/kmc059000/minesweeper-fs as the basis for my UI. I liked how the console application looked and it saved me from doing UI work that did not interest me.

I used the minesweeper rules at https://zyxyvy.wordpress.com/2012/08/11/the-rules-of-minesweeper/, including:

> The grid of mines for a board is pre-generated before the start of the game. The first square clicked never contains a mine. If it did contain a mine in the board pre-generation, the mine is moved to the upper-left hand corner of the board, and if that was a mine, the next square over to the right, and so on.

# Domain Vocabulary
**Board** The game playing area. A rectangular grid of squares

**Square** A cell on the board. They contain one of the following:
    **Mine** A square containing a mine. Unsafe to open
	**Number** A square adjacent to one or more mines. The number represents the count of neighboring squares that are mines
	**Blank** A square that is not adjacent to any mines

**Open** Reveal the contents of a sqaure
    These are tied too closely to the UI, but they are the domain expert's terms
    **Left-Click** Open a single square
    **Chord** Open the unflagged neighbors of a opened square
	    If the selected square is not open, do nothing
		If the count of flagged neighboring squares is not equal to the selected square's number, do nothing

**Flag**
    Mark an unopened, unflagged square as a mine
	Alternately, remove a flag on a flagged square

**Mines Left** A counter of mines to be flagged
    Equal to starting mines minus flagged squares
	Not used to determine if a game is won

**Difficulty** Standard board layouts with dimensions and mine counts
    **Beginner** 8x8 with 10 mines
	**Intermediate** 16x16 with 40 mines
	**Expert** 16x30 with 99 mines

**End-of-Game**
    **Lose** Open a square containing a mine
	    Show opened square(s) that caused the loss
		Open all squares with mines
		Show the total time since the first click
	**Win** Open all non-mine squares
	    Show the total time since the first click
