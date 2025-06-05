# Chapter2　　『変数・配列』

<br>

## 1．リテラル

### 1. 整数リテラルの区別

<br>

&emsp; 整数リテラルを扱う際は、何進法か？に気を付ける

```java
1.  public class Main {
2.      public static void main(String[] args) {
3.          int i01 = 255;          // 10進数：255
4.          int i02 = 25f;          // 10進数：コンパイルエラー
5.          int i03 = 0b11111111;   // 2進数：255
6.          int i04 = 0b2222;       // 2進数：コンパイルエラー
7.          int i05 = 0377;         // 8進数：255
8.          int i06 = 0877;         // 8進数：コンパイルエラー
9.          int i07 = 0xff;         // 16進数：255
10.         int i08 = 0xgg;         // 16進数：コンパイルエラー
11.     }
12. }
```

***

<br><br>

### 2.　＿（アンダースコア）が入った数値リテラル

<br>

&emsp; 数値リテラルを扱う際は、数字の途中に「 _ 」（アンダースコア）を使用できる。

```java
1.  public class Main {
2.      public static void main(String[] args) {
3.          float   x01 = 3_.1415F;         //NG：小数点の前は使用不可
4.          float   x02 = 3._1415F;         //NG：小数点の後も使用不可
5.          long    x03 = 999_99_9999_L;    //NG：サフィックス(Lなど)の前では使用不可

6.          int     x04 = _52;              //NG：リテラルの先頭は使用不可
7.          int     x06 = 52_;              //NG：リテラルの末尾は使用不可
8.          int     x05 = 5_2;              //OK：リテラルの途中は使用可能
9.          int     x07 = 5_______2;        //OK：＿に回数制限はないので使用可能

10.         int     x08 = 0_x52;            //NG：16進数を表す 0x の途中は使用不可
11.         int     x09 = 0x_52;            //NG：16進数を表す 0x の直後も使用不可
12.         int     x10 = 0x5_2;            //OK：リテラルの途中は使用可能
13.         int     x11 = 0_52;             //OK：8進数を表す 0 の直後は使用可能
14.     }
15. }
```

***

<br><br>

### 3. 文字リテラル

&emsp; 文字リテラルは、「 ' 」（シングルクォーテーション）で囲まれた、１文字で、char型を使います

```java
1.  public class Main {
2.      public static void main(String[] args) {
3.          char c01 = 'A';     // OK 
4.          char c02 = 'あ';    // OK
5.          char c03 = '人';    // OK
6.          char c04 = '1';     // OK
7.          char c05 = 89;      // OK Unicodeにおいて89に対応する文字が格納される
8.          char c06 = "a";     // NG 「 " 」で文字列と判定されるため、コンパイルエラー
9.          char c07 = 'abc';   // NG 「 ' 」だが、中身が文字列なため、コンパイルエラー
10.         char c08 = null;    // NG　char型はプリミティブ型のため、参照なしの「null」を持てない
11.     }
12.}
```

***

<br><br><br><br>

## 2. 変数

### 1. 識別子の命名

<br>

**【命名規則】**

- 識別子の１文字目は、英字 ( a-z , A-Z )、ドル記号 ( $ )、アンダースコア ( _ ) のみ
- 識別子の２文字目以降は、数字も使用可能
- 予約語は使用不可
- 大文字、小文字は区別される
- 文字数制限はない
- null、true、false は予約語ではないが、リテラルとして扱われるので、使用不可

***

<br><br>

### 2. ローカル変数の型推論

&emsp;　ローカル変数を宣言するときは、特定のデータ型以外に 「 var 」 を使用することができる

|【利用できる箇所】|
|:--|
|・　ローカル変数の初期化時|
|・　拡張for文内のインデックス|
|・　通常for文内のローカル変数|
|・　try-with-resources文内のローカル変数|

|【利用できない箇所】|
|:--|
|・　メソッドの引数|
|・　コンストラクタの引数|
|・　メソッドの戻り値|
|・　フィールド（メンバ変数）|
|・　catchブロック|

<br>

**&emsp; 【例】**

```java
1.  public class Main {
2.      var a = 100;            // NG メンバ変数（インスタンス変数）のため、 var 使用不可
3.      static var b = 100;     // NG メンバ変数（static変数）のため、 var 使用不可
4.
5.      public static void main(String[] args) {
6.          var c = "Hello";    // OK "Hello"より、String型に推論
7.          var d = 100;        // OK 100 より、int型に推論
8.          var e;              // NG 初期値なしは使用不可
9.          var f = null;       // NG nullにより、型推論不可
10.         final var g = 100;  // OK 定数でも使用可能
11.         var final h = 100;  // NG final は var の前に記述する必要がある
12.     }
13. }
```

***

<br><br><br><br>

## 3. 配列

### 1. 配列の宣言と初期化

<br>

```java
1.  public class Main {
2.      public static void main(String[] args) {
3.          int[][] a1 = new int[2][];          // OK 1次元目のみの容量確保は可能
4.          int[][] a2 = new int[][2];          // NG 2次元目のみの容量確保は不可
5.          int[]   a3 = new int[2]{ };         // NG 要素数の指定と初期化は同時にできない
6.          int[]   a4 = new int[2]{10, 20};    // NG 上記と同様
7.          int[]   a5 = new int[]{10, 20};     // OK 要素数の指定がなく初期化のみは可能
8.          int[]   a6 = { }                    // OK 要素数0の配列が出来上がる
9.          int[][] a7 = { }                    // OK 上記と同様
10.         int[][] a8 = new int[][]{ };        // OK 上記と同様
11.         var     a9 = {10, 20};              // NG varを使用した配列の初期化は、明示的な型の宣言が必要
12.         var     a10 = new int[]{10, 20};    // OK 明示的に方を宣言しているため可能
```

***

<br><br>

> [!Warning]
> 配列の中の「 null 」は注意が必要！！
>
> ```java
> String[] str = {"A", null, "C"};
> str.length;           // 3（ null も一つの要素に含まれる）
> str[1].length();      // 中身がない（ null ）ため コンパイルエラー
> ```

***
