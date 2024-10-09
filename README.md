# Tic-Tac-Toe-Game
TIC TAC TOE game using python
import tkinter as tk
from tkinter import messagebox

class TicTacToe:
    def __init__(self, master):
        self.master = master
        master.title("Tic Tac Toe")

        self.current_player = "X"
        self.board = [""] * 9
        self.buttons = []

        for i in range(3):
            row = []
            for j in range(3):
                button = tk.Button(master, text="", font=("Arial", 24), width=5, height=2,
                                   command=lambda i=i, j=j: self.make_move(i, j))
                button.grid(row=i, column=j)
                row.append(button)
            self.buttons.append(row)

    def make_move(self, i, j):
        index = i * 3 + j
        if self.board[index] == "" and not self.check_winner():
            self.board[index] = self.current_player
            self.buttons[i][j].config(text=self.current_player)
            if self.check_winner():
                messagebox.showinfo("Game Over", f"Player {self.current_player} wins!")
            elif "" not in self.board:
                messagebox.showinfo("Game Over", "It's a tie!")
            else:
                self.current_player = "O" if self.current_player == "X" else "X"

    def check_winner(self):
        winning_combinations = [
            (0, 1, 2), (3, 4, 5), (6, 7, 8),  # Rows
            (0, 3, 6), (1, 4, 7), (2, 5, 8),  # Columns
            (0, 4, 8), (2, 4, 6)              # Diagonals
        ]
        for a, b, c in winning_combinations:
            if self.board[a] == self.board[b] == self.board[c] != "":
                return True
        return False

if __name__ == "__main__":
    root = tk.Tk()
    game = TicTacToe(root)
    root.mainloop()
