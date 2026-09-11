<h1>ExpNo 7 : Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>Name: SWETHA C     </h3>
<h3>Register Number:   212224230283     </h3>
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

## Program :

```

import time
def initialize_game():
    current_state = [['.','.','.'],
                              ['.','.','.'],
                              ['.','.','.']]
    player_turn = 'X'
def draw_board():
    for i in range(0, 3):
        for j in range(0, 3):
            print('{}|'.format(current_state[i][j]), end=" ")
        print()
    print()
def is_valid(px, py):
    if px < 0 or px > 2 or py < 0 or py > 2:
        return False
    elif current_state[px][py] != '.':
        return False
    else:
        return True
def is_end():
# Vertical win
    for i in range(0, 3):
        if (current_state[0][i] != '.' and
            current_state[0][i] == current_state[1][i] and
            current_state[1][i] == current_state[2][i]):
            return current_state[0][i]
    # Horizontal win
    for i in range(0, 3):
        if (current_state[i] == ['X', 'X', 'X']):
            return 'X'
        elif (current_state[i] == ['O', 'O', 'O']):
            return 'O'
# Main diagonal win
    if (current_state[0][0] != '.' and
        current_state[0][0] == current_state[1][1] and
        current_state[0][0] == current_state[2][2]):
        return current_state[0][0]
# Second diagonal win
    if (current_state[0][2] != '.' and
        current_state[0][2] == current_state[1][1] and
        current_state[0][2] == current_state[2][0]):
        return current_state[0][2]
# Is the whole board full?
    for i in range(0, 3):
        for j in range(0, 3):
        # There's an empty field, we continue the game
            if (current_state[i][j] == '.'):
                return None
# It's a tie!
    return '.'
def min_alpha_beta(alpha, beta):
    '''Write Your Code Here
    '''
    minv = 2
    qx = None
    qy = None
    result = is_end()
    if result == 'X':
        return (-1,0,0)
    elif result == 'O':
        return (1,0,0)
    elif result == '.':
        return(0,0,0)
    for i in range(3):
        for j in range(3):
            if current_state[i][j]=='.':
                current_state[i][j]='X'
                (m,max_i,max_j)=max_alpha_beta(alpha,beta)
                if m<minv:
                    minv = m
                    qx = i
                    qy = j
                current_state[i][j]='.'
                if minv <= alpha:
                    return (minv,qx,qy)
                if minv < beta :
                    beta = minv
    return (minv,qx,qy)
def max_alpha_beta(alpha, beta):
    '''Write Your Code Here
    '''
    maxv = -2
    px = None
    py = None
    result = is_end()
    if result == 'X':
        return (-1,0,0)
    elif result == 'O':
        return (1,0,0)
    elif result == '.':
        return(0,0,0)
    for i in range(3):
        for j in range(3):
            if current_state[i][j]=='.':
                current_state[i][j]='O'
                (m,min_i,min_j)=min_alpha_beta(alpha,beta)
                if m>maxv:
                    maxv = m
                    px = i
                    py = j
                current_state[i][j]='.'
                if maxv >= beta:
                    return (maxv,px,py)
                if maxv > alpha :
                    alpha = maxv
    return (maxv,px,py)
def play_alpha_beta():
    player_turn = 'X'
    while True:
        draw_board()
        result = is_end()
        # Printing the appropriate message if the game has ended
        if result != None:
            if result == 'X':
                print('The winner is X!')
            elif result == 'O':
                print('The winner is O!')
            elif result == '.':
                print("It's a tie!")
            initialize_game()
            return
        # If it's player's turn
        if player_turn == 'X':
            while True:
                start = time.time()
                (m, qx, qy) = min_alpha_beta(-2, 2)
                end = time.time()
                #print('Evaluation time: {}s'.format(round(end - start, 7)))
                print('Recommended move: X = {}, Y = {}'.format(qx, qy))
                px = int(input())
                py = int(input())
                (qx, qy) = (px, py)
                if is_valid(px, py):
                    current_state[px][py] = 'X'
                    player_turn = 'O'
                    break
                else:
                    print('The move is not valid! Try again.')
        # If it's AI's turn
        else:
            (m, px, py) = max_alpha_beta(-2, 2)
            current_state[px][py] = 'O'
            player_turn = 'X'
current_state = [['.','.','.'],
                              ['.','.','.'],
                              ['.','.','.']]
play_alpha_beta()

```
## Output:

<img width="1264" height="997" alt="554547113-9e681e1e-b55e-426b-9061-da4d08669785" src="https://github.com/user-attachments/assets/ebdd3d54-e51d-4623-ba53-7f144635def4" />

<img width="1920" height="1200" alt="554547370-b4404efb-8363-4b1f-b0c5-811def2a766c" src="https://github.com/user-attachments/assets/5f1f62a1-de14-44b5-9070-ad175e57c868" />

## Result:
We have successfully implemented Alpha-Beta pruning of MiniMax Search Algorithm for a simple TIC-TAC-TOE game.
