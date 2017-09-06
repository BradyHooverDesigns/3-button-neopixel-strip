#include <Adafruit_NeoPixel.h>  //sets up a neopixel sketch

const int redButton = 9;         //sets pin 9 to read button presses and set pixel color to red
const int blueButton = 10;       //sets pin 10 to read button presses and set pixel color to blue
const int greenButton = 11;    //sets pin 11 to read button presses and set pixel color to green

int redPin = 0;   //creates a variable for the state of the red button
int bluePin = 0;  //creates a variable for the state of the blue button
int greenPin = 0; //creates a variable for the state of the green button

int red = 0;    //creates red as a variable for hex values 1 through 255
int green = 0;  //creates green as a variable for hex values 1 through 255
int blue = 0;   //creates blue as a variable for hex values 1 through 255

      #define PIN 7             //neopixel strip_a attacked to digital pin 5


// Parameter 1 = number of pixels in strip_a
// Parameter 2 = pin number (most are valid)
// Parameter 3 = pixel type flags, add together as needed:
//   NEO_KHZ800  800 KHz bitstream (most NeoPixel products w/WS2812 LEDs)
//   NEO_KHZ400  400 KHz (classic 'v1' (not v2) FLORA pixels, WS2811 drivers)
//   NEO_GRB     Pixels are wired for GRB bitstream (most NeoPixel products)
//   NEO_RGB     Pixels are wired for RGB bitstream (v1 FLORA pixels, not v2)
Adafruit_NeoPixel strip_a = Adafruit_NeoPixel(100, PIN, NEO_GRB + NEO_KHZ800);

void setup() {
  // put your setup code here, to run once:
  strip_a.begin();
  strip_a.show();   //Initialize all pixels to 'off'

  pinMode (redButton, INPUT);   //sets pin 9 as an input pin to read buttonpresses
  pinMode (blueButton, INPUT);     //sets pin 10 as an input pin to read buttonpresses
  pinMode (greenButton, INPUT);    // sets pin 11 as an input pin to read buttonpresses
  
  Serial.begin(1200); //begins serial communication for tracking buttonpresses
  Serial.println("resetting");  //writes RESETTING into the serial communication

  strip_a.setBrightness(84);  //sets brightness of the strip_a
}

void loop() {
  // put your main code here, to run repeatedly:

  //creates a loop running 60 times each time increasing variable i and writing blue to that pixel
  for (int a=0; a < 100; a++)  {
  redPin = digitalRead(redButton);      //uses variable redPin to identify the position of the red button
  bluePin = digitalRead(blueButton);    //uses variable bluePin to identify the position of the blue button
  greenPin = digitalRead(greenButton);  //uses variable greenPin to identify the position of the green button

  strip_a.show();

  if(redPin == 1) {
      
      //sets red variable to high and green and blue to low
      red = 255;

      //writes red to serial communication
      Serial.println("red");
  
  } //else if(bluePin == 0 && greenPin == 0)  {
//    //if the button is not pressed set red to low
//    red = 0;
//  }

  if(bluePin == 1)  {

    //sets blue variable to high and green and red to low
    blue = 255;
    
    //weites blue to serial communication
    Serial.println("red");
 
  } 
//  else if(greenPin == 0 && redPin == 0) {
//    //if the button is not pressed set blue to low
//    blue = 0;
  }

  if(greenPin == 1) {

    //sets green variable to high
    green = 255;

    //writes green to serial communication
    Serial.println("green");
  
  } 
//    else  if(bluePin == 0 && redPin == 0)  {
    //if the button is not pressed set green to low
//    green = 0;
  }
  
  //uint32_t hue(255,0,0,white); //creates the 32-BIT variable HUE to control the current pixel color

  strip_a.setPixelColor(a,red,green,blue);
  delay(20);
  }
}
