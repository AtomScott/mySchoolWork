##3.1 太陽電池の入力電圧によって高さの違う音を再生する

####1.	演習の目的
　この実験では，太陽電池と圧電スピーカを Arduino に接続し，太陽電池から発生した電圧の変化
に従って，圧電スピーカから出す音の高さを変化させる
####2.	問題解決の方針
テキストの実験手順に従って、太陽電池のから発生した変化によって音を発生させる。
以下の二つのプログラムを作成し、それぞれできているか確認する。

1.太陽電池に当たる光量を変化させた時に，それに伴って圧電スピーカから聞こえる音の高さが変化する。

2.太陽電池に当たる光量を変えた時に発生する電圧の変化を確認し、それに応じて音の高さが、おおよそ楽器の高さの幅になるようにパラメータを調節し，音の高さが変化する

####3.	プログラム
 ```C
 //−−−−− 実験課題3-2 −−−−−−−
 int G=392;
int G#=415.;
int A=440;
int A#=466;
int B=494.;
int C=523;
int C#=554;
int D=587;
int D#=622;
int E=659;
int F=698;
int F#=740;

int B16 = 125;
int B8 = B16 * 2;
int B4 = B16 * 4;
int B2 = B16 * 8;
int speaker = 2;

void sound (int hz){
  int tone_delay = 1/(hz*2)*1000000;
  tone_delay = hz;
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
}
 ```
####4.	実行結果
接続の仕方や，どのデジタル出力ピン およびアナログ入力ピンに接続するかのグループでの工夫
太陽電池からの入力電圧の違いによって，どのように音の高さ（ピッチ）が変わるようにしたか
太陽電池に当たる光量を変化させた時に，それに伴って圧電スピーカから聞こえる音の高さが変化する
太陽電池に当たる光量を変えた時に発生する電圧の変化を確認し、，それに応じて音の高さが，おおよそ楽器の高さの幅になるようにパラメータを調節し，音の高さが変化する
####6.	参考文献
「情報科学基礎実験!第2章Arduinoを用いた基礎的な実験」テキスト
####7.	謝辞
この実験をレポートとして形にすることが出来たのは、ペアの杉崎さん、TAの皆様に協力していただいたおかげです｡
協力していただいた皆様へ心から感謝の気持ちと御礼を申し上げたく、謝辞にかえさせていただきます｡ 　
