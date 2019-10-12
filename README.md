# Minesweeper
  A minsweeper clone made for the CLI for OOPL Mini-Project.

# Features
 - Randomly places mines on a grid.
 - Let's user flag and mark boxes.
 
# ADT for  Class Field
 Box of the grid which has the contents of the  box
```C++
enum fieldValues : byte { OPEN, CLOSED = 10, MINE, UNKNOWN, FLAG, ERR };
class FieldData
{
public:
	FieldData() : value(CLOSED), open(false) {}
	byte value;
	bool open, mine;
};
```
# ADT for Class Game
Builds the grid and has the contents of the game.

```C++
class Game
{
        int wid, hei, mMines, oMines;
	FieldData* field; bool go;
	int graphs[6];
private:
        void makeMove(int x, int y, string a);
        bool openCell(int x, int y);
        void drawBoard();
        void checkWin();
        void boom();
        void lastMsg(string s);
        bool isInside(int x, int y);
        void recOpen(int x, int y);
        int getMineCount(int x, int y);
public:
	~Game(){
		if (field) delete[] field;
	}

	Game(int x, int y){
		go = false; wid = x; hei = y;
		field = new FieldData[x * y];
		memset(field, 0, x * y * sizeof(FieldData));
		oMines = ((22 - rand() % 11) * x * y) / 100;
		mMines = 0;
		int mx, my, m = 0;
		for (; m < oMines; m++)
		{
			do
			{
				mx = rand() % wid; my = rand() % hei;
			} while (field[mx + wid * my].mine);
			field[mx + wid * my].mine = true;
		}
		graphs[0] = ' '; graphs[1] = '.'; graphs[2] = '*';
		graphs[3] = '?'; graphs[4] = '!'; graphs[5] = 'X';
	}
 };
```
