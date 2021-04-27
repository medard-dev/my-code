# my-code
import pygame

pygame.init()

instagram = '@Medard_fm'

screen_size = [630,500]
screen = pygame.display.set_mode(screen_size)
pygame.display.set_caption('Space Invaders')
background = pygame.image.load('C:/Python38/fist projecti/space.png')

# class for the planets

planets = ['C:/Users/medar/AppData/Local/Temp/Rar$DRa77364.19500/transparentplanet.png','C:/Users/medar/AppData/Local/Temp/Rar$DRa77364.21545/secondtransparentplanet.png','C:/Users/medar/AppData/Local/Temp/Rar$DRa77364.23204/3rdtransparentplanet.png']
p_index = 0
planet = pygame.image.load(planets[p_index])
planet_x = 140
move_direction = 'right'

#class for the Rocket
Rocket_x = pygame.image.load('C:/Users/medar/AppData/Local/Temp/Rar$DRa65604.17129/transparent rocket.png')
rect = Rocket_x.get_rect()
rect.center = (160,390)
move_direction = 'right'

# class for the bullet
bullet = pygame.image.load('bullet.png').convert()
bullet = pygame.transform.scale(bullet,(bullet.get_width()//6,bullet.get_height()//10))
bullet_y = 400
fired = False

font = pygame.font.Font('C:/Python38/clown.ttf', 29)
score = 0
text = font.render('Score: '+str(score),True,(255,255,255))

clock = pygame.time.Clock()
run = True
while run:
    for event in pygame.event.get():
            running = False
    keys = pygame.key.get_pressed()
        
    if keys[pygame.K_SPACE] == True:
        fired = True
        
    #making the player move left and right    
    if keys[pygame.K_RIGHT] == True:
        Rocket_x =+ 1
        move_direction = right = True
    
      
    if keys[pygame.K_LEFT] == True:
        Rocket_x =- -1
        move_direction = left = True
        
        

# Making the planets move left and right        
    if move_direction == 'right':
        planet_x = planet_x + 1
        if planet_x == 300:
            move_direction = 'left'
    else:
        planet_x = planet_x - 1
        if planet_x == 0:
            move_direction = 'right'

    if fired is True:
        bullet_y = bullet_y - 2
        if bullet_y == 40:
            fired = False
            bullet_y = 390        


            
    
     #blitting the images   
    screen.blit(background,(0,0))
    screen.blit(text,(0,0))
    screen.blit(planet,[planet_x,40])
    screen.blit(bullet,[159,bullet_y])
    screen.blit(Rocket_x,(160,390))
    
    #collsion,score, making a planet appear after the other
    if bullet_y < 80 and planet_x > 120 and planet_x < 180:
        score += 1
        text = font.render('Score: '+str(score),True,(255,255,255))
        p_index = p_index + 1
        if p_index < len(planets):
            planet = pygame.image.load(planets[p_index])
            planet_x = 10
        else:
            print('YOU WIN')
            print('Instagram:' + instagram)
            
            run = False



    pygame.display.update()
pygame.quit()   
