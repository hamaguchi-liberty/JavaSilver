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

## 3. static

<br>

***

<br><br><br><br>

## 4. 値コピー・参照コピー

<br>

***

<br><br><br><br>

## 5. ガベージコレクタ

<br>

***
