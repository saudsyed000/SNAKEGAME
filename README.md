#this is my first python code project in github
import pygame
import time
import random

pygame.init()

width = 600
height = 400
screen = pygame.display.set_mode((width,height))
pygame.display.set_caption("Snake game 🐍")

white = (255,255,255)
black = (0,0,0)
green = (0,255,0)
red = (255,0,0)

block_size = 20
snake_speed = 15
Clock = pygame.time.Clock()
font = pygame.font.SysFont(None,35)

def draw_snake(snake_list):
    for block in snake_list:
        pygame.draw.rect(screen,green,[block[0],block[1],block_size,block_size])

def message(msg,color):
    text = font.render(msg, True, color)
    screen.blit(text, [width / 6, height / 3])

def gameLoop():
    game_over = False
    game_close = False

x1 = width/2
y1 = height/2
x1_change = 0
y1_change = 0

snake_list = []
length_of_snake = 1

food_x = round(random.randrange(0,width-block_size)/20.0)*20.0
food_y = round(random.randrange(0,height-block_size)/20.0)*20.0

while not game_over:

    while game_close:
        screen.fill(whiite)
        message("You Lost! Press Q-Quit or C-Play Again",red)
        pygame.display.update()

for event in pygame.event.gry():
    if event.type == pygame.KEYDOWN:
        if event.key == pygame.K_LEFT:
            x1_change = -block_size
            y1_change = 0

if x1>=width or x1<0 or y1>=height  or y1<0:
    game_close = True

x1 += x1_change
y1 += y1_change

pygame.draw.rect(screen,red,[food_x,food_y,block_size,block_size])

snake_head = [x1,y1]
snake_list.append(snake_head)

if len(snake_list)>length_of_snake:
    del snake_list[0]

for block in snake_list[:-1]:
    if block == snake_head:
        game_close = True 

if x1 == food_x and y1 == food_y:
    food_x = round(random.randrange(0,width-block_size)/20.0)*20.0
    food_y = round(random.randrange(0,height-block_size)/20.0)*20.0
    length_of_snake += 1

gameLoop()

Clock.tick(snake_speed)

pygame.qut()
quit