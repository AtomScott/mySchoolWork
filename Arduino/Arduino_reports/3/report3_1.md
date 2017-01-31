##3.1 スイッチによるArduinoボードLEDの点滅

####1.	演習の目的
　この実験は，ピエゾ素子（圧電スピーカ）を，Arduino のデジタル出力に接続して，その出力
電圧を，高速にHIGH とLOW と切り替えることで，圧電スピーカを振動させ，圧電スピーカから，
任意の周波数の音を発生させる。
####2.	問題解決の方針
　テキストに従って、音を発生させる。
####3.	プログラム
 ```C
 //−−−−− 実験課題3-1 −−−−−−−
 int a = 440;
int b = 880;
int B16 = 125;
int B8 = B16 * 2;
int B4 = B16 * 4;
int B2 = B16 * 8;
int speaker = 2;

void sound (int hz){
  int tone_delay = 1/(hz*2)*1000000;
digitalWrite(speaker ,HIGH);
delayMicroseconds(tone_delay);
digitalWrite(speaker ,LOW);
delayMicroseconds(tone_delay);
}

void play (int tone, int length){
unsigned long tone_end_time;
tone_end_time = millis() + length;
while (millis() < tone_end_time){
sound(tone);
}
}

void yasumi (int length){
delay(length);
}

void setup (){
pinMode(speaker ,OUTPUT);
}

void loop (){
play(a, B4);
yasumi (2000);
play(b, B4);
}
 ```
####4.	実行結果
440hzと880hzの音を発生することができた。
####5.	結果に関する検討・考察
sound メソッドに以下のコードを追加した。
```C
 int tone_delay = 1/(hz*2)*1000000;
 ```
 このようにすることによって、880hzの音を出したければ、そのままそのhzを引数として渡せるようになった。
####6.	参考文献
「情報科学基礎実験!第2章Arduinoを用いた基礎的な実験」テキスト
####7.	謝辞
この実験をレポートとして形にすることが出来たのは、ペアの杉崎さん、TAの皆様に協力していただいたおかげです｡
協力していただいた皆様へ心から感謝の気持ちと御礼を申し上げたく、謝辞にかえさせていただきます｡ 　
