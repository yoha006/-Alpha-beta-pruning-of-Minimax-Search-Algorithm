<h1>ExpNo 7 : Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>Name: P.YOHALAKSHMI </h3>
<h3>Register Number: 212224060314      </h3>
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

<hr>
<h2>Program</h2>
       
    import math
    # Print the board in 3x3 format
    def print_board(board):
     print("\n")
    for i in range(3):
        print(board[3*i], board[3*i+1], board[3*i+2])
    print("\n")

    # Check winner
    def check_winner(board, player):
     win_states = [
        [0,1,2], [3,4,5], [6,7,8],      # Rows
        [0,3,6], [1,4,7], [2,5,8],      # Columns
        [0,4,8], [2,4,6]                # Diagonals
    ]
    return any(all(board[pos] == player for pos in state) for state in win_states)

    # Check draw
    def is_draw(board):
     return all(cell != "_" for cell in board)

    # ---------------------------
    #   MINIMAX + ALPHA-BETA
    # ---------------------------
    def minimax(board, depth, alpha, beta, is_maximizing):
    # Terminal conditions
    if check_winner(board, "O"):
        return 1
    if check_winner(board, "X"):
        return -1
    if is_draw(board):
        return 0

    # Maximizing player (AI = O)
    if is_maximizing:
        best_score = -math.inf

        for i in range(9):
            if board[i] == "_":
                board[i] = "O"

                score = minimax(board, depth + 1, alpha, beta, False)

                board[i] = "_"
                best_score = max(best_score, score)
                alpha = max(alpha, score)

                if beta <= alpha:
                    break  # Beta cutoff

        return best_score

    # Minimizing player (Human = X)
    else:
        best_score = math.inf

        for i in range(9):
            if board[i] == "_":
                board[i] = "X"

                score = minimax(board, depth + 1, alpha, beta, True)

                board[i] = "_"
                best_score = min(best_score, score)
                beta = min(beta, score)

                if beta <= alpha:
                    break  # Alpha cutoff

        return best_score

    # Choose best AI move
    def ai_move(board):
    best_score = -math.inf
    move = -1

    for i in range(9):
        if board[i] == "_":
            board[i] = "O"

            score = minimax(board, 0, -math.inf, math.inf, False)

            board[i] = "_"

            if score > best_score:
                best_score = score
                move = i

    board[move] = "O"


    # ---------------------------
    #     GAME LOOP
    # ---------------------------
    def play_game():
      board = ["_"] * 9

    print("TIC-TAC-TOE with Alpha-Beta Pruning")
    print("You are X, Computer is O")
    print_board(board)

    while True:
        # Human turn
        try:
            user = int(input("Enter your move (0-8): "))
        except:
            print("Invalid input! Enter a number between 0 and 8.")
            continue

        if user < 0 or user > 8 or board[user] != "_":
            print("Invalid move! Try again.")
            continue

        board[user] = "X"
        print_board(board)

        if check_winner(board, "X"):
            print("🎉 You Win!")
            break
        if is_draw(board):
            print("🤝 It's a Draw!")
            break

        # AI turn
        print("Computer thinking...")
        ai_move(board)
        print_board(board)

        if check_winner(board, "O"):
            print("💻 Computer Wins!")
            break
        if is_draw(board):
            print("🤝 It's a Draw!")
            break


     # Run the game
     play_game()


<hr>
<h2>Output</h2>
<img width="369" height="1030" alt="image" src="https://github.com/user-attachments/assets/1afd8592-3c30-4540-9964-82181ee49076" />
<img width="275" height="648" alt="image" src="https://github.com/user-attachments/assets/c381419a-a6de-4ab2-bd73-5f86d6f548fa" />


<hr>
<h2>Result</h2>
    Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game is implemented.
