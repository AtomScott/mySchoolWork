```C
int ledarray[10];
int picsize = 35;
int sensor = 0;
int delaytime = 0;
double x;
double y;
double sensval;
unsigned long time;
unsigned long ave=0;

char* picture[] = {

  "1111111111",
  "1111111111",
  "0000110000",
  "0000110000",
  "1111111111",
  "1111111111",
  "0000000000",
  "1110000011",
  "1110000011",
  "1111111111",
  "1111111111",
  "1110000011",
  "1110000011",
  "0000000000",
  "0000000000",
  "0000000000",
  "1111111011",
  "1111111011",
  "0000000000",
  "0000000000",
  "0000000000",
  "0000000000",
  "0000000000",
  "1111111011",
  "1111111011",
  "0000000000",
  "0000000000",
  "0000000000",
  "0000000000",
  "0000000000",
  "0000000000",
  "0000000000",
  "0000000000",
  "0000000000",
  "0000000000",
};


void setup(){

  for(int i=0; i<10;i++){
    ledarray[i] = i+2; 
    pinMode(ledarray[i], OUTPUT);
  }

  Serial.begin(9600);
  calibrate();
}

void loop(){

  for(int i=0; i < picsize; i++){
    display(picture[i]);
    sensval = analogRead(sensor);
    y = sensval;
    Serial.print("y,");
    Serial.println(y);
  }
}

void display(char* pic){
  delaytime = ave/picsize;
  
  int digits[picsize];
  for(int i = 0; i <10; i++){
    digits[i] = pic[i]-'0';
  }

  for(int i = 0; i <10; i++){
    if(digits[i]==0){
      digitalWrite(ledarray[i],LOW); 
    }
    else if(digits[i]==1){
      digitalWrite(ledarray[i],HIGH); 
    }
  }

  delay(delaytime);
}


void calibrate(){
  for(int i=0; i<10; i++){
    digitalWrite(ledarray[i],HIGH);
    delay(30);
}
for(int i=9; i>-1; i--){
    digitalWrite(ledarray[i],LOW);
    delay(30);
}


  for(int i=0; i<10; i++){
    digitalWrite(ledarray[i],HIGH);
    time = millis();
    //set
    //基準
    int base = analogRead(sensor);
    delay(100);

    //right to left

    while(1){
      y = analogRead(sensor)-base;
      if(y<-150){
        time = millis();
        break;
      }
    }

    i++;
    digitalWrite(ledarray[i],HIGH);
    //left to right

    while(1){
      y = analogRead(sensor)-base;
      if(y>150){
       time = millis() - time;
        break;
      }
    }
  ave =ave+time;
  }
  ave = ave/5;
Serial.println(ave);

}



```
