# Chapter3　　『演算子・分岐』

<br>

## 1．演算子

### 1. 算術演算子

<br>

&emsp; 型の変化に注意する。

```java
1.  public class Main {
2.      public static void main(String[] args) {
3.          int     n1 = 10 / 3;    // 3            （整数同士の計算では、答えも整数になる）
4.          float   n2 = 10 / 3.0;  // 3.33・・・   （整数と小数点数の計算では、答えは小数点数になる）
5.          float   n4 = 10 / 3;    // 3.0         （答えは整数だが、代入先の方がfloatなため、小数点数表記になる）
6.      }
7.  }
```

***

<br><br>

### 2. ＋演算子を用いた文字列連結

<br>

&emsp; ＋演算子の計算は左から行われる。（）がある場合は、そこが優先される。

```java
1.  public class Main {
2.      public static void main(String[] args) {
3.          System.out.println("Hello" + 10 + 20);          // Hello1020
4.          System.out.println("Hello" + (10 + 20));        // Hello30
5.          System.out.println("Hello" + (10 + 20) + 30);   // Hello3030
6.          System.out.println(10 + 20 + "Hello");          // 30Hello
7.          System.out.println(10 + 20 + "Hello" + 30);     // 30Hello30
8.      }
9.  }
```

***

<br><br>

### 3. インクリメント・デクリメント

<br>

|名称| a の初期値|式|実行後の a の値|実行後の b の値|
|--|--|--|--|--|
|前置インクリメント|10|b = ++a;|11|11|
|後置インクリメント|10|b = a++;|11|10|
|前置デクリメント|10|b = --a;|9|9|
|後置デクリメント|10|b = a--;|9|10|

***

<br><br>

### 4. 論理演算子

<br>

|演算子 |記述例|説明|
|--     |--|--|
|&      |a & b      | a と b が両方 true のとき、 true <br> a が false でも、 b は評価される。|
|&&     |a && b     | a と b が両方 true のとき、 true <br> a が false なら b は評価されない。 <br> a が true なら b も評価される。|
|｜     |a ｜ b     | a か b が true のとき true <br> a が true でも、 b は評価される。|
|｜｜   |a ｜｜ b   | a か b が true のとき true <br> a が true なら、 b は評価されない。 <br> a が false なら b も評価される。|
|^      |a ^ b      | a と b の値が異なるとき、 true|
|!      | !a        | a の値が false のとき、 true|

***

<br><br><br><br>

## 2. 文字列の扱い

### 1. Stringクラスのメソッド

<br>

**【例】文字列「abcdefa」の場合**

|メソッド|説明|変数が指す文字列|結果|
|--|--|--|--|
|charAt(2)          | 引数番目の添え字の文字を返す | 0 1 2 3 4 5 6 <br> a b <span style="color: red; ">c</span> d e f a | c |
|equals("abcdefa")  | 引数の文字列と一致比較し、booleanで返す | a b  c d e f a | true |
|intern()           | 同じ文字列を文字列プールから返す | a b c d e f a | abcdefa |
|indexOf('c')       | 引数の文字が最初に出現する場所の添え字を返す | 0 1 2 3 4 5 6 <br> a b <span style="color: red; ">c</span> d e f a | 2 |
|length()           | 文字数を返す | a b c d e f a | 7 |
|replace('a','z')   | 第１引数の文字を、第２引数の文字に変え、結果の文字列を返す | <span style="color: red;">a</span> b c d e f <span style="color: red;">a</span> | zbcdefz |
|subString(2)       | 引数番目の添え字からの文字列を返す | 0 1 2 3 4 5 6 <br> a b <span style="color: red;">c d e f a</span> | cdefa |

***

<br><br>

### 2. StringBuilderクラスのメソッド

<br>

**【例】文字列「Ab␣Cdefge」の場合**

|メソッド|説明|変数が指す文字列|結果|
|--|--|--|--|
| append("XYZ")         | 引数で指定された文字列を現在の文字列に追加 | A b ␣ C d e f g e | Ab␣CdefgeXYZ |
| insert(2,"ZZ")        | 引数で指定された文字列を、引数番目の添え字の前に挿入 | 0 1 &nbsp;2 &nbsp;3 4 5 6 7 8 <br> A b <span style="color: red;">␣</span> C d e f g e | AbZZ␣Cdefge |
| delete(0,5)           | 第１引数から第２引数 - 1番目の添え字までの文字列を削除 | 0 1 &nbsp;2 &nbsp;3 4 5 6 7 8 <br> <span style="color: red;">A b ␣ C d</span> e f g e | efge |
| replace(3,9,"YYY")    | 第１引数から第２引数 - 1番目の添え字までの文字列を第３引数の文字列に置換 | 0 1 &nbsp;2 &nbsp;3 4 5 6 7 8 <br> A b ␣ <span style="color: red;">C d e f g e</span> | Ab␣YYY |
| substring(5)          | 引数番目の添え字から最後までの文字列を返す | 0 1 &nbsp;2 &nbsp;3 4 5 6 7 8 <br> A b ␣ C d <span style="color: red;">e f g e</span> | efge |

