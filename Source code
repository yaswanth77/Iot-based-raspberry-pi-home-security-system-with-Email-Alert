from picamera import PiCamera
from time import sleep
import smtplib
import time
from datetime import datetime
from email.mime.image import MIMEImage
from email.mime.multipart import MIMEMultipart
import RPi.GPIO as GPIO
import picamera
import time

toaddr = 'nadellasivaram@gmail.com'
me = 'yeswanthreddysunkara@gmail.com'
Subject='security alert'
led=17
pir=24
HIGH=1
LOW=0
GPIO.setwarnings(False)
GPIO.setmode(GPIO.BCM)
GPIO.setup(17, GPIO.OUT)            # initialize GPIO Pin as outputs
GPIO.setup(24, GPIO.IN)  

GPIO.output(led , GPIO.HIGH)
P=PiCamera()
P.resolution= (1024,768)
P.start_preview()
    
GPIO.setup(24, GPIO.IN)
while True:
    if GPIO.input(24):
        print("Motion...")
        #camera warm-up time
        time.sleep(2)
        P.capture('movement.jpg')
        time.sleep(10)
        subject='Security allert!!'
        msg = MIMEMultipart()
        msg['Subject'] = subject
        msg['From'] = me
        msg['To'] = toaddr
        fp= open('movement.jpg','rb')
        img = MIMEImage(fp.read())
        fp.close()
        msg.attach(img)

        server = smtplib.SMTP('smtp.gmail.com',587)
        server.starttls()
        server.login(user = 'yeswanthreddysunkara@gmail.com',password='skuysr357')

        server.send_message(msg)
        server.quit()    

while 1:
    if gpio.input(pir)==1:
        gpio.output(led, HIGH)
        capture_image()
        while(gpio.input(pir)==1):
            time.sleep(1)
        
    else:
        gpio.output(led, LOW)
        time.sleep(0.01)
