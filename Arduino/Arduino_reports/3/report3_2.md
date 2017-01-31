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
1.太陽電池に当たる光量を変化させた時に，それに伴って圧電スピーカから聞こえる音の高さが変化するプログラム。
 ```C
//−−−−− 実験課題3-2 −−−−−−−
int G=392;
int Gs=415.;
int A=440;
int As=466;
int B=494.;
int C=523;
int Cs=554;
int D=587;
int Ds=622;
int E=659;
int F=698;
int Fs=740;

int B16 = 125;
int B8 = B16 * 2;
int B4 = B16 * 4;
int B2 = B16 * 8;

int sensVal;

//pins
int speaker = 13;
int sensorPin = 1;

void sound (int hz){
        int tone_delay = 1/(hz*2)*1000000;
        tone_delay = hz;
        digitalWrite(speaker,HIGH);
        delayMicroseconds(tone_delay);
        digitalWrite(speaker,LOW);
        delayMicroseconds(tone_delay);
}

void play (int tone, int length){
        unsigned long tone_end_time;
        tone_end_time = millis() + length;
        while (millis() < tone_end_time) {
                sound(tone);
        }
}

void yasumi (int length){
        delay(length);
}

void setup (){
        pinMode(speaker,OUTPUT);
        Serial.begin(9600);
}

void loop (){
        sensVal = analogRead(sensorPin);
        Serial.println(sensVal);
        play(sensVal, B4);
}
 ```
2.太陽電池に当たる光量を変えた時に発生する電圧の変化を確認し、それに応じて音の高さが、おおよそ楽器の高さの幅になるようにパラメータを調節し，音の高さが変化する
```c

//−−−−− 実験課題3-2 −−−−−−−
int G=392;
int Gs=415.;
int A=440;
int As =466;
int B=494.;
int C=523;
int Cs =554;
int D=587;
int Ds =622;
int E=659;
int F=698;
int Fs =740;

int B16 = 125;
int B8 = B16 * 2;
int B4 = B16 * 4;
int B2 = B16 * 8;

int sensVal;

//pins
int speaker = 13;
int sensorPin = 1;

void sound (int hz){
        hz = (hz-50)/10;
 
        switch (hz) {
        case 1:
                hz=G;
                    break;
        case 2:
                hz=Gs;
                    break;
        case 3:
                hz=A;
                    break;
        case 4:
                hz=As;
                    break;
        case 5:
                hz=B;
                    break;
        case 6:
                hz=C;
                    break;
        case 7:
                hz=Cs;
                    break;
        case 8:
                hz=D;
                    break;
        case 9:
                hz=Ds;
                    break;
        case 10:
                hz=E;
                    break;
        case 11:
                hz=F;
                    break;
        case 12:
                hz=Fs;
                    break;

        default:
                return;
                break;
        }
        int tone_delay = 1/(hz*2)*1000000;
        tone_delay = hz;
        digitalWrite(speaker,HIGH);
        delayMicroseconds(tone_delay);
        digitalWrite(speaker,LOW);
        delayMicroseconds(tone_delay);
}

void play (int tone, int length){
        unsigned long tone_end_time;
        tone_end_time = millis() + length;
        while (millis() < tone_end_time) {
                sound(tone);
        }
}

void yasumi (int length){
        delay(length);
}

void setup (){
        pinMode(speaker,OUTPUT);
        Serial.begin(9600);
}

void loop (){

        sensVal = analogRead(sensorPin);
               Serial.println(sensVal);
        play(sensVal, B4);
}
```
####4.	実行結果
太陽電池の入力電圧に応じて，スピーカーの出力する音を変化させることに成功した．

####5．考察
###### 接続の仕方や，どのデジタル出力ピン およびアナログ入力ピンに接続するかのグループでの工夫
アナログピンに太陽電池を接続し，スピーカーはデジタルピンに接続した．

###### 太陽電池からの入力電圧の違いによって，どのように音の高さ（ピッチ）が変わるようにしたか
* 太陽電池に当たる光量を変化させた時に，それに伴って圧電スピーカから聞こえる音の高さが変化する
シリアルモニターに太陽光の入力電圧を表示し，その結果を以下のヒストグラムにまとめた．
![alt text]( https://github.com/AtomScott/mySchoolWork/blob/master/Arduino/Arduino_reports/3/histogram1.png  "Histogram")
一つめのプログラムでは，入力電圧を音の周波数として，そのままスピーカーに出力したため，入力電圧があまりにも低くなると聞こえなくなることがあった．またヒストグラムから分かる通り，160hzの音の出力が最も大きかった．

* 太陽電池に当たる光量を変えた時に発生する電圧の変化を確認し、，それに応じて音の高さが，おおよそ楽器の高さの幅になるようにパラメータを調節し，音の高さが変化する
上のヒストグラムを参考に，入力電圧が10変わる毎に音もそれに応じて変化するようにした．
####6.	参考文献
「情報科学基礎実験!第2章Arduinoを用いた基礎的な実験」テキスト
####7.	謝辞
この実験をレポートとして形にすることが出来たのは、ペアの杉崎さん、TAの皆様に協力していただいたおかげです｡
協力していただいた皆様へ心から感謝の気持ちと御礼を申し上げたく、謝辞にかえさせていただきます｡ 　
