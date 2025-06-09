# Chapter5　　『クラス定義とオブジェクトの生成』

<br>

## 1．クラス

### 1. 変数のスコープ

<br>

**二種類の変数**

| 名称 | 宣言の場所 | 初期化 | 有効範囲 |
| -- | -- | -- | -- |
| メンバ変数 | クラス直下 | 必要なし | クラス内 |
| ローカル変数 | ブロック（ if , for など）の中、引数など | 必須 | 宣言したブロック内 |

<br>

```java
1.  class Test {
2.      int x;  // メンバ変数
3.
4.      public static void main(String[] args) {
5.          boolean y = true;               // ローカル変数（main()メソッド内）
6.          if(y) {                         // 同じブロック内なので、アクセス可能
7.              String z = "Java World";    // ローカル変数（if文内）
8.          }
9.          System.out.println(z);          // ブロック外なので、アクセス不可（コンパイルエラー）
10.     }
11. }
```

<br><br>

> [!Warning]
>
> **同名のメンバ変数とローカル変数**
>
> ```java
> 1.    class Test {
> 2.        int x = 1;                  // メンバ変数 x 
> 3.
> 4.        public static void main(String[] args) {
> 5.            int x = 10;             // ローカル変数 x 
> 6.            int y = 20;             // ローカル変数 y
> 7.            Test test = new Test();
> 8.
> 9.            System.out.println(x);          // ローカル変数の x が呼ばれる
> 10.           System.out.println(y);          // ローカル変数の y が呼ばれる
> 11.           System.out.println(test.x);     // メンバ変数の x が呼ばれる
> 12.       }
> 13.   }
> ```

***

<br><br>

### 2. コンストラクタと定数

<br>

&emsp; **定数はコンストラクタの中で、初期化ができる**

```java
1.  public class Test {
2.      final int num;
3.      Test(int num) { this.name = name; }
4.  }
```

***

<br><br><br><br>

## 2. 可変長引数

<br>

**可変長引数のルール**

- データ型の後に 「 … 」 と記述する
- 渡された後は、配列として扱われる
- 他の型の引数と併用可能
&emsp; ただし、可変長引数は最後尾に記述

```java
    void method(String s, int... a) { } // OK
    void method(int... a, String s) { } // NG
```

- 可変長引数は一つしか使用できない

```java
    void method(String s, int... a) { }     // OK
    void method(String... s, int... a) { }  // NG
```

- 明確な定義の引数と可変長引数がある場合は、明確に引数を定義しているメソッドが優先される
&emsp; （例）method( 10, 20 );と呼び出されている場合

```java
    void method(int... a) { }
    void method(int a, int b) { }  // こちらが優先される
```

<br><br>

> [!Important]
> **オーバーロードの優先順位**
>
> > 完全一致 > 暗黙の型変換 > Boxing > 可変長引数
>
> ```java
> 
> ```

***

<br><br><br><br>

## 3. staticメンバ と staticメソッド

staticは、クラスの中で宣言しているものの、クラスとは別で保管されるものです。

### 1. **メンバの種類**

<br>

||メンバ変数|メンバメソッド|
|--|:--:|:--:|
|インスタンスメンバ|インスタンス変数|インスタンスメソッド|
|staticメンバ|static変数|staticメソッド|

> [!Warning]
> ※static はメンバ変数にしか付与できないので、書かれている場所に注意！

***

<br><br>

### 2. static変数・staticメソッドの呼び出し

<br>

**【構文】**
&emsp; クラス名 . static変数名
&emsp; クラス名 . staticメソッド名

**【例文】**

```java
/** class.java */
1.  class Test { 
2.      int num1 = 100;
3.      static int num2 - 200;
4.      void methodA() { }
5.      static void methodB() { }
6.  }

/** main.java */
1.  public class Main {
2.      public static void main(String[] args) {
3.          Test.num1;              // NG インスタンス変数は、インスタンス化しないと使用不可
4.          Test.num2;              // OK
5.          Test.methodA();         // NG インスタンスメソッドは、インスタンス化しないと使用不可
6.          Test.methodB();         // OK
7.          Test obj = new Test();  // インスタンス化
8.          obj.num1;               // OK
9.          obj.num2;               // OK
10.         obj.methodA();          // OK
11.         obj.methodB();          // OK
12.     }
13. }
```

***

<br><br>

### 3. クラス内でのアクセス

<br>

**ルール**

