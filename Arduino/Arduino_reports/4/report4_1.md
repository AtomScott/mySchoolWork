# 3.3 点滅するL E D の移動

## 1.演習の目的

複数あるLEDの点滅を制御することを学ぶ

## 2.問題解決の方針

3.1.<br>
1 度に点灯する LED は 1 つとし、点灯する LED を一定時間 ごとに変更するようにする。これが、繰り返し実行されるようにする。全ての LED が点灯され ることを確認することで、正しく配線できていることも確認する。

3.2.<br>
点灯する LED が 1 方向にのみ移動するのではなく、端から端まで行ったり来たりするよう にしてみる。

## 3.プログラム

### 3.1.のプログラム

```arduino
int ledarray[10];

void setup(){
  for(int i=0; i<10;i++){
    ledarray[i] = i+2;
    pinMode(ledarray[i], OUTPUT);
  }
Serial.begin(9600);
}

void loop(){
  for(int i=0; i < picsize; i++){
    digitalWrite(ledarray[i],HIGH);
    delay(20);
    digitalWrite(ledarray[i],LOW)
  }
}
```

3.2.のプログラム

```arduino
int ledarray[10];

void setup(){
  for(int i=0; i<10;i++){
    ledarray[i] = i+2;
    pinMode(ledarray[i], OUTPUT);
  }
Serial.begin(9600);
}

void loop(){
  for(int i=0; i < 10; i++){
    digitalWrite(ledarray[i],HIGH);
    delay(20);
    digitalWrite(ledarray[i],LOW)
  }
  for(int i=9; i > 0; i--){
    digitalWrite(ledarray[i],HIGH);
    delay(20);
    digitalWrite(ledarray[i],LOW)
  }
}
```

## 4.実行結果

２つの課題とも，指定通りにledは点滅し，課題の目的を達成することが確認できた．

## 5.考察
ledのsetupを工夫することができた．
以下のように，ledpinをそれぞれ配列に格納することでfor文を用いて簡単にsetupすることができることが分かった．
```Arduino
void setup(){
  for(int i=0; i<10;i++){
    ledarray[i] = i+2;
    pinMode(ledarray[i], OUTPUT);
  }
Serial.begin(9600);
}
```

## 6.参考文献

「情報科学基礎実験!第2章Arduinoを用いた基礎的な実験」テキスト

## 7.謝辞

この実験をレポートとして形にすることが出来たのは、ペアの杉崎さん、TAの皆様に協力していただいたおかげです｡ 協力していただいた皆様へ心から感謝の気持ちと御礼を申し上げたく、謝辞にかえさせていただきます｡
