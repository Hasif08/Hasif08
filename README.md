import time
import random

def main():
    print("Welcome to the Bat Obstacle Game!")
    print("Use 'A' and 'D' keys to move the bat.")
    print("Cross obstacles to earn points.")
    print("Avoid collisions!\n")

    bat_position = 5  # Initial bat position
    obstacles = ["|   |", "|   |", "|   |", "|   |", "|   |"]  # Initial set of obstacles
    score = 0  # Starting score
    while True:
        display_game(obstacles, bat_position, score)
        user_input = input("Press 'A' to move left, 'D' to move right, or 'Q' to quit: ").lower()

        if user_input == 'a':
            bat_position = max(0, bat_position - 1)  # Move bat left
        elif user_input == 'd':
            bat_position = min(9, bat_position + 1)  # Move bat right
        elif user_input == 'q':
            break  # Quit the game
        
        obstacles = move_obstacles(obstacles)  # Move obstacles
        score += check_collision(obstacles, bat_position)  # Check for collision and update score
        time.sleep(0.5)  # Add a small delay for better visualization

    print("Thanks for playing!")

def display_game(obstacles, bat_position, score):
    print("\nScore:", score)
    for i in range(len(obstacles)):
        if i == bat_position:
            print("  /\\ ", end='')
        else:
            print("     ", end='')
    print()
    for obstacle in obstacles:
        print(obstacle, end='')
    print("\n" + "=" * 20)

def move_obstacles(obstacles):
    new_obstacles = ["|   |"]  # Generate a new set of obstacles
    for i in range(len(obstacles) - 1):
        new_obstacles.append(obstacles[i])
    return new_obstacles

def check_collision(obstacles, bat_position):
    if obstacles[bat_position] == "|   |":  # If the bat crosses an obstacle
        return 1
    return 0

if __name__ == "__main__":
    main()
