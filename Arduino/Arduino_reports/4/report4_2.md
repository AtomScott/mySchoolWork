```C
int ledarray[10];
int picsize = 35;
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

}

void loop(){
  for(int i=0; i < picsize; i++){
    display(picture[i]);
  }
}

void display(char* pic){
  int digits[picsize];
  for(int i = 0; i <10; i++){
   digits[i] = pic[i]-'0';
   Serial.print(digits[i]);
  }
  
  for(int i = 0; i <10; i++){
   if(digits[i]==0){
    digitalWrite(ledarray[i],LOW); 
   }else if(digits[i]==1){
    digitalWrite(ledarray[i],HIGH); 
   }
  }
  
  delay(5);
}
```
