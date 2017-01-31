##3.5 音楽の再生をより簡単にするために工夫する
####1.	演習の目的
　report3_3~report3_4において，音楽を再生することが可能になったが，一つの音程を再生するために毎回play()関数に音程の長さと音程を書く必要があった．
 これは時間がかかり，面倒なので，よりよい方法はないかと探す．
####2.	問題解決の方針

1. エクセルの関数を使い，音程と長さを指定すればPlay(音程,長さ)という命令がつくられるようにする．

2. コードを変更し，音程と長さだけ指定すればいいようにする．

####3.	プログラム

1. エクセルの関数を使い，音程と長さを指定すればPlay(音程,長さ)という命令がつくられるようにする．

    =CONCATENATE(A2,B2,C2,D2,E2)
を用いる．このようにすれば，以下のテーブルをエクセル上で作ることができる．

| A1 	| B1 	| C1 	| D1 	| E1  |=CONCATENATE(A1,B1,C1,D1,E1) 	|
|----	|----	|----	|----	|-----|-------------------------	    |
|play(|E    |,    |B8   |);   |play(E,B8);|
|play(|0    |,    |B8   |);   |play(0,B8);|
|play(|0    |,    |B8   |);   |play(0,B8);|
|play(|E    |,    |B8   |);   |play(E,B8);|
|play(|F    |,    |B8   |);   |play(F,B8);|

2. コードを変更し，音程と長さだけ指定すればいいようにする．
（以下のようにplay()とloop()だけに変更を加えた．）

```c
void play (int tonestack[], int lengthstack[]){
        int stacklength = sizeof(a) / sizeof(int);
        for(int i = 0; i<stacklength; i++){
          int length = lengthstack[i];
          int tone = tonestack[i];
          unsigned long tone_end_time;
          tone_end_time = millis() + length;
          while (millis() < tone_end_time) {
                  sound(tone);
          }
        }
}
```

```c
void loop (){
int tonestack[10]={C,C,C,C,D,D,D,B,C,A};
int lengthstack[10]={B8,B8,B8,B32,B8,B8,B8,B16,B16,B8};
play(tonestack,lengthstack);
}
```