***

<br><br><br><br>

## 3. データの比較

### 1. 基本データ型の比較

<br>

```java
1.  public class Main {
2.      public static void main(String[] args) {
3.          int     n1  = 10;
4.          int     n2  = 1_0;
5.          long    n3  = 10L;
6.          byte    n4  = 10;
7.          char    n5  = 'a';
8.          float   n6  = 10.0f;
9.          double  n7  = 10.0;
10.         boolean n8  = true;
11.
12.         System.out.println(n1 == n2);   // true
13.         System.out.println(n1 == n3);   // true
14.         System.out.println(n1 == n4);   // true
15.         System.out.println(n5 == 'a');  // true
16.         System.out.println(n6 == n7);   // true
17.         System.out.println(n8 == true); // true
18.     }
19. }
```

&emsp; ※型が違っていても、値が一致していれば 「 true 」が返される。

***

<br><br>

### 2. 参照型の比較

<br>

```java
1.  public class Main {
2.      public static void main(String[] args) {
3.          int[] a1 = {10};
4.          int[] a2 = {10};
5.          System.out.println(a1 == a2);   // false
6.
7.          int[] a3 = {10};
8.          int[] a4 = a3;
9.          System.out.println(a3 == a4);   // true
10.     }
11. }
```

&emsp; ※値が一致していても、参照先が違っていれば 「 false 」 が返される。

***

<br><br>

### 3. 文字列の比較

<br>

**【例】 Stringクラスのequals()メソッドを使った文字列比較**

```java
1.  public class Main {
2.      public static void main(String[] args) {
3.          String s1 = "tanaka";
4.          String s2 = "tanaka";
5.          System.out.println(s1.equals(s2));  // true
6.
7.          String s1 = "TANAKA";
8.          System.out.println(s1.equals(s3));  // false
9.      }
10. }
```

&emsp; equals()メソッドは文字列が同じ場合に 「 true 」 を返す。
&emsp; ただし、小文字と大文字は区別される。

***

<br>

**【例】 == 演算子を使った文字列比較**

```java
1.  public class Main {
2.      public static void main(String[] args) {
3.          String s1 = "Hello";
4.          String s2 = new String("Hello");
5.          String s3 = "Hello";
6.          String s4 = s2.intern();
7.          System.out.println(s1 == s2);   // false
8.          System.out.println(s1 == s3);   // true
9.          System.out.println(s1 == s4);   // true
10.         System.out.println(s2 == s4);   // false
11.     }
12. }
```

&emsp; newを使わずに文字列を代入した場合、プール（領域）上に同じ文字列がすでにある場合は、それを参照する。
&emsp; ない場合は、プール上に新しく生成する。

&emsp; new を使用して文字列を作成・代入した場合は、個別に文字列が作られる。

***

<br>

> [!Warning]
> **StringとStringBilderの違い**
>
> 【例１】 ＋ 演算子を使った文字列連結
>
> ```java
> String s1 = "X";
> String s2 = s1 + "Y";             //別の「 XY 」という文字列が生成される
> System.out.println(s1 == s2);     // false
> ```
>
> 【例２】 concat ( ) メソッドを使った文字列連結
>
> ```java
> String s3 = "X";
> String s4 = s3.concat("Y");       //別の「 XY 」という文字列が生成される
> System.out.println(s3 == s4);     // false
> ```
>
> 【例３】StringBuilderクラスの文字列連結
>
> ```java
> StringBuilder s5 = new StringBuilder("X");
> StringBuilder s6 = s5.append("Y");    //既存の文字列が書き換わる
> System.out.println(s5 == s6);         // true
> ```

***

<br><br>

### 4. null の比較

<br>

```java
1.  public class Main {
2.      public static void main(String[] args) {
3.          String s1 = null;
4.          String s2 = "";
5.          int[] array1 = null;
6.          int[] array2 = new int[1];
7.          System.out.println(s1 == null);   // true
8.          System.out.println(s2 == null);   // false
9.          System.out.println(array1 == null);   // false
10.         System.out.println(array2 == null);   // true
11.     }
12. }
```

