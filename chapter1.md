# Chapter1　　『Javaプログラミング基礎』

## 1．基礎知識

### 1. IDE

**《 IDE(統合開発環境) 》** は、様々ある。

- JDKが同梱されているもの
- 事前に用意されたJDKを使用するもの

また、 IDE セットアップ後に JDK  をインストールし、使用する設定も可能

<br>

### 2. JDK

**《 JDK 》** は、様々なベンダから有償・無償問わず提供されている。

&emsp; JDK はすべてのOSにバンドル(セットで提供)されているわけではない。
&emsp;&emsp; -> Java開発者が必要に応じて JDK をセットアップ

<br>

### 3. JRE

**《 JRE 》** は、Java11から単体配布されていない。

&emsp;開発環境の構築では、JDKのみのインストールでOK。( JREのインストールは不要 )
&emsp;Javaプログラムの実行は、JREがあれば可能。
&emsp;また、単体配布がない代わりに、カスタマイズしたものをアプリに同梱することが推奨されている。

<br><br><br><br>

## 2. コンパイルと実行

### 1. コンパイル

&emsp; コンパイルを行うことで、ソースファイル内のクラスのクラスファイルが出来上がる。

<br>

**【構文】&emsp; 通常のコンパイル**

&emsp;javac␣ソースファイル名.java

【例】&emsp; Sample.javaをコンパイルする場合

```sh
    javac Sample.java
```

***

<br><br>

**【構文】&emsp; パッケージ化されたソースコードのコンパイル**

&emsp;javac␣ディレクトリ名¥ソースファイル名.java

【例】&emsp; comディレクトリ内のSample.javaをコンパイルする場合

```sh
    javac com¥Sample.java
```

***

<br><br>

**【構文】&emsp; パッケージに対応したディレクトリ階層を作成をしながらのコンパイル**

&emsp;javac␣-d␣パッケージの一番上のディレクトリを置く場所␣ソースファイル名.java

【例】&emsp; 現在いる場所(カレントディレクトリ)にパッケージに沿ったディレクトリ階層を作成し、Sample.javaをコンパイルする場合
&emsp;&emsp;&emsp; (カレントディレクトリは「.」で表す)

```sh
    javac -d . Sample.java
```

***

<br><br><br><br>

### 2. 実行

<br>

**【構文】&emsp; 通常の実行**

&emsp;java␣クラスファイル名

【例】&emsp; Sample.classを実行する場合
&emsp;&emsp;&emsp; (「.class」は付けない)

```sh
    java Sample
```

***

<br><br>

**【構文】&emsp; コンパイルを省略した通常の実行**

&emsp;java␣ソースファイル名.java

【例】&emsp; Sample.javaを実行する場合

```sh
    java Sample.java
```

> [!IMPORTANT]
> この方法を使った場合、一番上のクラスの中に main()メソッドを探そうとする。
> そのため、Main()が含まれるクラスよりも上に、別のクラスがあった場合、エラーとなる。

【例】&emsp; Mainクラスよりも前にSampleクラスがある場合

```Java
1.  class Sample { }
2.  class Main {
3.      public static void main(string[] args) {
4.          ~~~記述~~~
5.      }
6.  }
```

> [!IMPORTANT]
> また、同ディレクトリ内に、同名のクラスファイルがあった場合も、エラーとなる。

【例】&emsp; 同ディレクトリ内に、同名のクラスファイルがあった場合

```sh
プロンプト > java Main.java
エラー：アプリケーション・クラス・パスにクラスが見つかりました： Main
```

***

<br><br>

**【構文】&emsp; 別ディレクトリのクラスファイルの実行**

&emsp;java␣-classpath␣ディレクトリ名␣クラスファイル名
&emsp;java␣-cp␣ディレクトリ名␣クラスファイル名

【例】&emsp; sampleディレクトリのSample.classを実行する場合

```sh
    java -classpath sample Sample

    java -cp sample Sample
```

***

<br><br><br><br>

### 3. パッケージ

<br>

**【パッケージの目的】**

- 名前空間を提供し、名前の衝突を避ける
- アクセス修飾子と組み合わせてアクセス制御機能を提供する
- クラスの分類を可能にする

***

<br>

**【構文】&emsp; パッケージ化**

&emsp;package␣パッケージ名

【例】&emsp; パッケージ名：com.se.sample の場合

