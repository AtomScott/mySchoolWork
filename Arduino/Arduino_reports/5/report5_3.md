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