- クラス内のインスタンスメンバ同士・staticメンバ同士は直接アクセスできる
- クラス内のインスタンスメンバは、クラス内のstaticメンバに直接アクセスできる
- クラス内のstaticメンバは、クラス内のインスタンスメンバに直接アクセスできない。アクセスする場合は、インスタンス化してから、アクセスする

<br>

【例文】

```java
1.  public class {
2.      int instanceNum;            // インスタンス変数
3.      static int staticNum;       // static変数
4.      int methodA() { return instanceNum; }           // OK インスタンスメソッド -> インスタンス変数
5.      int methodB() { return staticNum; }             // OK インスタンスメソッド -> static変数
6.      static int methodC() { return instanceNum; }    // NG staticメソッド -> インスタンス変数
7.      static int methodD() { return staticNum; }      // OK staticメソッド -> static変数
8.      static int methodE() {                          // OK インスタンス化して、アクセス
9.          Test obj = new Test();
10.         return obj.instanceNum;
11.     }
12. }
```

***

<br><br>

### 4. nullに対するstaticメンバ呼び出し

【例文】

```java
1.  class Test {
2.      static String staticValue = "static";   // static変数
3.      String instanceValue = "instance";      // インスタンス変数
4.  }
5.
6.  class Main {
7.      public static void main(String[] args) {
8.          Test obj = null;
9.          System.out.println(obj.staticValue);    // OK static変数は別領域のため
10.         System.out.println(obj.instanceValue);  // NG NullPointerエラー
11.     }
12. }
```

***

<br><br>

### 5. staticイニシャライザ

<br>

&emsp; インスタンス化前やmain()メソッド実行前に実行する処理（メソッドのようなもの）

【構文】
&emsp; static { 処理; }

<br>

【例文】staticイニシャライザとコンストラクタ

```java
1.  class Test {
2.      static {
3.          System.out.println("Test : staticイニシャライザ");
4.      }
5.      Test() {
6.          System.out.println("Test : コンストラクタ");
7.      }
8.  }
9.
10. public class Main {
11.     static {
12.         System.out.println("main : staticイニシャライザ");
13.     }
14.     public static void main(String[] args) {
15.         System.out.println("main : main()メソッド");
16.         Test obj = new Test();
17.     }
18. }
```

【結果】

```sh
main : staticイニシャライザ
main : main()メソッド
Test : staticイニシャライザ
Test : コンストラクタ
```

***

<br><br><br><br>

## 4. 値コピー・参照コピー

&emsp; メソッドで引数を使った計算などを行うとき、引数の型によって、呼び出し側の引数の値の挙動が異なる場合がある。

| 型 | 引数の型（例） | 引数の値 | 処理 | メソッド定義側の結果 | メソッド呼び出し側の結果 |
|--|--|--|--|--|--|
| 基本データ型 | int | 10 | int += 10 | 20 | 10 |
| 参照型 | int [ ] | { 10 } | int [ 0 ] += 10 | 20 | 20 |

<br>

【例文】

```java
1.  class Test {
2.      void method1(int num) {
3.          num += 10;
4.          System.out.println("定義側：" + num);
5.      }
6.      void method2(int[] array) {
7.          num[0] += 10;
8.          System.out.println("定義側：" + array[0]);
9.      }
10. }
11. public Main {
12.     public static void main(String[] args) {
13.         int num = 10;
14.         int[] array = {10};
15.         Test obj = new Test();
16.         obj.method1(num);
17.         System.out.println("呼び出し側：" + num);
18.         obj.method2(array);
19.         System.out.println("呼び出し側：" + array[0]);
20.     }
21. }
```

```sh
定義側：20
呼び出し側：10
定義側：20
呼び出し側：20
```

***

<br><br><br><br>

## 5. ガベージコレクタ

&emsp; メモリの管理をしている機プログラム
&emsp; プログラムが使用しなくなったメモリ領域を検出・解放する

<br>

**ガベージコレクタによるメモリの解放**

&emsp; ガベージコレクタにメモリを解放させるには、オブジェクトの参照をなくす必要がある
&emsp; 方法は以下の２通り

1. **null を代入**
&emsp; null を代入することで、明示的に「オブジェクトを参照しない」ことを表す。

2. **参照変数を他のオブジェクトに割り当てる**
&emsp; 新しくオブジェクトを割り当てることで、基のオブジェクトの参照をなくす。

***
