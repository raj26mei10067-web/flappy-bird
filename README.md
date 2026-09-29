# flappy-bird
simple game flappy bird 
pimport pygame
import random

pygame.init()

screen = pygame.display.set_mode((600, 400))
pygame.display.set_caption("Mini Flappy Bird")

bird = pygame.Rect(100, 200, 30, 30)
pipes = []
score = 0
gravity = 1
jump = -10
velocity = 0
clock = pygame.time.Clock()

for x in range(600, 1200, 250):
    gap = random.randint(120, 250)
    pipes.append(pygame.Rect(x, 0, 50, gap))
    pipes.append(pygame.Rect(x, gap + 100, 50, 400))

running = True

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE:
                velocity = jump

    velocity += gravity
    bird.y += velocity

    for pipe in pipes:
        pipe.x -= 3

        if bird.colliderect(pipe):
            running = False

    if bird.top < 0 or bird.bottom > 400:
        running = False

    screen.fill((135, 206, 235))

    pygame.draw.rect(screen, (255, 220, 0), bird)

    for pipe in pipes:
        pygame.draw.rect(screen, (0, 180, 0), pipe)

    pygame.display.update()
    clock.tick(60)

pygame.quit()