# Ping-Pong

Короче говоря тут я написал пинг-понг, где надо играть за две доски(двум игрокам), и надо отбивать мяч пока не устанешь(от скуки).Первая доска w or s, а вторая доска вверх или вниз(тут все).
# Ping-Pong

from  pygame import *

weight = 900
hieght = 700
green = (154, 205, 50)
window = display.set_mode((weight, hieght))
display.set_caption('Пинг-понг')
window.fill(green)




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

clock = time.Clock()
FPS = 60

joker = Player('джокер.jpg',30, 200,  50, 150, 4)
joker2 = Player('джокер.jpg',750, 200, 50, 150, 4)
ball = shuterSprite('магма.jpg', 200, 200, 50, 50, 4)



font.init()
font = font.Font(None, 36)
lose_1 = font.render("Первый джокер поиграл", True,  (180, 0, 0))
lose_2 = font.render("Второй джокер поиграл", True,  (180, 0, 0))

speed_x = 3
speed_y = 3

finish = False
game = True
while game:
    for e in event.get():
        if e.type == QUIT:
            game = False

    if finish != True:
        window.fill(green)
        joker.reset()
        joker.update_left()
        joker2.reset()
        joker.update_right()

        ball.rect.x += speed_x
        ball.rect.y += speed_y

        if sprite.collide_rect(joker, ball) or sprite.collide_rect(joker2, ball):
            speed_x *= -1
        ball.reset()
        if ball.rect.x >= 850:
            lose_2= True
        if ball.rect.x <= 30:
            lose_1 = True
        if ball.rect.y >= 600:
            speed_y *= -1
        if ball.rect.y <= 100:
            speed_y *= -1

    display.update()
    clock.tick(FPS)

