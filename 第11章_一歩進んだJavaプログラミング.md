# 第11章　一歩進んだJavaプログラミング

## ストリーム

### コレクションとストリーム

- ストリーム：ストリームを使えば、より短く直感的にオブジェクトの集合を扱える
  - 終端操作：最後に行う処理
  - 中間操作：終端操作を行うまでの処理（何度でも可能、なくてもよい）

### ストリームの生成

ストリームは、インタフェースであるためnew演算子では生成できない。その代わりに、コレクションクラスが持つstreamメソッドを使用して取得する。

```java
List<String> list = Arrays.asList("January", "February", "March");
Stream<String> stream = list.stream();
```

Streamインタフェースのofメソッドを使っても作ることができる。

```java
Stream<String> stream = Stream.of("January", "February", "March");
```

### ストリームに対する終端操作

forEachとラムダ式を使って、ここのオブジェクトに対する処理を書ける

```java
List<String> list = Arrays.asList("January", "February", "March");
list.stream().forEach(s -> System.out.println(s));
```

countメソッドで、オブジェクトの数を取得できる

```java
long n = list.stream().count();
System.out.println(n);
```

### ストリームに対する中間操作

filterメソッド。条件を満たすオブジェクトの抽出

中間操作を行うメソッドはストリームオブジェクトを戻り値とするため、メソッドの呼び出しをドットで連結して記述できる

```java
long l = list.stream().
filter(s -> s.length() > 5).
count();
```

mapメソッド。別のオブジェクトにマッピング

```java
map(s -> "[" + s + "]")
```

sortedメソッド。並べ替え

```java
sorted((s0, s1) -> s0.length() - s1.length())
```

### ストリームからおbジェクトの配列やコレクションを生成する

```java
Stream<String> stream = Stream.of("A", "B", "C");

// Object型の配列
stream.toArray

// String型の配列
String[] strings = stream.toArray(size -> new String[size]);

// List型のコレクションオブジェクト
List<String> list = stream.collect(Collectors.toList());
```

## 知っておきたい機能

### スタティックインポート

スタティックインポート：クラス名を記述しなくても、クラス変数とクラスメソッドを直接使用できるようにすること

```java
import static java.lang.Math.PI;
import static java.lang.Math.abs;

public class StaticImportExample {
    public static void main(String[] args) {
        System.out.println("P1=" + PI);
        System.out.println("abs(-2)=" + abs(-2));
    }
}
```

### インタフェースのデフォルトメソッド

インタフェースにはデフォルトメソッドを記述できる。

```java
interface SayHello {
    default void hello() {
        System.out.println("Hello");
    }
}

class EnglishGreet implements SayHello {
}

class JapaneseGreet implements SayHello {
    public void hello() {
        System.out.println("こんにちは");
    }
}

public class DefaultMethodExample {
    public static void main(String[] args) {
        SayHello a = new EnglishGreet();
        SayHello b = new JapaneseGreet();
        a.hello();
        b.hello();
    }
}
```

### アノテーション

@Override：メソッドが、インタフェースやスーパークラス、あるいはサブクラスのメソッドをオーバライドしたものであることを示す

### System.out.printfメソッド

```java
int i = 99;
System.out.printf("iの値は%dです%n", i);
// %d と i が置き換えられる
```

%d：整数
%n：開業
%f：小数点を含む数値
%s：文字列

### enum宣言

```java
class Student {
    enum Gender { MAlE, FEMALE };
    String name;
    Gender gender;
}

Student s = new Student();
s.name = "山田太郎";
s.gender = Student.Gender.MALE;
```

### ==演算子とequalsメソッド

```java
class Point {
    int x;
    int y;
    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public boolean equals(Object p) {
        Point point = (Point)p;
        return (point.x == this.x && point.y == this.y);
    }
}

public class CompareExample2 {
    public static void main(String[] args) {
        Point p1 = new Point(2,3);
        Point p2 = new Point(2,3);
        Point p3 = p2;

        System.out.println(p1 == p2);
        System.out.println(p2 == p3);

        System.out.println(p1.equals(p2));
        System.out.println(p1.equals(p2));
    }
}
```

練習問題

11.1

```java
List<Point> list = Arrays.asList(new Point(7,7, new Point(9,3), new Point(3,1)));
list.stream().
    filter(p  -> p.x > 3).
    sorted((p0, p1) -> p0.y - p1.y).
    forEach(p -> p.printInfo());
    // forEach(p -> System.out.println(p));
```

11.2
1: x
2: o
3: o
4: x

11.3
1:

```java
class Student {
    enum Gender { MALE, FEMALE, UNKNOWN };
    String name = "匿名";
    Gender gender = Gender.UNKNOWN;
}

2:
public boolean equals(Object obj) {
    Student student = (Student)obj;
    return (s.name == this.name && s.gender == this.gender);
}
```