```java
1.  package com.se.sample;
2.
3.  class hoge{ }   //com.se.sample.hoge として扱われる
```

***

<br>

> [!Warning]
> **無名パッケージへのアクセス**
> 無名パッケージに属するクラスは、同じ無名パッケージに属するクラスからしかアクセスできない。

***

<br><br><br><br>

### 4. インポート

<br>

**【構文】&emsp; インポート文**

&emsp;import␣パッケージ名.クラス名

【例】&emsp; com.se.sampleパッケージに属する Do クラスをインポートする場合

```java
import com.se.sample.Do;    //OK 構文通り
import com.se.sample.*;     //OK クラス名を「*」にすることで、
                            // パッケージに属するすべてのクラスを利用できる

import com.*;               //NG パッケージ名に「*」は使用できない
```

***

<br><br>

**【構文】&emsp; 利用クラスを完全名で指定**

&emsp; パッケージ名.クラス名 修飾名 = new  パッケージ名.クラス名();

【例】&emsp; com.se.sampleパッケージに属する Do クラスを利用する場合

```java
1. com.se.sample.Do do = new com.se.sample.Do();
```

***

<br><br>

> [!IMPORTANT]
> Import宣言をしなくても、自動的にImportされるもの
>
> - java.langパッケージに属するクラス
> - 同じパッケージに属するクラス

***

<br><br><br><br>

### 5. ソースファイル

<br>

> [!IMPORTANT]
> 記述順は package -> import -> class

【例】

```java
1.  package com.se;
2.  import com.se.sample.*;
3.  public class Main { ~~~記述~~~ }
```

***

<br><br>

> [!Warning]
> 一つのソースファイルにpublicなクラスは一つのみ

```java
// Test.java
class Foo { }
class Bar { }
// OK
```

```java
// Foo.java
public class Foo { }
public class Bar { }
// NG 一つのソースファイルに複数のPublicクラスが存在してはならない
```

```java
// Foo.java
public class Foo { }
class Bar { }
// OK
```

```java
// Bar.java
public class Foo { }
class Bar { }
// NG publicクラス名はソースファイル名と同じでなくてはならない
```

***

<br><br><br><br>

### 5. エントリポイント（ main()メソッド ）

<br>

**【エントリポイントの定義】**

- 公開されていること（ public ）
- インスタンスを生成しなくても実行できること（ static ）
- 戻り値を戻さないこと（ void ）
- メソッド名は「main」であること
- 引数はString型配列を１つ受け取ること

```java
public static void main(String[] args) {

}

```

&emsp; ※ 引数名「args」は自由

***

<br><br>

> [!Tip]
> **引数には可変長配列も設定できる**

```java
public static void main(String... args) {

}
```

&emsp; 可変長配列の引数はコンパイル時に、配列型に変換されるため。

***

<br><br><br><br>

### 6. 起動パラメータ

<br>

**【構文】　通常の起動パラメータ**

&emsp; > java␣クラスファイル名␣〇〇␣△△

【例】起動パラメータとして 「 a 」 , 「 b 」 , 「 c 」 と送る場合

```sh
> java Main a b c
```

&emsp; この場合、 「 a 」 , 「 b 」 , 「 c 」 が１文字ずつString型として送られる。

***

<br><br>

**【構文】スペースを含む起動パラメータ**

&emsp; > java␣クラスファイル名␣"〇〇␣△△"

【例】起動パラメータとして 「 Hello World 」 と送る場合

```sh
> java Main "Hello World"
```

&emsp;ダブルクォーテーションで囲んだ場合は、スペースで区切られない。

***

<br><br>

**【構文】ダブルクォーテーションを含む起動パラメータ**

&emsp; > java␣クラスファイル名␣¥"〇〇␣△△"¥

【例】起動パラメータとして 「 "Hello 」 , 「 World" 」 と送る場合

```sh
> java Main ¥"Hello World"¥
```

&emsp;  「 ¥" 」 でダブルクォーテーションを文字として渡すことができる。

***

<br><br>

> [!Warning]
> **" の後にスペースが開いていない場合**
> <br>
> 【例】 「 abc 」 という文字列が送られる
>
> ```sh
> > java main "a"bc
> ```
>
> &emsp; この場合、 「 " 」 は文字として扱われず、区切りとしても扱われない。

***
