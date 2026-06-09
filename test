from pygame import *
from random import randint
#cargando las funciones de fuente por separado
font.init()
font1 = font.Font(None, 80)
win = font1.render('¡GANASTE!', True, (255, 255, 255))
lose = font1.render('¡PERDISTE!', True, (180, 0, 0))


font2 = font.Font(None, 36)


#música de fondo
mixer.init()
mixer.music.load('space.ogg')
mixer.music.play()
fire_sound = mixer.Sound('fire.ogg')


#necesitamos las siguientes imágenes:
img_back = "galaxy.jpg" #fondo de juego
img_bullet = "bullet.png" #bala
img_hero = "rocket.png" #héroe
img_enemy = "ufo.png" #enemigo
score = 0 #naves destruidas
goal = 10 #la cantidad de naves que necesitan ser destruidas para ganar
lost = 0 #naves falladas
max_lost = 3 #se pierde si se falla tantas veces
#clase padre para otros objetos
class GameSprite(sprite.Sprite):
 #constructor de clase
   def __init__(self, player_image, player_x, player_y, size_x, size_y, player_speed):
       #llamada para el constructor de la clase (Sprite):
       sprite.Sprite.__init__(self)


       #cada objeto debe almacenar la propiedad image
       self.image = transform.scale(image.load(player_image), (size_x, size_y))
       self.speed = player_speed


       #cada objeto debe tener la propiedad rect que representa el rectángulo en el que se encuentra
       self.rect = self.image.get_rect()
       self.rect.x = player_x
       self.rect.y = player_y
 #método de dibujo del personaje en la ventana
   def reset(self):
       window.blit(self.image, (self.rect.x, self.rect.y))


#Clase del jugador principal
class Player(GameSprite):
   #método para controlar el objeto con las flechas
   def update(self):
       keys = key.get_pressed()
       if keys[K_LEFT] and self.rect.x > 5:
           self.rect.x -= self.speed
       if keys[K_RIGHT] and self.rect.x < win_width - 80:
           self.rect.x += self.speed
 #método para “disparar” (use la posición del jugador para crear una bala ahí)
   def fire(self):
       bullet = Bullet(img_bullet, self.rect.centerx, self.rect.top, 15, 20, -15)
       bullets.add(bullet)


#clase del objeto enemigo  
class Enemy(GameSprite):
   #movimiento del enemigo
   def update(self):
       self.rect.y += self.speed
       global lost
       #desaparece al llegar al borde de la pantalla
       if self.rect.y > win_height:
           self.rect.x = randint(80, win_width - 80)
           self.rect.y = 0
           lost = lost + 1
#clase del objeto de la bala  
class Bullet(GameSprite):
   # movimiento del enemigo
   def update(self):
       self.rect.y += self.speed
       # desaparece al llegar al borde de la pantalla
       if self.rect.y < 0:
           self.kill()
#Crear una ventana pequeña
win_width = 700
win_height = 500
display.set_caption("Tirador")
window = display.set_mode((win_width, win_height))
background = transform.scale(image.load(img_back), (win_width, win_height))
#Crear objetos
ship = Player(img_hero, 5, win_height - 100, 80, 100, 10)
#Creando un grupo de objetos enemigos
monsters = sprite.Group()
for i in range(1, 6):
   monster = Enemy(img_enemy, randint(80, win_width - 80), -40, 80, 50, randint(1, 5))
   monsters.add(monster)
bullets = sprite.Group()
#La variable “juego terminado”: cuando sea True, los objetos dejan de funcionar en el ciclo principal
finish = False
#Ciclo de juego principal:
run = True #La bandera es reiniciada con el botón de cerrar ventana
while run:
   #Evento de pulsación del botón “Cerrar”
   for e in event.get():
       if e.type == QUIT:
           run = False
       #evento de pulsación de barra espaciadora – el objeto dispara
       elif e.type == KEYDOWN:
           if e.key == K_SPACE:
               fire_sound.play()
               ship.fire()
 #el juego: acción de los objetos, comprobando las reglas del juego, volviendo a dibujar
   if not finish:
       #actualiza el fondo
       window.blit(background,(0,0))


       #Ejecuta los movimientos del objeto
       ship.update()
       monsters.update()
       bullets.update()


       #los actualiza en una nueva ubicación con cada iteración del ciclo
       ship.reset()
       monsters.draw(window)
       bullets.draw(window)
       #Comprueba una colisión entre una bala y los monstruos (tanto los monstruos como la bala desaparecen al tocarse)
       collides = sprite.groupcollide(monsters, bullets, True, True)
       for c in collides:
           #este ciclo se repetirá tantas veces como se golpee a los enemigos
           score = score + 1
           monster = Enemy(img_enemy, randint(80, win_width - 80), -40, 80, 50, randint(1, 5))
           monsters.add(monster)


       #posible derrota: se fallaron muchos enemigos o el personaje chocó con el enemigo
       if sprite.spritecollide(ship, monsters, False) or lost >= max_lost:
           finish = True #derrota, se establece el fondo y ya no se puede controlar los objetos.
           window.blit(lose, (200, 200))


       #comprobación de victoria: ¿cuántos puntos se tienen?
       if score >= goal:
           finish = True
           window.blit(win, (200, 200))


       #Se escribe texto en la pantalla
       text = font2.render("Puntaje: " + str(score), 1, (255, 255, 255))
       window.blit(text, (10, 20))


       text_lose = font2.render("Fallados: " + str(lost), 1, (255, 255, 255))
       window.blit(text_lose, (10, 50))


       display.update()
   #extra: reinicio automático del juego
   else:
       finish = False
       score = 0
       lost = 0
       for b in bullets:
           b.kill()
       for m in monsters:
           m.kill()


       time.delay(3000)
       for i in range(1, 6):
           monster = Enemy(img_enemy, randint(80, win_width - 80), -40, 80, 50, randint(1, 5))
           monsters.add(monster)
      


   time.delay(50)
