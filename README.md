//Proyecto-final-digital-1
//Proyecto mano robotica

#include <Servo.h>


// Definición de pines para cada servo
#define servo1 (1 << PB1)
#define servo2 (1 << PB2)
#define servo3 (1 << PB3)
#define servo4 (1 << PB4)
#define servo5 (1 << PB5)
Servo myservo1;
Servo myservo2;
Servo myservo3;
Servo myservo4;
Servo myservo5;




void setup() {
  myservo1.attach(9);
  myservo2.attach(10);
  myservo3.attach(11);
  myservo4.attach(12);
  myservo5.attach(13);

  
  
  //Configurar interrupciones 
  PCMSK2 |= (1 << PCINT18);
  PCMSK2 |= (1 << PCINT19);
  PCMSK2 |= (1 << PCINT20);
  PCMSK2 |= (1 << PCINT21);
  PCMSK2 |= (1 << PCINT22);
  

  
}

// TIMER 0 for interrupt frequency 1000 Hz:
cli(); // stop interrupts
TCCR0A = 0; // set entire TCCR0A register to 0
TCCR0B = 0; // same for TCCR0B
TCNT0  = 0; // initialize counter value to 0
// set compare match register for 1000 Hz increments
OCR0A = 249; // = 16000000 / (64 * 1000) - 1 (must be <256)
// turn on CTC mode
TCCR0B |= (1 << WGM01);
// Set CS02, CS01 and CS00 bits for 64 prescaler
TCCR0B |= (0 << CS02) | (1 << CS01) | (1 << CS00);
// enable timer compare interrupt
TIMSK0 |= (1 << OCIE0A);
sei(); // allow interrupts


void loop() {
  // Controlar los ángulos de los servos
  myservo1.write(90);
  myservo2.write(90);
  myservo3.write(90);
  myservo4.write(90);
  myservo5.write(90);

  delay(2000);

 
  myservo1.write(0);
  myservo2.write(0);
  myservo3.write(0);
  myservo4.write(0);
  myservo5.write(0);

  delay(2000);
  
  int count0 = 0;
  
  ISR(TIMER0_COMPA_vect){ //1000HZ
   //interrupt commands for TIMER 0 here
   count0++;
   if (count0 == 900){
      count0 = 0;
   myservo1.write(180);
   }
    else ( count0 == 900){
      count0 =1;
     myservo1.write(0);
   myservo2.write(180);
      
      else (count0 == 900){
        

   
 
}
  
}
