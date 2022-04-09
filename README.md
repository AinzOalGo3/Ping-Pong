# Ping-Pong

Короче говоря тут я написал пинг-понг, где надо играть за две доски(двум игрокам), и надо отбивать мяч пока не устанешь(от скуки).Первая доска w or s, а вторая доска вверх или вниз(тут все).
from  pygame import *

weight = 900
hieght = 700
green = (139, 69, 19)
window = display.set_mode((weight, hieght))
display.set_caption('Пинг-понг')
window.fill(green)
clock = pygame.time.Clock()

green = (139, 69, 19)

class shuterSprite(sprite.Sprite):
    def __init__(self, player_image, player_x, player_y, size_x, size_y, player_speed):
        super().__init__()
        self.image = transform.scale(image.load(player_image), (size_x, size_y))
        self.speed = player_speed
        self.rect = self.image.get_rect()
        self.rect.x = player_x
        self.rect.y = player_y

    def reset(self):
        window.blit(self.image, (self.rect.x, self.rect.y))


# создание игрока
class Player(shuterSprite):
    def update_left(self):
        key_pressed = key.get_pressed()

        if key_pressed[K_w] and self.rect.x > 5:
            self.rect.x -= self.speed
        if key_pressed[K_s] and self.rect.x < weight - 70:
            self.rect.x += self.speed

    def update_right(self):
        key_pressed = key.get_pressed()

        if key_pressed[K_UP] and self.rect.x > 5:
            self.rect.x -= self.speed
        if key_pressed[K_DOWN] and self.rect.x < weight - 70:
            self.rect.x += self.speed

joker = Player('джокер.png',30, 200,  50, 150, 4)
joker2 = Player('джокер.png',30, 550, 50, 150, 4)
ball = shuterSprite('магма.png', 200, 200, 50, 50, 4)



font.init()
font = font.Font(None, 36)
lose_1 = font.render("Первый джокер поиграл",1,  (0, 0, 0))
lose_2 = font.render("Второй джокер поиграл",1,  (0, 0, 0))

speed_x = 3
speed_y = 3

finish = False
game = True
while game:
    for e in event.get():
        if e.type == QUIT:
            game = False

        if finish == True:
            window.fill(green)
            joker.reset()
            joker.update_left()
            joker2.reset()
            joker.update_right()
            
