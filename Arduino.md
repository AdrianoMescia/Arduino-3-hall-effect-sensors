# Arduino-3-hall-effect-sensors

#include <SimpleTimer.h>

// thall timer object
SimpleTimer timer;

int hallAPin = 12;
int hallBPin = 11;
int hallCPin = 10;

int hallAState = 0;
int hallBState = 0;
int hallCState = 0;
int state = 0;

int startTime;
int timeTaken;

// a function to be executed periodically
void repeatMe() {
    Serial.print("Total time (s): ");
    Serial.println(millis());
}


void setup() { 

  Serial.begin(9600);
  timer.setInterval(1000, repeatMe);    
  startTime = millis();
}

void loop() {
  timer.run(); 
  
  hallAState = digitalRead(hallAPin);
  hallBState = digitalRead(hallBPin);
  hallCState = digitalRead(hallCPin);
  
  Serial.println(state);
  delay(500);
  
  
  if (hallAState == LOW){
    state = 1;
    
    //find start time
    startTime = millis();
  }
  
  else if (hallBState == LOW) {
    if (state == 1) {
      
      //Serial.println(count); 
      timeTaken = millis() - startTime;
      Serial.println("Time taken: ");
      Serial.print(timeTaken);
      
      state = 0;
    }
  }
  
  else if (hallCState == LOW) {
    state = 0;
  }

}
