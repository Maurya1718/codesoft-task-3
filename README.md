# codesoft-task-3
tas#include <iostream>
#include <vector>
#include <string>

using namespace std;

// Function to draw the Tic Tac Toe board
void drawBoard(const vector<vector<char>>& board) {
    cout << "  1 2 3" << endl;
    cout << " +-+-+-+" << endl;
    for (int i = 0; i < 3; ++i) {
        cout << i + 1 << "|";
        for (int j = 0; j < 3; ++j) {
            cout << board[i][j] << "|";
        }
        cout << endl;
        cout << " +-+-+-+" << endl;
    }
}

// Function to check if the move is valid
bool isValidMove(const vector<vector<char>>& board, int row, int col) {
    return (row >= 0 && row < 3 && col >= 0 && col < 3 && board[row][col] == ' ');
}

// Function to check if the game is over
bool isGameOver(const vector<vector<char>>& board, char& winner) {
    // Check rows
    for (int i = 0; i < 3; ++i) {
        if (board[i][0] != ' ' && board[i][0] == board[i][1] && board[i][0] == board[i][2]) {
            winner = board[i][0];
            return true;
        }
    }

    // Check columns
    for (int j = 0; j < 3; ++j) {
        if (board[0][j] != ' ' && board[0][j] == board[1][j] && board[0][j] == board[2][j]) {
            winner = board[0][j];
            return true;
        }
    }

    // Check diagonals
    if (board[0][0] != ' ' && board[0][0] == board[1][1] && board[0][0] == board[2][2]) {
        winner = board[0][0];
        return true;
    }
    if (board[0][2] != ' ' && board[0][2] == board[1][1] && board[0][2] == board[2][0]) {
        winner = board[0][2];
        return true;
    }

    // Check if the board is full
    for (int i = 0; i < 3; ++i) {
        for (int j = 0; j < 3; ++j) {
            if (board[i][j] == ' ') {
                return false; // If there's an empty space, game is not over
            }
        }
    }
    // If the board is full and no winner, it's a tie
    winner = 'T';
    return true;
}

int main() {
    vector<vector<char>> board(3, vector<char>(3, ' ')); // Initialize an empty board
    int row, col;
    char currentPlayer = 'X';
    char winner = ' ';

    cout << "Welcome to Tic Tac Toe!" << endl;

    // Main game loop
    while (!isGameOver(board, winner)) {
        drawBoard(board);
        cout << "Player " << currentPlayer << ", enter your move (row column): ";
        cin >> row >> col;

        // Check if the move is valid
        if (isValidMove(board, row - 1, col - 1)) {
            board[row - 1][col - 1] = currentPlayer;

            // Switch player
            currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
        } else {
            cout << "Invalid move! Try again." << endl;
        }
    }

    // Game over
    drawBoard(board);
    if (winner == 'T') {
        cout << "It's a tie!" << endl;
    } else {
        cout << "Player " << winner << " wins!" << endl;
    }

    return 0;
}k 3
