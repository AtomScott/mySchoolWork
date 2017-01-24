##2.6 チャタリング防止について

###1.	演習の目的
　実験レポート1.5で述べた通り、テキストに提示されていたチャタリング防止の方法で誤動作が起こっていたため、その理由とより防止方法を考える。
###2.	問題解決の方針
　テキストに提示された方法と単純にdelay関数を使用した方法を比較する。
 違いがなければ、チャタリングが起きたときと起きなかったときを比較して、チャタリングを防ぐための最小delay時間を見つける。
 また、比較するためにスイッチが反応した回数と、反応した時間をデータをcsv形式で出力されるようにした。
###3.	プログラム
```c
#include <stdio.h>
unsigned long time;
int SW = 2;
int swnow;
int swlast;
int count;

long ldt = 0;
//dd のタイムを変更しながら実験する
long dd = 0;

void setup(){
   Serial.begin(9600);
   pinMode(SW, INPUT);
   Serial.println("Using textbook");
   Serial.println("Count, Time");
}

void loop(){

  swnow = digitalRead(SW);
  if(swlast == LOW && swnow == HIGH){
    //delay(50);　
    int now = millis();
    if((now-ldt)>dd){
      onPress();
    }
    ldt = now;
  }
  swlast = swnow;
}

void onPress(){
  Serial.print(++count);  
  Serial.print("  ");
  time = micros();
  Serial.print(time);
  Serial.print("\n");
}    
    ldt = now;
  }
  swlast = swnow;
}


void onPress(){
  switch(state++ % 3){   
   case 0:
     digitalWrite(gre, HIGH);
     digitalWrite(red, LOW);
     break;
   case 1:
     digitalWrite(yel, HIGH);
     digitalWrite(gre, LOW);
     break;
   case 2:
     digitalWrite(red, HIGH);
     digitalWrite(yel, LOW);
     break;
  }

}
```
###4.	実行結果
| delayの種類と時間|チャタリングを起こした回数|
| :------------:|:-------------:| 
| no delay time | 12| 
| delay(200) |0| 
| dd=200| 0 | 
|delay(50)|7|
|dd=50|5|
###5.	結果に関する検討・考察
すべてのチャタリング防止方法をあわせて、計２４回のチャタリングが起きていることが分かる。チャタリングを起こしたときのスイッチを押した具体的な間隔は分からないが、スイッチを押した間隔が短いもの２４個をチャタリングを起こした間隔と推定することができる。以下
チャタリングを起こした間隔順にデータを並べ、以下のテーブルとグラフを作成した。
No.|時間|チャタリングの有無
::|::|::
22|172652|有
23|175836|有
24|178240|無
25|179132|無
26|185800|無

###6.	参考文献
「情報科学基礎実験!第2章Arduinoを用いた基礎的な実験」テキスト
###7.	謝辞
この実験をレポートとして形にすることが出来たのは、ペアの杉崎さん、TAの皆様に協力していただいたおかげです｡
協力していただいた皆様へ心から感謝の気持ちと御礼を申し上げたく、謝辞にかえさせていただきます｡ 　

