import math

# Tic-Tac-Toe AI using Minimax
human = "O"
ai = "X"

# Initialize empty board
board = [" " for _ in range(9)]

def print_board(board):
    print()
    for i in range(3):
        print(" | ".join(board[i*3:(i+1)*3]))
        if i < 2:
            print("---------")
    print()

def check_winner(brd, player):
    # All winning combinations
    win_combinations = [
        [0,1,2], [3,4,5], [6,7,8], # rows
        [0,3,6], [1,4,7], [2,5,8], # columns
        [0,4,8], [2,4,6]           # diagonals
    ]
    for combo in win_combinations:
        if all(brd[pos] == player for pos in combo):
            return True
    return False

def is_draw(brd):
    return " " not in brd

def minimax(brd, depth, is_maximizing):
    if check_winner(brd, ai):
        return 1
    elif check_winner(brd, human):
        return -1
    elif is_draw(brd):
        return 0

    if is_maximizing:
        best_score = -math.inf
        for i in range(9):
            if brd[i] == " ":
                brd[i] = ai
                score = minimax(brd, depth+1, False)
                brd[i] = " "
                best_score = max(score, best_score)
        return best_score
    else:
        best_score = math.inf
        for i in range(9):
            if brd[i] == " ":
                brd[i] = human
                score = minimax(brd, depth+1, True)
                brd[i] = " "
                best_score = min(score, best_score)
        return best_score

def best_move():
    best_score = -math.inf
    move = None
    for i in range(9):
        if board[i] == " ":
            board[i] = ai
            score = minimax(board, 0, False)
            board[i] = " "
            if score > best_score:
                best_score = score
                move = i
    return move

def play():
    print("Welcome to Tic-Tac-Toe! You are O, AI is X.")
    print_board(board)

    while True:
        # Human move
        move = int(input("Enter your move (1-9): ")) - 1
        if board[move] != " ":
            print("Invalid move, try again!")
            continue
        board[move] = human

        print_board(board)

        if check_winner(board, human):
            print("🎉 You win! 🎉")
            break
        elif is_draw(board):
            print("It's a draw!")
            break

        # AI move
        ai_move = best_move()
        board[ai_move] = ai
        print("AI chooses:", ai_move+1)
        print_board(board)

        if check_winner(board, ai):
            print("💻 AI wins! Better luck next time.")
            break
        elif is_draw(board):
            print("It's a draw!")
            break

if __name__ == "__main__":
    play()
