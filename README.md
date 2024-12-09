# FOCP-Assignment-6

ASSIGNMENT -6
TIC TAC TOE
#include <stdio.h>
#include <stdlib.h>
void printBoard(char board[3][3]);
int checkWin(char board[3][3]);
int isFull(char board[3][3]);
int main() {
   char board[3][3] = {
       {'1', '2', '3'},
       {'4', '5', '6'},
       {'7', '8', '9'}
   };
   int turn = 1;
   int move, row, col, winner = 0;
   printf("Welcome to Tic Tac Toe!\n");
   printf("Player 1: O | Player 2: X\n\n");
   while (!winner && !isFull(board)) {
       printBoard(board);
       printf("Player %d's turn. Enter your move (1-9): ", turn);
       scanf("%d", &move);
       row = (move - 1) / 3;
       col = (move - 1) % 3;
 
       if (move < 1 || move > 9 || board[row][col] == 'O' || board[row][col] == 'X') {
           printf("Invalid move! Try again.\n");
           continue;
       }
       board[row][col] = (turn == 1) ? 'O' : 'X';
       winner = checkWin(board);
       turn = (turn == 1) ? 2 : 1;
   }
 
   printBoard(board);
 
   if (winner) {
       printf("Player %d wins!\n", (turn == 1) ? 2 : 1);
   } else {
       printf("It's a tie!\n");
   }
 
   return 0;
}
void printBoard(char board[3][3]) {
   printf("\n");
   for (int i = 0; i < 3; i++) {
       for (int j = 0; j < 3; j++) {
           printf(" %c ", board[i][j]);
           if (j < 2) printf("|");
       }
       printf("\n");
       if (i < 2) printf("---+---+---\n");
   }
   printf("\n");
}
int checkWin(char board[3][3]) {
   for (int i = 0; i < 3; i++) {
       if (board[i][0] == board[i][1] && board[i][1] == board[i][2]) return 1;//Row
       if (board[0][i] == board[1][i] && board[1][i] == board[2][i]) return 1; // Column
   }
   if (board[0][0] == board[1][1] && board[1][1] == board[2][2]) return 1; // Diagonal
   if (board[0][2] == board[1][1] && board[1][1] == board[2][0]) return 1;
 
   return 0;
}
int isFull(char board[3][3]) {
   for (int i = 0; i < 3; i++) {
       for (int j = 0; j < 3; j++) {
           if (board[i][j] != 'O' && board[i][j] != 'X') return 0;
       }
   }
   return 1;
}
