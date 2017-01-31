##3.3 ドレミの音階の再生と簡単な音楽の演奏

####1.	演習の目的
　この実験では，Arduino に接続された圧電スピーカから，ドレミのような規則的な音階を再生
するとともに，それに基づいて簡単な音楽を演奏する。
####2.	問題解決の方針
テキストの実験手順に従って、太陽電池のから発生した変化によって音を発生させる。
以下の３つのプログラムを作成し、それぞれできているか確認する。
1. ドレミの音階を任意の長さだけ再生できるようなスケッチを作成
2. ドレミファソラシドを続けて再生するような，スケッチを作成
3. 簡単な曲を演奏する
####3.	プログラム
1. ドレミの音階を任意の長さだけ再生できるようなスケッチを作成
```C

//−−−−− 実験課題3-3 −−−−−−−
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
        //playの引数に任意の音程，長さを入力することができる．
        //ここではすべての音を繰り返し，鳴らすようにしている．
        for(int val=0; val <11; val++) {
                play(val, B4);
                delay(100);
        }
}

```
2. ドレミファソラシドを続けて再生するような，スケッチを作成
```C

//−−−−− 実験課題3-3 −−−−−−−
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
        //playの引数に任意の音程，長さを入力することができる．
        //ここではすべての音を繰り返し，鳴らすようにしている．
        for(int val=0; val <11; val++) {
                play(val, B4);
        }
}

```
3. 簡単な曲を演奏する
```C

//−−−−− 実験課題3-3 −−−−−−−
int Gl=392/2;
int Gsl=415/2;
int Al=440/2;
int Asl =466/2;
int Bl=494/2;
int Cl=523/2;
int Csl =554/2;
int Dl=587/2;
int Dsl =622/2;
int El=659/2;
int Fl=698/2;
int Fsl =740/2;

int G=392;
int Gs=415;
int A=440;
int As =466;
int B=494;
int C=523;
int Cs =554;
int D=587;
int Ds =622;
int E=659;
int F=698;
int Fs =740;

int B16 = 125;
int B64 = B16/4;
int B32 = B16/2;

int B8 = B16 * 2;
int B6 = B16 * 3;
int B4 = B16 * 4;
int B3 = B16 * 6;
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
        //曲の部分．
        play(El,B8);
        play(0,B8);
        play(0,B8);
        play(El,B8);
        play(Fsl,B8);
        play(Gl,B8);
        play(0,B8);
        play(C,B8);
        play(0,B8);
        play(B,B3);
        play(B,B2);
        play(A,B8);
        play(0,B8);
        play(0,B8);
        play(A,B8);
        play(C,B8);
        play(B,B4);
        play(0,B8);
        play(Gl,B8);
        play(0,B8);
        play(El,B3);
        play(El,B2);
}

```
####4.	実行結果
ドレミの音階を任意の長さだけ再生できるようなスケッチ，ドレミファソラシドを続けて再生するようなスケッチを作成をし，簡単な曲を演奏することができた．
####5．考察

* ドレミの音階を任意の長さだけ再生できるようなスケッチを作成
以下のコードを見ると，valをincrementさせ，繰り返し低い音程から音程をsound()で演奏していることが分かる．
```C
void loop (){
        //playの引数に任意の音程，長さを入力することができる．
        //ここではすべての音を繰り返し，鳴らすようにしている．
        for(int val=0; val <11; val++) {
                play(val, B4);
                delay(100);
        }
}
```

* ドレミファソラシドを続けて再生するような，スケッチを作成
上記のコードからdelay()を消す続けて再生するようになる．
```C
void loop (){
        //playの引数に任意の音程，長さを入力することができる．
        //ここではすべての音を繰り返し，鳴らすようにしている．
        for(int val=0; val <11; val++) {
                play(val, B4);
                
        }
}
```
* 簡単な曲を演奏する
The Gorillaz の Feel Good Inc を再生した．(https://www.youtube.com/watch?v=HyHNuVaZJ-k)
このときに，ベースラインの楽譜を用いて，楽譜から曲の音程と長さを探した．
####6.	参考文献
「情報科学基礎実験!第2章Arduinoを用いた基礎的な実験」テキスト
####7.	謝辞
この実験をレポートとして形にすることが出来たのは、ペアの杉崎さん、TAの皆様に協力していただいたおかげです｡
協力していただいた皆様へ心から感謝の気持ちと御礼を申し上げたく、謝辞にかえさせていただきます｡ 　
