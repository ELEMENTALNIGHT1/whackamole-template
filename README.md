import pygame
import random

# Constants for grid and screen size
GRID_WIDTH = 32
GRID_HEIGHT = 32
GRID_COLS = 20
GRID_ROWS = 16
SCREEN_WIDTH = GRID_WIDTH * GRID_COLS
SCREEN_HEIGHT = GRID_HEIGHT * GRID_ROWS


def main():
    try:
        pygame.init()
        # Set up the screen
        screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
        pygame.display.set_caption("Whack-a-Mole")

        # Load the mole image
        mole_image = pygame.image.load("mole.png")
        mole_size = mole_image.get_size()

        # Initialize clock
        clock = pygame.time.Clock()
        running = True

        # Mole's initial position
        mole_x, mole_y = 0, 0

        while running:
            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    running = False
                elif event.type == pygame.MOUSEBUTTONDOWN:
                    # Check if the mole is clicked
                    mouse_x, mouse_y = event.pos
                    if (mole_x <= mouse_x < mole_x + GRID_WIDTH and
                            mole_y <= mouse_y < mole_y + GRID_HEIGHT):
                        # Move mole to a new random position
                        mole_x = random.randrange(0, GRID_COLS) * GRID_WIDTH
                        mole_y = random.randrange(0, GRID_ROWS) * GRID_HEIGHT

            # Fill the screen
            screen.fill("light green")

            # Draw the grid
            for x in range(0, SCREEN_WIDTH, GRID_WIDTH):
                pygame.draw.line(screen, "black", (x, 0), (x, SCREEN_HEIGHT))
            for y in range(0, SCREEN_HEIGHT, GRID_HEIGHT):
                pygame.draw.line(screen, "black", (0, y), (SCREEN_WIDTH, y))

            # Draw the mole
            screen.blit(mole_image, mole_image.get_rect(topleft=(mole_x, mole_y)))

            # Update the display
            pygame.display.flip()
            clock.tick(60)
    finally:
        pygame.quit()


if __name__ == "__main__":
    main()
