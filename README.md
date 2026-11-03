<h1>ExpNo 7 : Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>Name: ARAVIND P </h3>
<h3>Register Number: 212224240015  </h3>
<H3>Aim:</H3>
<p>
Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game
</p>
<h1>GOALS of Alpha-Beta Pruning in MiniMax Search Algorithm</h1>

<h3>Improve the decision-making efficiency of the computer player by reducing the number of evaluated nodes in the game tree.</h3>
<h3>Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning and the Minimax algorithm with Python Code.</h3>
<h1>IMPLEMENTATION</h1>

The project involves developing a Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning with the Minimax algorithm. Using this algorithm, the computer player analyzes the game state, evaluates possible moves, and selects the optimal action based on the anticipated outcomes.

<h1>The Minimax algorithm</h1>

recursively evaluates all possible moves and their potential outcomes, creating a game tree.

<h1>Alpha-Beta pruning</h1>

Alpha–Beta (𝛼−𝛽) algorithm is actually an improved minimax using a heuristic. It stops evaluating a move when it makes sure that it’s worse than a previously examined move. Such moves need not to be evaluated further.

When added to a simple minimax algorithm, it gives the same output but cuts off certain branches that can’t possibly affect the final decision — dramatically improving the performance
<hr>
<h2>Sample Input and Output:</h2>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8d5e329a-9aff-41a6-bcf0-46efa10e1b92)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/438b242d-54ba-443e-b040-a936e6ae3b55)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/99a33390-fa11-4ade-a19f-e93bcd7aaec9)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/440797bd-53cb-49c1-b18d-89776864c3e7)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/81575a16-26b2-46f1-a8ac-27c9ed0a0fe5)

## PROGRAM:
```python

import time


class TicTacToe:
    def __init__(self):
        self.board = [['.' for _ in range(3)] for _ in range(3)]

    def draw_board(self):
        print('  X 0 1 2')
        for y in range(3):
            print('Y {} {}'.format(y, ' '.join(self.board[y])))
        print()

    def winner(self):
        lines = []
        lines.extend(self.board)
        lines.extend([[self.board[y][x] for y in range(3)] for x in range(3)])
        lines.append([self.board[i][i] for i in range(3)])
        lines.append([self.board[i][2 - i] for i in range(3)])

        for line in lines:
            if line[0] != '.' and line[0] == line[1] == line[2]:
                return line[0]
        if all(cell != '.' for row in self.board for cell in row):
            return 'tie'
        return None

    def minimax(self, player):
        result = self.winner()
        if result == 'X':
            return -1, None
        if result == 'O':
            return 1, None
        if result == 'tie':
            return 0, None

        best_score = -2 if player == 'O' else 2
        best_move = None
        for y in range(3):
            for x in range(3):
                if self.board[y][x] == '.':
                    self.board[y][x] = player
                    score, _ = self.minimax('X' if player == 'O' else 'O')
                    self.board[y][x] = '.'
                    if ((player == 'O' and score > best_score) or
                            (player == 'X' and score < best_score)):
                        best_score = score
                        best_move = (x, y)
        return best_score, best_move

    def play(self):
        while True:
            self.draw_board()
            result = self.winner()
            if result is not None:
                if result == 'tie':
                    print("It's a tie!")
                else:
                    print('The winner is {}!'.format(result))
                break

            start = time.time()
            _, recommended = self.minimax('X')
            elapsed = time.time() - start
            print('Evaluation time: {}s'.format(round(elapsed, 7)))
            print('Recommended move: X = {}, Y = {}'.format(
                recommended[0], recommended[1]))

            while True:
                try:
                    x = int(input('Enter X (0-2): '))
                    y = int(input('Enter Y (0-2): '))
                    if 0 <= x <= 2 and 0 <= y <= 2 and self.board[y][x] == '.':
                        self.board[y][x] = 'X'
                        break
                    print('That square is unavailable. Try again.')
                except ValueError:
                    print('Enter whole numbers from 0 to 2.')

            if self.winner() is not None:
                continue

            _, computer_move = self.minimax('O')
            self.board[computer_move[1]][computer_move[0]] = 'O'


if __name__ == '__main__':
    TicTacToe().play()


```
## OUTPUT:
<img width="767" height="760" alt="684614977-f661d250-6e76-4933-9f0b-7b011629a66f" src="https://github.com/user-attachments/assets/32135782-e526-4fff-8a3f-2a03482a7b3d" />

## RESULT:
Thus, the program was executed successfully.
