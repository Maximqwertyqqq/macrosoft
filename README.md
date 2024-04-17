# macrosoft



'''python
import pygame
import time
from random import randint

pygame.init()
LIGHTBLUE = (200,255,255)
BLUE = (0,0,255)
RED = (255,0,0)
GREEN = (0,255,0)
YELLOW = (255,255,0)
BLACK = (0, 0, 0)
window = pygame.display.set_mode((500, 500))
window.fill(LIGHTBLUE)
clock = pygame.time.Clock()

class Area():
    def __init__(self, x, y, width, height, color=YELLOW):
        self.rect = pygame.Rect(x, y, width, height)
        self.fill_color = color
    def fill(self):
        pygame.draw.rect(window, self.fill_color, self.rect)
        # pygame.draw.rect(window, BLUE, self.rect, 3)
    def color(self, new_color):
        self.fill_color = new_color
    def collidepoint(self, x, y):
        return self.rect.collidepoint(x, y)

class Label(Area):
    def set_text(self, text, fsize=40, text_color=BLACK):
        self.image = pygame.font.SysFont('verdana', fsize).render(text, True, text_color)
    def draw(self, shift_x=0, shift_y=0):
        self.fill()
        window.blit(self.image, (self.rect.x + shift_x, self.rect.y + shift_y))

cards = list()
x_cor = 60
for i in range(4):
    card = Label(x_cor, 100, 70, 100, YELLOW)
    card.set_text("Click!", 26)
    x_cor += 100
    cards.append(card)

time_text = Label(20, 20, 50, 50, LIGHTBLUE)
time_text.set_text("Время:", 40, BLUE)
time_text.draw()

timer = Label(50, 50, 50, 50, LIGHTBLUE)
timer.set_text("0", 40, BLUE)
timer.draw()

score_text = Label(400,20,50,50,LIGHTBLUE)
score_text.set_text('Счёт:', 40, BLUE)
score_text.draw()

score = Label(430,50,50,50,LIGHTBLUE)
score.set_text('0', 40, BLUE)
score.draw()

start_time = time.time()
cur_time = start_time

wait = 0
points = 0
game = True
while game:
    if wait == 0:
        number = randint(0, 3)
        for i in range(4):
            cards[i].color(YELLOW)
            if i == number:
                cards[i].draw(10, 30)
            else:
                cards[i].fill()
        wait = 20
    else:
        wait -= 1

    for event in pygame.event.get():
        if event.type == pygame.MOUSEBUTTONDOWN and event.button == 1:
            x, y = event.pos
            # Здесь проверяем,попали в карточку или нет
            for i in range(4):
                if cards[i].collidepoint(x, y):
                    if i == number:
                        cards[i].color(GREEN)
                        points += 1
                    else:
                        cards[i].color(RED)
                        points -= 1
                    cards[i].fill()
                    score.set_text(str(points), 40, BLUE)
                    score.draw()

    new_time = time.time()
    if new_time - cur_time >= 1:
        timer.set_text(str(int(new_time-start_time)), 40, BLUE)
        timer.draw()
        cur_time = new_time

    if points >= 5:
        window.fill(GREEN)
        win_text = Label(140,200,50,50,GREEN)
        win_text.set_text('ПОБЕДА!!!', 80, BLACK)
        win_text.draw()
        game = False

    if new_time - start_time > 10:
        window.fill(RED)
        lose_text = Label(100,200,50,50,RED)
        lose_text.set_text('Время вышло!!!', 80, BLACK)
        lose_text.draw()
        game = False


    pygame.display.update()
    clock.tick(40)


