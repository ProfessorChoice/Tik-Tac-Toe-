board = [["-", "-", "-"],["-", "-", "-"],["-", "-", "-"]]

def check_col_win(player, board):
    if (board[0][0] == player and board[1][0] == player and board[2][0] == player):
        return True
    if (board[0][1] == player and board[1][1] == player and board[2][1] == player):
        return True
    if (board[0][2] == player and board[1][2] == player and board[2][2] == player):
        return True
    return False

def check_row_win(player, board):
    if (board[0][0] == player and board[0][1] == player and board[0][2] == player):
        return True
    if (board[1][0] == player and board[1][1] == player and board[1][2] == player):
        return True
    if (board[2][0] == player and board[2][1] == player and board[2][2] == player):
        return True
    return False

def check_diag_win(player, board):
    if (board[0][0] == player and board[1][1] == player and board[2][2] == player):
        return True
    if (board[0][2] == player and board[1][1] == player and board[2][0] == player):
        return True
    return False

def check_win(player, board):
    return check_col_win(player, board) or check_row_win(player, board) or check_diag_win(player, board)

def is_valid_move(row, col):
    try:
        row = int(row)
        col = int(col)
        if row < 3 and row >= 0 and col < 3 and col >= 0 and board[row][col] == "-":
            return True
        return False
    except ValueError:
        return False

def make_hypothetical_move(board, player, row, col):
    new_board = [row[:] for row in board]
    new_board[row][col] = player
    return new_board

def emptyspaces(boardInput):
    listEmptySpaces = []
    for i in range(3):
        for j in range(3):
            if boardInput[i][j] == "-":
                listEmptySpaces.append((i, j))
    return listEmptySpaces

def take_turnX(player, board):
    print(f"{player}'s turn")
    rowNumber = input("Enter a row ")
    colNumber = input("Enter a column ")
    if is_valid_move(rowNumber, colNumber):
        board[int(rowNumber)][int(colNumber)] = f"{player}"
        if check_win(player, board):
            print(f"{player} wins")
            quit()
        if len(emptyspaces(board)) == 0:
            print("It's a Tie!")
            quit()
        take_turnO("O", minimax('O', board, 0)[1],minimax('O', board, 0)[2], board)
    else:
        print("Please enter a valid move")
        take_turnX(player, board)

def take_turnO(player, positionX, positionY, board):
    print(f"{player}'s turn")
    rowNumber = positionX
    colNumber = positionY
    if check_win(player, board):
        print(f"{player} wins")
        quit()
    if is_valid_move(rowNumber, colNumber):
        if check_win(player, board):
            print(f"{player} wins")
            quit()
        board[rowNumber][colNumber] = f"{player}"
        print_board()
        if check_win(player, board):
            print(f"{player} wins")
            quit()
        take_turnX("X", board)
    else:
        take_turnO(player, positionX, positionY, board)

def minimax(player, board, depth):
    if check_win("O", board):
        return 1 + depth, board, depth
    elif check_win("X", board):
        return -10 + depth, board, depth
    elif len(emptyspaces(board)) == 0:
        return 0, board, depth

    if player == 'O':
        max_eval = float('-inf')
        rowHolder = None
        colHolder = None
        for row, col in emptyspaces(board):
            new_board = make_hypothetical_move(board, 'O', row, col)
            eval = minimax('X', new_board, depth - 1)[0]
            if eval > max_eval:
                max_eval = eval
                rowHolder = row
                colHolder = col
        return max_eval, rowHolder, colHolder
    else:
        min_eval = float('inf')
        rowHolder = None
        colHolder = None
        for row, col in emptyspaces(board):
            new_board = make_hypothetical_move(board, 'X', row, col)
            eval = minimax('O', new_board, depth - 1)[0]
            if eval < min_eval:
                min_eval = eval
                rowHolder = row
                colHolder = col
        return min_eval, rowHolder, colHolder

def print_board():
    print("\n")
    print("\t\t\t\t\t")
    count = 0
    for item in board:
        row = ""
        for space in item:
            row += "\t" + space + "\t"
        print(count,row + "\n")
        count += 1

print_board()
take_turnX('X', board)
