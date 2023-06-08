- 👋 Hi, I’m @Rohi56u
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Rohi56u/Rohi56u is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import pygame
import random

# Initialize Pygame
pygame.init()

# Set up the game window
WIDTH = 800
HEIGHT = 600
window = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("My 2D Game")

# Set up colors
WHITE = (255, 255, 255)
RED = (255, 0, 0)

# Set up the player
player_size = 50
player_x = WIDTH // 2 - player_size // 2
player_y = HEIGHT - player_size - 10

# Set up the enemy
enemy_size = 50
enemy_x = random.randint(0, WIDTH - enemy_size)
enemy_y = 0
enemy_speed = 5

# Set up the game clock
clock = pygame.time.Clock()

# Game loop
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Handle player movement
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT] and player_x > 0:
        player_x -= 5
    if keys[pygame.K_RIGHT] and player_x < WIDTH - player_size:
        player_x += 5

    # Update enemy position
    enemy_y += enemy_speed
    if enemy_y > HEIGHT:
        enemy_x = random.randint(0, WIDTH - enemy_size)
        enemy_y = 0

    # Check for collision
    if (
        player_x < enemy_x + enemy_size
        and player_x + player_size > enemy_x
        and player_y < enemy_y + enemy_size
        and player_y + player_size > enemy_y
    ):
        running = False

    # Render the game
    window.fill(WHITE)
    pygame.draw.rect(window, RED, (player_x, player_y, player_size, player_size))
    pygame.draw.rect(window, RED, (enemy_x, enemy_y, enemy_size, enemy_size))
    pygame.display.update()

    # Set the frames per second
    clock.tick(60)