***

<br><br><br><br>

## 4. 基本データ型の型変換

### 1. 型変換ルール

<br>

【暗黙型変換】
`byte` -> `short` -> `int` -> `long` -> `float` -> `double`
&emsp;&emsp;&emsp;&emsp;&emsp;`char` ->

【キャストによる型変換】
`double` -> `float` -> `long` -> `int` -> `short` -> `byte`
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; -> `char`

***

<br>

> [!Important]
>
> **算術演算子による計算を行った場合の型変化**
>
> |一方の型|もう一方の型|結果の型|
> |--|--|--|
> | double | なんでも | double |
> | float | double以外 | float |
> | long | float,double以外 | long |
> | long,float,double以外 | long,float,double以外 | int |
>

***

<br><br>

### 2. ラッパークラス

&emsp; 基本データ型を参照型として扱う専用のクラス

|基本データ型|対応するラッパークラス|
|--|--|
| boolean | Boolean |
| byte | Byte |
| char | Character |
| short | Short |
| int | Integer |
| long | Long |
| float | Float |
| double | Double |

***

<br><br>

### 3. BoxingとUnboxing

**Boxsing**
&emsp; &emsp; 基本データ型からラッパークラスへの自動変換
**Unboxing**
&emsp; &emsp; ラッパークラスから基本データ型への自動変換

<br>

【例】 int 型 と Integer 型

```java
1.  public class Main {
2.      public static void main(String[] args) {
3.          int i1 = 100;
4.          Integer obj = i1;   // Boxing
5.          int i2 = obj;       // Unboxing
6.          method(i2);         // int型でメソッドの引数に渡す
7.      }
8.      static void method(Integer obj) {   // Integer型で受け取る
9.          int i = obj + 100;              // 計算も可能
10.         System.out.println(i);          // ２００
11.     }
12. }
```

<br><br><br><br>

## 5. 分岐文

### 1. 条件演算子

<br>

**【構文】条件演算子を使った分岐文**

&emsp; 条件式 ? 式１ : 式２

**【例】if文と条件演算子の違い**

&emsp; **if文**

```java
int num = 10;
boolean bool = false;
if(num >= 10) {
    bool = true;
} else {
    bool = false;
}
```

&emsp; **条件演算子**

```java
int num = 10;
boolean bool = false;
bool = num >= 10 ? true : false;
```

***

<br><br>

### 2. switch文

**【構文】switch文**

&emsp; switch( 式 ) {
&emsp; case 定数１:
&emsp; &emsp; &emsp; 処理１;
&emsp; case 定数２:
&emsp; &emsp; &emsp; 処理２;
&emsp; &emsp; ・
&emsp; &emsp; ・
&emsp; &emsp; ・
&emsp; default :
&emsp; &emsp; &emsp; 処理文
&emsp; }

> [!Warning]
> **式に入るクラスは以下に限られる**
>
> - char（Character）
> - byte（Byte）
> - short（Short）
> - int（Integer）
> - enum
> - String
>
> <br>
>
> **また、式で変数を定義することはできない**
>
> ```java
> int num = 2;
> switch(int x = 2;){ }     // 無効（コンパイルエラー）
> switch(num + 1){ }        // 有効
> switch(num++){ }          // 有効
> ```
>
> <br>
>
> **case 文の値はすべて`定数`でなければならない。**
>
> ```java
> 1.    public class Main {
> 2.        public static void main(String[] args) {
> 3.            int a = 1;
> 4.            final int b = 2;
> 5.            switch(num) {
> 6.                case a:             // コンパイルエラー
> 7.                    System.out.println("1");
> 9.                case b:             // final で定数なので、OK
> 10.                   System.out.println("2");
> 11.           }
> 12.       }
> 13.   }
> ```
>
> <br>
>
> **switch文は一致した部分から順に処理をしていくが、Break文で、中断が可能**
>
> ```java
> 1.    public class Main {
> 2.        public static void main(String[] args) {
> 3.            int num = 2;
> 4.            switch(num) {
> 5.                case 1:             // num == 1 の場合の処理
> 6.                    System.out.println("1");
> 7.                    break;          // break で switch から抜ける
> 8.                case 2:             // num == 2 の場合の処理
> 9.                    System.out.println("2");
> 10.                   // break文がないので、そのまま default に進む
> 11.               default:            // 上記すべてに当てはまらなかった時の処理
> 12.                   System.out.println("default");
> 13.           }
> 14.       }
> 15.   }
> ```

***
