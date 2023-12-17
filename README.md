import pygame
import sys
import random

# Oyun başlangıcı
pygame.init()

# Ekran boyutları
screen_width = 800
screen_height = 600

# Renkler
white = (255, 255, 255)
black = (0, 0, 0)
red = (255, 0, 0)

# Ekran oluştur
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Uçak Oyunu")

# Oyuncu uçağı
player_width = 50
player_height = 50
player_x = screen_width // 2 - player_width // 2
player_y = screen_height - player_height - 10
player_speed = 5

# Düşman uçakları
enemy_width = 50
enemy_height = 50
enemy_speed = 3
enemies = []

def create_enemy():
    enemy_x = random.randint(0, screen_width - enemy_width)
    enemy_y = random.randint(-screen_height, 0)
    enemies.append([enemy_x, enemy_y])

# Oyuncu uçağını çiz
def draw_player(x, y):
    pygame.draw.rect(screen, white, [x, y, player_width, player_height])

# Düşman uçağını çiz
def draw_enemy(x, y):
    pygame.draw.rect(screen, red, [x, y, enemy_width, enemy_height])

# Oyun döngüsü
clock = pygame.time.Clock()

while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    # Oyuncu kontrolü
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT] and player_x > 0:
        player_x -= player_speed
    if keys[pygame.K_RIGHT] and player_x < screen_width - player_width:
        player_x += player_speed

    # Düşman oluşturma
    if random.randint(0, 100) < 5:
        create_enemy()

    # Düşman hareketi ve çizimi
    for enemy in enemies:
        enemy[1] += enemy_speed
        draw_enemy(enemy[0], enemy[1])

    # Oyuncu uçağını çiz
    draw_player(player_x, player_y)

    # Ekranı güncelle
    pygame.display.flip()

    # FPS ayarı
    clock.tick(30)

