3.4 タクトスイッチを使った簡易キーボードの制作
この実験では，タクトスイッチを用いて，各スイッチを音階に対応させ，各音階に対応するスイッ
チが押された時に，それに対応した高さの音を鳴らすような，簡易キーボードを作成する．なお，2 つ
以上のスイッチは同時には押されないとする．なお，この実験では，最後に，TA に動作確認のチェックを
受ける必要がある．
6
実験手順
1. この実験では，圧電スピーカの２つの入力コード（赤と黒）を，一方（赤）を Arduino のデジ
タル出力に，もう一方（黒）を，GND にワニ口クリップコードで接続する．さらに，5 個以上
のタクトスイッチを，一方は Arduino ボードの別々のデジタル入力に直接， もう一方をすべ
て GRD に接続せよ．なお，後述のスケッチ作成のヒントで述べるが，今回はプルアップ抵抗や
プルダウン抵抗は省略してよい．接続の仕方や，どのデジタル入 出力ピンに接続するかは，各
グループで工夫して決めよ．参考のために，8 個のタクトス イッチを配線した例を，図2 に示
しておく．
l 配線をする際には，USB ケーブルを Arduino ボードから外すこと．
l 配線においては，Arduino ボードの接続ピンの番号などに注意すること．
2. ドレミファソ（タクトスイッチが 5 つの時）あるいは，ドレミファソラシド（タクトスイッチ
が 8 つの時）の音階を各タクトスイッチに対応させ，対応するタクトスイッチが 押された時
に，その音階の音が鳴り続けスイッチを離すと音が止まるようなスケッチを 作成せよ．スケッ
チの作成にあたっては，後述の作成のヒントを参考にすること．
3. タクトスイッチを押して，音階や曲を演奏してみよ．
4. この実験については，完成したら，TA を呼んで，正しく動作していることを確認してもらう必
要がある．

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

int G2=392*2;
int Gs2=415*2;
int a2=440*2;
int As2 =466*2;
int b2=494*2;
int C2=523*2;
int Cs2 =554*2;
int D2=587*2;
int Ds2 =622*2;
int E2=659*2;
int F2=698*2;
int Fs2 =740*2;

int B16 = 125;
int B64 = B16/4;
int B32 = B16/2;

int B8 = B16 * 2;
int B6 = B16 * 3;
int B4 = B16 * 4;
int B3 = B16 * 6;
int B2 = B16 * 8;

int sw1 = 2;
int sw2 = 4;
int sw3 = 6;
int sw4 = 8;
int sw5 = 10;


//pins
int speaker = 13;
int sensorPin = 1;

int swpress;
int swlast;
int swnow;
int now;
int dd;
int ldt;

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
        pinMode(sw1, INPUT);
        pinMode(sw2, INPUT);
        pinMode(sw3, INPUT);
        pinMode(sw4, INPUT);
        pinMode(sw5, INPUT);
}

void loop (){

        digitalWrite(sw1, LOW);
        digitalWrite(sw2, LOW);
        digitalWrite(sw3, LOW);
        digitalWrite(sw4, LOW);
        digitalWrite(sw5, LOW);
        delay(30);
        if(digitalRead(sw1)==HIGH) {
                swpress=1;
        }
        if(digitalRead(sw2)==HIGH) {
                swpress=2;
        }
        if(digitalRead(sw3)==HIGH) {
                swpress=3;
        }
        if(digitalRead(sw4)==HIGH) {
                swpress=4;
        }
        if(digitalRead(sw5)==HIGH) {
                swpress=5;
        }

        while(1) {
                switch (swpress) {
                case 1:
                        play(C,B2);
                        break;
                case 2:
                        play(D,B2);
                        break;
                case 3:
                        play(E,B2);
                        break;
                case 4:
                        play(F,B2);
                        break;
                case 5:
                        play(G,B2);
                        break;
                default:
                        break;
                }
        }

  
}
```
