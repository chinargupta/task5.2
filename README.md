from tkinter import *   // Import the tkinter library for making the GUI
from turtle import color // Import the color library 
from gpiozero import LED // Import LED library to define the LED
import tkinter.font as style // Import the font to define the style
import RPi.GPIO // Import Rpi.Gpio library for configure , read and write to GPIO pins

RPi.GPIO.setmode(RPi.GPIO.BCM)

led_red = LED(26)    // define the red led pin with the Rasberry pi gpio pin 26
led_white =LED(18)   // define the white pin with the Rasberry pi gpio pin 18
led_green = LED(20)   // define the green pin with the Rasbery pi gpio pin 20
 

root = Tk() // It helps to display the root window and manages all the other components of the tkinter application.
root.geometry("300x200") // Display size
root.title("Radiobuttonblinker") // Gui page title name

var = IntVar()

def led1(): // define led1 function
	if led_red.is_lit:   // Here I use if loop and write down the condition
		led_red.off()
		ledButton1["text"] = "Turn RED-LED ON"

	else:  // here I write down the else condition
		led_red.on() // Only red led on another two led are off
		led_white.off()
		led_green.off()
		ledButton1["text"] = "Turn RED-LED OFF"

def led2(): // Define the next function
	if led_green.is_lit: // Here I use if loop and write down the condition
		led_green.off()
		ledButton1["text"] = "Turn GREEN-LED ON"

	else:
		led_red.off() // Only green led on and other two led are off
		led_white.on()
		led_blue.off()
		ledButton1["text"] = "Turn GREEN-LED OFF" // show the display this text

def led3(): // Define the next function
	if led_blue.is_lit: // Here I use if loop and write down the conditon
		led_green.off()
		ledButton1["text"] = "Turn BLUE-LED ON"

	else:
		led_red.off()  // Only blue led on and another two led are off
		led_white.off()
		led_green.on()
		ledButton1["text"] = "Turn BLUE-LED OFF"

def close(): // define close function
	RPi.GPIO.cleanup() // To clean  up all the ports which I used
	root.destroy()



Label(root, text="Which LED you want to Blink?", font="lucida 12 bold", justify=LEFT, padx=14).pack() // To make Gui I use label tag

ledButton1 = Radiobutton(root, text="Red", padx=14,  font="Times" , command = led1,variable=var,bg="#DC143C" , value=1, height = 2).pack() // I use radiobutton to craete the button
ledButton2 = Radiobutton(root, text="white", padx=14, font="Times" , command= led2,variable=var, bg="#7FFF00", value=2, height = 2).pack()
ledButton3 = Radiobutton(root, text="green", padx=14, font="Times" , command = led3,variable=var, value=3, bg="#0000FF", height = 2).pack()
Button(root, text = "QUIT", font = "Times", command = close, bg = "red", height = 1).pack()
root.mainloop()  // This is the method which we execute we want to run our applications
