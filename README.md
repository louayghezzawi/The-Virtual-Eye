# The-Virtual-Eye
A project that help sightless people to detect obstacles in his pathway - IEA Raspberry Pi Competition Entry
import RPi.GPIO as GPIO
import time
import pygame

pygame.init()
pygame.mixer.music.load("/home/pi/Desktop/18925_acclivity_chimebar-g6-nd.ogg")
pygame.mixer.music.play()
time.sleep(1.5)

#Right Triger =26
#Right Echo=24

#Center Triger =18
#Center Echo =16

#Left Triger = 12
#Left Echo =10

GPIO.setwarnings(False)
GPIO.setmode(GPIO.BOARD)

#Left Ultra
GPIO.setup(12,GPIO.OUT)
GPIO.setup(10,GPIO.IN)
#Center Ultra
GPIO.setup(18,GPIO.OUT)
GPIO.setup(16,GPIO.IN)
#Right Ultra
GPIO.setup(26,GPIO.OUT)
GPIO.setup(24,GPIO.IN)
signleOff=0
while True:
    #StartLeft
    GPIO.output(12,False)
    time.sleep(0.3)
    GPIO.output(12,True)
    time.sleep(0.001)
    GPIO.output(12,False)

    while GPIO.input(10)==0:
        signalOff=time.time()

    while GPIO.input(10)==1:
        signalOn=time.time()

    timePassed=signalOn-signalOff
    distance1=timePassed*17000

    print distance1," Left cm"
    pygame.init()
    pygame.mixer.music.load("/home/pi/python_games/beep1.ogg")   
    if distance1 >60 and distance1 <100:
	pygame.mixer.music.play() 
    if distance1 <= 60:
        pygame.mixer.music.load("/home/pi/Desktop/12.ogg")
	pygame.mixer.music.play()
    #End Left
    #Start Center Ultra

    GPIO.output(18,False)
    time.sleep(0.3)
    GPIO.output(18,True)
    time.sleep(0.001)
    GPIO.output(18,False)

    while GPIO.input(16)==0:
        signalOff=time.time()

    while GPIO.input(16)==1:
        signalOn=time.time()

    timePassed=signalOn-signalOff
    distance2=timePassed*17000

    print distance2," Center cm"

    pygame.init()
    pygame.mixer.music.load("/home/pi/python_games/beep1.ogg")   
    if distance2 >60 and distance2 <100:
	pygame.mixer.music.play() 
    if distance2 <= 60:
        pygame.mixer.music.load("/home/pi/Desktop/12.ogg")
	pygame.mixer.music.play()
	
	

    #EndCenter
  
    #Start Right Ultra

    GPIO.output(26,False)
    time.sleep(0.3)
    GPIO.output(26,True)
    time.sleep(0.001)
    GPIO.output(26,False)

    while GPIO.input(24)==0:
        signalOff=time.time()

    while GPIO.input(24)==1:
        signalOn=time.time()

    timePassed=signalOn-signalOff
    distance3=timePassed*17000


    print distance3," Right cm"
    pygame.init()
    pygame.mixer.music.load("/home/pi/python_games/beep1.ogg")   
    if distance3 >60 and distance3 <100:
	pygame.mixer.music.play() 
    if distance3 <= 60:
        pygame.mixer.music.load("/home/pi/Desktop/12.ogg")
	pygame.mixer.music.play()

GPIO.cleanup()
