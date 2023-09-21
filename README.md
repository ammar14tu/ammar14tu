- 👋 Hi, I’m @ammar14tu
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
ammar14tu/ammar14tu is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
---> 
import random

# Initialize game variables
board = []
player_pos = [0, 0]
score = 0
game_over = False

# Create the game board
def create_board(width, height):
    return [[' ' for _ in range(width)] for _ in range(height)]

# Place Pac-Man and food on the board
def initialize_board(board, player_pos):
    width = len(board[0])
    height = len(board)

    player_x, player_y = player_pos
    board[player_y][player_x] = 'P'
    board[random.randint(0, height - 1)][random.randint(0, width - 1)] = 'F'

# Display the game board
def display_board(board):
    for row in board:
        print("".join(row))

# Move Pac-Man
def move_player(board, direction):
    player_x, player_y = player_pos
    width = len(board[0])
    height = len(board)

    if direction == 'W':
        player_y -= 1
    elif direction == 'S':
        player_y += 1
    elif direction == 'A':
        player_x -= 1
    elif direction == 'D':
        player_x += 1

    # Check for collisions with food
    if board[player_y][player_x] == 'F':
        board[player_y][player_x] = ' '
        global score
        score += 1
        spawn_food(board)

    # Update player position
    board[player_pos[1]][player_pos[0]] = ' '
    board[player_y][player_x] = 'P'
    player_pos[0], player_pos[1] = player_x, player_y

# Spawn food on the board
def spawn_food(board):
    width = len(board[0])
    height = len(board)
    while True:
        x, y = random.randint(0, width - 1), random.randint(0, height - 1)
        if board[y][x] == ' ':
            board[y][x] = 'F'
            break

# Main game loop
def main():
    global game_over
    global score

    width = 10
    height = 10

    board = create_board(width, height)
    initialize_board(board, player_pos)

    while not game_over:
        display_board(board)
        print("Score:", score)
        move = input("Enter a move (W/A/S/D to move, Q to quit): ").upper()

        if move == 'Q':
            game_over = True
            print("Game over! Final score:", score)
        elif move in ('W', 'A', 'S', 'D'):
            move_player(board, move)
        else:
            print("Invalid move. Use W/A/S/D to move or Q to quit.")

if __name__ == "__main__":
    main()
