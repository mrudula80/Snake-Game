import pygame
import random
import sys

# Initialize Pygame
pygame.init()

# Screen settings
WIDTH, HEIGHT = 600, 400
CELL_SIZE = 20

screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Snake Game")

clock = pygame.time.Clock()
font = pygame.font.SysFont(None, 35)

# Colors
WHITE = (255, 255, 255)
GREEN = (0, 200, 0)
RED = (220, 0, 0)
BLACK = (0, 0, 0)

# Snake
snake = [(100, 100)]
direction = (CELL_SIZE, 0)

# Food
food = (
    random.randrange(0, WIDTH, CELL_SIZE),
    random.randrange(0, HEIGHT, CELL_SIZE)
)

score = 0


def draw_text(text, x, y):
    img = font.render(text, True, WHITE)
    screen.blit(img, (x, y))


running = True

while running:

    # Events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_UP and direction != (0, CELL_SIZE):
                direction = (0, -CELL_SIZE)
            elif event.key == pygame.K_DOWN and direction != (0, -CELL_SIZE):
                direction = (0, CELL_SIZE)
            elif event.key == pygame.K_LEFT and direction != (CELL_SIZE, 0):
                direction = (-CELL_SIZE, 0)
            elif event.key == pygame.K_RIGHT and direction != (-CELL_SIZE, 0):
                direction = (CELL_SIZE, 0)

    # Move snake
    head = (
        snake[0][0] + direction[0],
        snake[0][1] + direction[1]
    )

    # Collision with walls or itself
    if (
        head[0] < 0 or head[0] >= WIDTH or
        head[1] < 0 or head[1] >= HEIGHT or
        head in snake
    ):
        break

    snake.insert(0, head)

    # Eat food
    if head == food:
        score += 1
        food = (
            random.randrange(0, WIDTH, CELL_SIZE),
            random.randrange(0, HEIGHT, CELL_SIZE)
        )
    else:
        snake.pop()

    # Draw
    screen.fill(BLACK)

    pygame.draw.rect(screen, RED, (*food, CELL_SIZE, CELL_SIZE))

    for segment in snake:
        pygame.draw.rect(screen, GREEN, (*segment, CELL_SIZE, CELL_SIZE))

    draw_text(f"Score: {score}", 10, 10)

    pygame.display.flip()
    clock.tick(10)

# Game Over
screen.fill(BLACK)
draw_text("Game Over!", 220, 150)
draw_text(f"Final Score: {score}", 200, 200)
pygame.display.flip()
pygame.time.wait(3000)

pygame.quit()
sys.exit()