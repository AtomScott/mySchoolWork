```C
#include <Sprite.h>
#include <Matrix.h>

int sensor = 0;
double sensval;

Matrix mtx = Matrix(10, 12, 11);
Sprite tsuku = Sprite( // スプライト 1 文字目
8, 7,
B01000000,
B01000000,
B10000000,
B10000000,
B10000000,
B01000000,
B10000000);
Sprite ba = Sprite( // スプライト 2 文字目
8, 7,
B10000000,
B00000000,
B10000000,
B00000000,
B10000000,
B10000000,
B11000000);
void setup() { 
  mtx.clear(); 
}
int x = 0;
void loop() {
  mtx.write(0 - x, 0, tsuku); // スプライトの書き込み
  mtx.write(8 - x, 0, ba);
  mtx.write(16 - x, 0, tsuku);
  delay(100);
  sensval = analogRead(sensor);
  if(sensval > 600){
    for (int j = 0; j < 8; j++) {
      for (int i = 0; i < 8; i++) {
        mtx.write(i, j, HIGH); // (i,j) の位置のLED を点灯
        delay(100);
        mtx.write(i, j, LOW); // (i,j) の位置のLED を消灯
      }
    }
  }
  if (x == 16) x = 0;
  x++;
}
```

```C
#include <Sprite.h>
#include <Matrix.h>

int sensor = 0;
double sensval;

Matrix mtx = Matrix(10, 12, 11);
Sprite p1 = Sprite( // スプライト 1 文字目
8, 7,
B00011100,
B00010100,
B01011100,
B00111110,
B00001001,
B00010100,
B00100100);
Sprite p2 = Sprite( // スプライト 2 文字目
8, 7,
B00011100,
B00010100,
B00011100,
B01111111,
B00001000,
B00010100,
B00010100);
Sprite p3 = Sprite( // スプライト 2 文字目
8, 7,
B00011100,
B00010100,
B00011101,
B00111110,
B01001000,
B00010100,
B00010010);
Sprite p4 = Sprite( // スプライト 2 文字目
8, 7,
B00000000,
B00011100,
B00010100,
B00011100,
B00111110,
B01011101,
B00011100);
Sprite p5 = Sprite( // スプライト 2 文字目
8, 4,
B00011100,
B00100010,
B00100010,
B00100010);
Sprite p6 = Sprite( // スプライト 2 文字目
8, 4,
B00000000,
B01000001,
B01000001,
B01000001);
Sprite p7 = Sprite( // スプライト 2 文字目
8, 4,
B00000000,
B00000000,
B00000000,
B00000000);
void setup() { 
  mtx.clear(); 
}
int x = 0;
void loop() {

  delay(100);
  sensval = analogRead(sensor);
  while(1){
    mtx.write(0, 0, p1);
    if(analogRead(sensor) > 550)break;
    delay(200);
    mtx.write(0, 0, p2); // スプライトの書き込み
        if(analogRead(sensor) > 550)break;
    delay(200);
    mtx.write(0, 0, p3); // スプライトの書き込み
        if(analogRead(sensor) > 550 || analogRead(sensor) < 450)break;
    delay(200);
  }
mtx.write(0, 0, p4); // スプライトの書き込み
delay(1000);
//    mtx.write(0, 0, p5); // スプライトの書き込み
//    delay(200);
//    mtx.write(0, 0, p6); // スプライトの書き込み
//    delay(200);
//    mtx.write(0, 0, p7); // スプライトの書き込み
//    delay(600);
  
}
```
