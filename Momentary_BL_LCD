#include <Wire.h>            // handles our I2C communication
#include "rgb_lcd.h"
#include <math.h>

int a;
float temperature;
int B=3975;                  //B value of the thermistor
float resistance;
int thermoPin = 0;           // pin the thermometer module is plugged into

rgb_lcd lcd;                 // instantiate our LCD

int buttonVal = 0;
int buttonPin = 2;           // pin the button module is plugged into

// Change these values to what you want the RGB of the backlight to be
const int colorR = 255;
const int colorG = 255;
const int colorB = 255;

unsigned long buttonTime = 0;          // self-defined timer for the button presses
unsigned long printerTime = 0;     // self-defined timer for the display

void setup() 
{
  // set up the LCD's number of columns and rows, Grove RGB Backlight LCD is 16x2
  lcd.begin(16, 2);
  
  // we will be using a digital button
  pinMode(buttonPin, INPUT);
  
  // assign the RGB values (in that order).  We want no colors
  lcd.setRGB(0, 0, 0);
  
  // print the message on line 1
  lcd.print("Temperature (F):");
}

void loop() 
{  
  buttonVal = digitalRead(buttonPin);
  
  // if the button is pressed (i.e. a logic HIGH), light the display and start (reset) the timer
  if(buttonVal != 0)
  {
    lcd.setRGB(colorR, colorG, colorB);
    buttonTime = millis();
  }
  
  // Turn off the backlight after 5 seconds from the last button press
  if(millis()-buttonTime >= 5000)
  {
    lcd.setRGB(0,0,0);
  }
  
  a=analogRead(thermoPin);
  resistance=(float)(1023-a)*10000/a; //get the resistance of the sensor
  temperature=1/(log(resistance/10000)/B+1/298.15)-273.15; //convert to temperature (based on info from Grove)
  
  // display the temperature every second
  if(millis()-printerTime >= 1000)
  {
    // set the cursor to first column, second row and print the temperature
    // (note: line 1 is the second row, because of 0-indexing in C):
    lcd.setCursor(0, 1);
    lcd.print(temperature*(1.8)+32);
    printerTime = millis();           // reset the printing timer
  }
  
  delay(10);      // have a slight delay in our program
}
