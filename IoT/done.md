```python
"""
IoT Room Temperature Monitoring System

This script monitors the room temperature using an analog temperature sensor
connected to a microcontroller. Based on the temperature reading, the system
automatically controls a heating element or an air cooler to maintain a
comfortable environment.

Features:
- Reads temperature data from an analog sensor.
- Displays temperature information on an LCD display.
- Activates a cooling system when the temperature is too high.
- Activates a heating system when the temperature is too low.
- Prevents the heater and cooler from operating at the same time.

Hardware Connections:
Pin 0 : Temperature Sensor (Analog Input)
Pin 1 : LCD Display Output
Pin 2 : Heating Element (Digital Output)
Pin 3 : Air Cooler (Digital Output)

Temperature Conditions:
- temp >= 300 → Cooling mode activated
- temp < 200  → Heating mode activated
- 200–299     → Normal temperature (no action required)
"""

from gpio import *
from time import sleep


def main():
    """Initialize hardware pins and continuously monitor room temperature."""

    # Configure pin modes
    pinMode(0, IN)   # Temperature Sensor
    pinMode(1, OUT)  # LCD Display
    pinMode(2, OUT)  # Heating Element
    pinMode(3, OUT)  # Air Cooler

    print("ROOM TEMPERATURE MONITOR")

    while True:
        # Read temperature from sensor
        temp = analogRead(0)

        print("TEMPERATURE:", temp)

        # Display temperature reading
        customWrite(1, "Temp: " + str(temp))

        # Temperature too high → activate cooler
        if temp >= 300:
            digitalWrite(3, HIGH)  # Turn ON cooler
            digitalWrite(2, LOW)   # Turn OFF heater
            customWrite(1, "Cooling... " + str(temp))

        # Temperature too low → activate heater
        elif temp < 200:
            digitalWrite(2, HIGH)  # Turn ON heater
            digitalWrite(3, LOW)   # Turn OFF cooler
            customWrite(1, "Heating... " + str(temp))

        # Temperature within normal range
        else:
            digitalWrite(2, LOW)   # Heater OFF
            digitalWrite(3, LOW)   # Cooler OFF
            customWrite(1, "Normal: " + str(temp))

        # Wait before next reading
        sleep(2)


if __name__ == "__main__":
    main()
    
    
# Tinker CAD simulation
"""
// Blocking polling in tinkercad simulation
/**
Write a simple program that read the digital input. Your work as follows:

- All LEDs are OFF at the start of the program
- Once the program begins. LED1 and LED4 blinks continuously at 1 Hz
-  While the switch SW1 is pressed LED2 is turned ON and stays ON until the switch SW1 is released
- When SW1 is pressed and then released turn ON LED3 for one second and turn it OFF 
*/
/**
int led1 = 2;
int led2 = 3;
int led3 = 4;
int led4 = 5;

int sw1 = 7;

int lastState = HIGH;
bool stopBlink = false;
bool firstStart = true;

void setup()
{
  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  pinMode(led3, OUTPUT);
  pinMode(led4, OUTPUT);

  pinMode(sw1, INPUT_PULLUP);

  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
}

void loop()
{
  if(firstStart == true)
  {
    delay(1000);
    firstStart = false;
  }

  int state = digitalRead(sw1);

  // Blink LED1 and LED4
  if(stopBlink == false)
  {
    digitalWrite(led1, HIGH);
    digitalWrite(led4, HIGH);
    delay(500);

    digitalWrite(led1, LOW);
    digitalWrite(led4, LOW);
    delay(500);
  }

  // LED2 ON while pressed
  if(state == LOW)
  {
    digitalWrite(led2, HIGH);
  }
  else
  {
    digitalWrite(led2, LOW);
  }

  // Detect press
  if(lastState == HIGH && state == LOW)
  {
    stopBlink = true;
    digitalWrite(led1, LOW);
    digitalWrite(led4, LOW);
  }

  // Detect release
  if(lastState == LOW && state == HIGH)
  {
    digitalWrite(led3, HIGH);
    delay(1000);
    digitalWrite(led3, LOW);

    delay(3000);

    stopBlink = false;
  }

  lastState = state;
}
*/


/**
int led1 = 2;
int led2 = 3;
int led3 = 4;
int led4 = 5;

int counter = 0;

void setup()
{
  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  pinMode(led3, OUTPUT);
  pinMode(led4, OUTPUT);
}

void loop()
{
  digitalWrite(led1, counter & 1);
  digitalWrite(led2, (counter >> 1) & 1);
  digitalWrite(led3, (counter >> 2) & 1);
  digitalWrite(led4, (counter >> 3) & 1);

  delay(1000);

  counter++;

  if(counter > 15)
  {
    counter = 0;
  }
}
*/


int led1 = 2; // LSB
int led2 = 3;
int led3 = 4;
int led4 = 5; // MSB

int btn = 6;  // button input

int counter = 0;
int lastState = HIGH;

void setup()
{
  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  pinMode(led3, OUTPUT);
  pinMode(led4, OUTPUT);

  pinMode(btn, INPUT_PULLUP);

  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
}

void loop()
{
  int state = digitalRead(btn);

  // detect button press (HIGH -> LOW)
  if(lastState == HIGH && state == LOW)
  {
    counter++;
    if(counter > 15) counter = 0;

    // update LEDs in reverse order (start from last LED)
    digitalWrite(led4, counter & 1);           // bit0 -> last LED
    digitalWrite(led3, (counter >> 1) & 1);    // bit1
    digitalWrite(led2, (counter >> 2) & 1);    // bit2
    digitalWrite(led1, (counter >> 3) & 1);    // bit3 -> first LED
  }

  lastState = state;

  delay(50); // simple debounce
}
"""


# -------------------------------------------------------------------------------


"""
// C++ code
//
/**
void setup()
{
  pinMode(2, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
}

void loop()
{
  digitalWrite(2, HIGH);
  digitalWrite(3, LOW);
  digitalWrite(4, LOW);
  delay(5000); // Wait for 5000 millisecond(s)
  digitalWrite(2, LOW);
  digitalWrite(3, HIGH);
  digitalWrite(4, LOW);
  delay(5000); // Wait for 5000 millisecond(s)
  digitalWrite(2, LOW);
  digitalWrite(3, LOW);
  digitalWrite(4, HIGH);
  delay(5000); // Wait for 5000 millisecond(s)
}
*/


/**
#include <Adafruit_LiquidCrystal.h>

// Initialize the LCD (use I2C address 0 for default example)
Adafruit_LiquidCrystal lcd(0);

// Temperature sensor pin
const int sensorPin = A0;

void setup() {
  lcd.begin(16, 2);        // 16 columns, 2 rows
  lcd.setBacklight(1);     // Turn on LCD backlight

  lcd.print("Temp Monitor");
  delay(2000);
  lcd.clear();
}

void loop() {
  // Read raw analog value from sensor
  int rawValue = analogRead(sensorPin);

  // Convert analog value to voltage (assuming 5V Arduino)
  float voltage = rawValue * (5.0 / 1023.0);

  // Convert voltage to temperature in Celsius (TMP36)
  float tempC = (voltage - 0.5) * 100.0;

  // Optionally convert to Fahrenheit
  float tempF = tempC * 9.0 / 5.0 + 32.0;

  // Display temperature on LCD
  lcd.setCursor(0, 0);
  lcd.print("Temp: ");
  lcd.print(tempC, 1);  // 1 decimal place
  lcd.print((char)223);  // Degree symbol
  lcd.print("C");

  lcd.setCursor(0, 1);
  lcd.print("Temp: ");
  lcd.print(tempF, 1);
  lcd.print((char)223);
  lcd.print("F");

  delay(2000); // Update every 2 seconds
}
*/


/**
// Simple Arduino Temperature Monitor
// Using Adafruit LiquidCrystal and an LM35 or similar analog temperature sensor

#include <Adafruit_LiquidCrystal.h>

// Initialize the LCD (I2C address 0 for example)
Adafruit_LiquidCrystal lcd(0);

// Analog pin where the temperature sensor is connected
const int sensorPin = A0;

void setup() {
  // Initialize the LCD with 16 columns and 2 rows
  lcd.begin(16, 2);

  // Turn on the LCD backlight
  lcd.setBacklight(1);

  // Display a welcome message for 2 seconds
  lcd.print("Temp Monitor");
  delay(2000);
  
  // Clear the LCD to prepare for temperature readings
  lcd.clear();
}

void loop() {
  // Read the raw analog value from the sensor (0 - 1023)
  int rawValue = analogRead(sensorPin);

  // Convert raw value to Celsius
  // LM35: 10 mV per degree Celsius, Arduino ADC: 5V / 1024 steps ≈ 4.8828125 mV per step
  float tempC = rawValue * 0.48828125; // Each step ≈ 0.488°C

  // Display the temperature on the LCD
  lcd.setCursor(0, 0);      // Start at column 0, row 0
  lcd.print("Temp: ");
  lcd.print(tempC, 1);      // Print with 1 decimal place
  lcd.print(" C");

  // Wait for 1 second before updating again
  delay(1000);
}
*/


/*
Simple Arduino Motion Monitor
Using Adafruit LiquidCrystal and a PIR motion sensor

Purpose
Detect motion and show the system status on the LCD.

Hardware
LED  -> pin 2
Buzzer -> pin 3
PIR sensor -> pin 4
LCD -> Adafruit LiquidCrystal

Behavior
When motion appears the LED and buzzer turn ON and the LCD shows a detection message.
When no motion appears the devices turn OFF and the LCD shows normal monitoring.
*/

#include <Adafruit_LiquidCrystal.h>

// Initialize LCD
Adafruit_LiquidCrystal lcd(0);

// int ledPin = 2;
int buzzerPin = 6; //  8
int motionPin = 5; // 4

int motionState = 0;

void setup()
{
  // pinMode(ledPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  pinMode(motionPin, INPUT);

  lcd.begin(16,2);

  lcd.setCursor(0,0);
  lcd.print("Motion Monitor");

  lcd.setCursor(0,1);
  lcd.print("System Ready");

  delay(3000);
}

void loop()
{
  motionState = digitalRead(motionPin);

  lcd.setCursor(0,0);
  lcd.print("Motion Monitor:");

  if(motionState == HIGH)
  {
    // digitalWrite(ledPin, HIGH);
    digitalWrite(buzzerPin, HIGH);

    lcd.setCursor(0,1);
    lcd.print("Object Detected ");
  }
  else
  {
    // digitalWrite(ledPin, LOW);
    digitalWrite(buzzerPin, LOW);

    lcd.setCursor(0,1);
    lcd.print("No Object       ");
  }

  delay(300);
}
"""
```
