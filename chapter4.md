# Chapter4　　『繰り返し・制御文』

<br>

## 1．For文

### 1. 省略形

<br>

&emsp; For文の各式は、省略することができます。

【例文】

```java
int i1 = 0;
for ( ; i1 < 5 ; i1++) { }          // 初期化式の省略
for ( int i2 = 0 ; ; i2++) { }      // 条件式の省略（無限ループ）
for ( int i3 = 0 ; i3 < 5 ; ) { }   // 変化式の省略
```

<br>

> [!Important]
>
> **for文の各式には、ルールがあります。**
>
> 1. 初期化式は文である必要がある
>
> ```java
> 1.    int i1 = 0;
> 2.    for(i1 ; i1 < 5 ; i1++) { }         // 無効（コンパイルエラー）
> 3.    for(i1 += 1 ; i1 < 5 ; i1++) { }    // 有効
> ```
>
> <br>
>
> 2. 初期化式には宣言でない式を２つ入れることができる
>
> ```java
> 1.    int i2 = 0, i3 = 0;
> 2.    for(i2++, i3++ ; i2 + i3 < 5 ; i2++) { }    // 有効
> ```
>
> <br>
>
> 3. また、初期化式の宣言は１つのみ
>
> ```java
> 1.    for(int i4 = 0, int i5 = 0 ; i4 + i5 < 5 ; i4++) { }    //無効（コンパイルエラー）
> 2.    for(int i6 = 0, i7 = 0 ; i6 + i7 < 5 ; i6++) { }        // 有効
> ```
>
> <br>
>
> 4. 変化式にも、カンマ区切りで２つの式を入れることができる
>
> ```java
> 1.    for(int i6 = 0, i7 = 0 ; i6 + i7 < 5 ; i6++, i7++) { }  // 有効
> ```
>
> <br>
>
> 5.何も記述いないことで、無限ループを作ることができる
>
> ```java
> 1.    for( ; ; ) { }  // 有効
> 2.    for() { }       // 無効（コンパイルエラー）
> ```

<br><br><br><br>

## 2. 繰り返し制御文

### 1. ラベル

<br>

&emsp; 繰り返し文に名前を付けることで、 break 文 continue 文の対象をネストの外側の繰り返し文にすることができる機能

<br>

**【構文】ラベルを使った繰り返し制御**

&emsp; ラベル名 :                               <br>
&emsp; for(初期化式 ; 条件式 ; 変化式) {        <br>
&emsp; &emsp; …                                 <br>
&emsp; &emsp; for(初期化式 ; 条件式 ; 変化式) { <br>
&emsp; &emsp; &emsp; …                          <br>
&emsp; &emsp; &emsp; break ラベル名 ;           <br>
&emsp; &emsp; }                                 <br>
&emsp; }                                        <br>

&emsp; 内側ではなく、直接、外側のfor文から抜け出せる

**【例】**
```java
1.  public class Main {
2.      public static void main(String[] args) {
3.          loop1 : 
4.          for(int x = 0; x < 3; x++) {
5.              for(int y = 0; y < 3; y++) {
6.                  System.out.println(" X = " + x + " y = " + y);
7.                  if(x == 1 && y == 1) {
8.                      System.out.println("break文の実行");
9.                      break loop1;
10.                 }
11.             }
12.         }
13.         System.out.println("----------------------------------------");
14.         loop2 :
15.         for(int x = 0; x < 3; x++) {
16.             for(int y = 0; y < 3; y++) {
17.                 System.out.println(" X = " + x + " y = " + y);
18.                 if(x == 1 && y == 1) {
19.                     System.out.println("continue文の実行");
20.                     continue loop2;
21.                 }
22.             }
23.         }
24.     }
25. }
```

**【結果】**

```sh
x = 0 y = 0 
x = 0 y = 1 
x = 0 y = 2 
x = 1 y = 0 
x = 1 y = 1 
break文の実行
----------------------------------------
x = 0 y = 0 
x = 0 y = 1 
x = 0 y = 2 
x = 1 y = 0 
x = 1 y = 1 
continue文の実行
x = 2 y = 0
x = 2 y = 1
x = 2 y = 2
```

***