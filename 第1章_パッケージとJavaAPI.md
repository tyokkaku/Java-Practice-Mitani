# 第1章　パッケージとJava API

## パッケージの利用

パッケージの利用

Javaに用意された共通に必要とされる機能を持ったクラスを、クラスライブラリと呼ぶ。クラスライブラリのクラスやインタフェースは「パッケージ」と呼ばれる単位で管理されている。

完全限定名：パッケージ名とクラス名を(.)でつなげた表記方法によるクラス名

```java
import java.util.Random;

public class ImportExample {
    public static void main(String[] args) {
        Random rand = new Random();
        // 0〜1の間のランダムな値を出力する
        System.out.print(rand.nextDouble());
    }
}
```

## 基本的なクラス

String型は、基本型ではなく、java.langパッケージに含まれる``Stringクラス``。したがって、newキワードを使って生成できる。

``String message = new String("こんにちは")``

```java
String s1 = new String("こんにちは");
String s2 = new String("こんにちは");
System.out.println(s1 == s2);

// false：インタンス内容は同じだが、インスタンスが参照しているのは別々のところである

String s1 = "こんにちは";
String s2 = "こんにちは";
System.out.println(s1 == s2);

// true：同じ文字列は1つのインスタンスとして済まされる
```

## パッケージの作成

パッケージの作成：``package パッケージ名``

package宣言が省略されたクラスは、デフォルトパッケージと呼ばれる名前のないパッケージに自動的に含まれる。

```java
// mypackage/MyClass

package mypackage;

public class MyClass {
    public void printMessage() {
        System.out.println("mypackageパッケージのMyClassのprintMessageメソッドです");
    }
}

// packageのクラスを使う

import mypackage.MyClass;

public class ImportExample {
    public static void main(String[] args) {
        Random rand = new Random();
        // 0〜1の間のランダムな値を出力する
        System.out.print(rand.nextDouble());
        MyClass a = new MyClass();
        a.printMessage();
    }
}
```

- srcファイル： プログラムコード
- binファイル： コンパイルしてできたバイトコード

パッケージの階層構造は、フォルダ構成と一致する

## クラスのアクセス制御

- クラスとインタフェースのアクセス修飾子(つけられるのはpublicのみ)
  - public：どのパッケージからでもアクセスできる
  - なし：同じパッケージのみ

アクセス制限は、フィールドやメソッドよりクラスが優先される

### 複数のクラス宣言を持つプログラムコード

- 原則
  - public修飾子のついたクラス名はファイル名と同じである必要がある
  - public修飾子をつけることができるクラスは1つのみ