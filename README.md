<h1>ExpNo 5 : Implement Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>Name:           </h3>
<h3>Register Number/Staff Id:          </h3>
<h3>Name: VARSHA A </h3>
<h3>Register Number/Staff Id: 212223220121 </h3>
<H3>Aim:</H3>
<p>
    Implement Minimax Search Algorithm for a Simple TIC-TAC-TOE game
@@ -111,6 +111,125 @@ end
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/a8a27e2a-6fd4-46a2-afb5-6d27b8556702)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/a2acb6a1-ed8e-42e5-8968-fe805e4b0255)

<h2>Program:</h2>

```
import time
class TicTacToe:
    def __init__(self):
        self.initialize_game()
    def initialize_game(self):
        # 3x3 board
        self.board = [['.' for _ in range(3)] for _ in range(3)]
        self.player_turn = 'X'  # Human always plays first
    def draw_board(self):
        for row in self.board:
            print(" | ".join(row))
        print()
    def is_valid(self, x, y):
        return 0 <= x < 3 and 0 <= y < 3 and self.board[x][y] == '.'
    def is_end(self):
        for i in range(3):
            if self.board[i][0] == self.board[i][1] == self.board[i][2] != '.':
                return self.board[i][0]
            if self.board[0][i] == self.board[1][i] == self.board[2][i] != '.':
                return self.board[0][i]
        if self.board[0][0] == self.board[1][1] == self.board[2][2] != '.':
            return self.board[0][0]
        if self.board[0][2] == self.board[1][1] == self.board[2][0] != '.':
            return self.board[0][2]
        for row in self.board:
            if '.' in row:
                return None  
        return '.'  
    def max(self):
        maxv = -2
        px = None
        py = None
        result = self.is_end()
        if result == 'X': return (-1, 0, 0)
        if result == 'O': return (1, 0, 0)
        if result == '.': return (0, 0, 0)
        for i in range(3):
            for j in range(3):
                if self.board[i][j] == '.':
                    self.board[i][j] = 'O'
                    (m, _, _) = self.min()
                    if m > maxv:
                        maxv = m
                        px, py = i, j
                    self.board[i][j] = '.'
        return (maxv, px, py)
    def min(self):
        minv = 2
        qx = None
        qy = None
        result = self.is_end()
        if result == 'X': return (-1, 0, 0)
        if result == 'O': return (1, 0, 0)
        if result == '.': return (0, 0, 0)
        for i in range(3):
            for j in range(3):
                if self.board[i][j] == '.':
                    self.board[i][j] = 'X'
                    (m, _, _) = self.max()
                    if m < minv:
                        minv = m
                        qx, qy = i, j
                    self.board[i][j] = '.'
        return (minv, qx, qy)
    def play(self):
        while True:
            self.draw_board()
            result = self.is_end()
            if result is not None:
                if result == 'X':
                    print("You win!")
                elif result == 'O':
                    print("AI wins!")
                else:
                    print("It's a tie!")
                self.initialize_game()
                return
            if self.player_turn == 'X':
                # Human turn
                while True:
                    try:
                        px = int(input("Enter row (0-2): "))
                        py = int(input("Enter col (0-2): "))
                    except ValueError:
                        print("Enter valid integers 0-2")
                        continue
                    if self.is_valid(px, py):
                        self.board[px][py] = 'X'
                        self.player_turn = 'O'
                        break
                    else:
                        print("Invalid move, try again.")
            else:
                # AI turn
                print("AI is making a move...")
                start = time.time()
                _, px, py = self.max()
                end = time.time()
                print(f"AI move: row={px}, col={py}, evaluation time: {round(end-start, 7)}s")
                self.board[px][py] = 'O'
                self.player_turn = 'X'
def main():
    game = TicTacToe()
    game.play()
if __name__ == "__main__":
    main()
```
<h2>Output:</h2>
<img width="587" height="466" alt="image" src="https://github.com/user-attachments/assets/cfb9ed9a-26c6-480e-905c-fd378971f7b5" />
<hr>
<h2>Result:</h2>
<p>Thus,Implementation of  Minimax Search Algorithm for a Simple TIC-TAC-TOE game wasa done successfully.</p>
Footer
