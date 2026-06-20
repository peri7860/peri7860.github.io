---
title: "Java基礎知識：Scannerクラス（Scanner Class）のまとめ"
date: 2026-06-18 15:09:00 +0900
categories: [JAVA‐入門]  
tags: [JAVA, Scannerクラス]
---

# Java基礎知識：Scannerクラス（Scanner Class）のまとめ

## 1. Scannerクラスとは？

**Scannerクラス**とは、キーボードやファイルなどからデータを読み取るためのクラスです。

Javaの学習では主にキーボード入力を行うために使用します。

Scannerは `System.in` から入力されたデータを読み取り、文字列・整数・小数・真偽値などの型へ変換して返します。

```java
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int num = sc.nextInt();

        System.out.println(num);
    }
}
```

この例では、キーボードから入力された整数を取得しています。

---

## 2. Scannerクラスが必要な理由

通常のプログラムでは固定された値だけを扱います。

```java
int age = 20;
```

しかし実際のアプリケーションでは、ユーザーから値を入力してもらう必要があります。

例えば、

* 名前入力
* 年齢入力
* 点数入力
* 検索キーワード入力
* 会員登録フォーム

などです。

Scannerクラスを使用することで、実行中にユーザーから入力を受け取ることができます。

---

## 3. Scannerクラスの基本構文

### Scannerオブジェクトの生成

```java
Scanner sc = new Scanner(System.in);
```

---

### Scanner

入力を処理するクラス名です。

```java
Scanner
```

---

### sc

Scannerオブジェクトを保存する変数名です。

```java
Scanner sc
```

変数名は自由に決めることができます。

---

### new

オブジェクトを生成するためのキーワードです。

```java
new Scanner(...)
```

---

### System.in

標準入力を表します。

通常はキーボード入力を意味します。

```java
System.in
```

---

## 4. Scannerクラスの仕組み

Scannerは内部的に `System.in` から入力されたデータを読み取ります。

例えば、

```java
int age = sc.nextInt();
```

の場合、

```text
キーボード入力
↓
System.in
↓
Scanner
↓
int型へ変換
↓
変数へ格納
```

という流れで処理されます。

Scannerは入力されたデータを適切な型へ変換して返してくれるため、開発者は複雑な変換処理を書く必要がありません。

---

## 5. 主な入力メソッド

| メソッド | 説明 |
| :--- | :--- |
| `next()` | 1単語取得 |
| `nextLine()` | 1行取得 |
| `nextInt()` | int型取得 |
| `nextLong()` | long型取得 |
| `nextDouble()` | double型取得 |
| `nextFloat()` | float型取得 |
| `nextBoolean()` | boolean型取得 |

---

### next()

空白・タブ・改行までの文字列を取得します。

```java
String name = sc.next();
```

入力：

```text
Tanaka Suzuki
```

結果：

```text
Tanaka
```

---

### nextLine()

改行までの文字列全体を取得します。

```java
String name = sc.nextLine();
```

入力：

```text
Tanaka Suzuki
```

結果：

```text
Tanaka Suzuki
```

---

### nextInt()

整数を取得します。

```java
int age = sc.nextInt();
```

入力：

```text
20
```

結果：

```java
age = 20;
```

---

### nextDouble()

小数を取得します。

```java
double height = sc.nextDouble();
```

入力：

```text
173.5
```

結果：

```java
height = 173.5;
```

---

### nextBoolean()

真偽値を取得します。

```java
boolean flag = sc.nextBoolean();
```

入力：

```text
true
```

結果：

```java
flag = true;
```

---

## 6. Scannerを利用した入力例

### 名前入力

```java
Scanner sc = new Scanner(System.in);

System.out.print("名前：");
String name = sc.next();

System.out.println(name);
```

---

### 年齢入力

```java
Scanner sc = new Scanner(System.in);

System.out.print("年齢：");
int age = sc.nextInt();

System.out.println(age);
```

---

### 複数入力

```java
Scanner sc = new Scanner(System.in);

String name = sc.next();
int age = sc.nextInt();

System.out.println(name);
System.out.println(age);
```

---

## 7. Scanner使用時の注意点

### nextInt() と nextLine() を連続して使う場合

Scannerを使用する際によく発生するミスのひとつです。

例えば次のコードを見てみましょう。

```java
Scanner sc = new Scanner(System.in);

System.out.print("年齢：");
int age = sc.nextInt();

System.out.print("名前：");
String name = sc.nextLine();

System.out.println(age);
System.out.println(name);
```

入力：

```text
年齢：20
名前：Tanaka
```

期待する結果：

```text
20
Tanaka
```

しかし実際には、

```text
20

```

のように、名前が取得できないことがあります。

---

### なぜ起こるのか？

`nextInt()` は整数だけを読み取り、Enterキーで入力された改行文字（`\n`）は読み取りません。

例えば、

```text
20↵
```

と入力した場合、

```text
20 → nextInt() が取得
↵ → 入力バッファに残る
```

という状態になります。

その後、

```java
String name = sc.nextLine();
```

が実行されると、

入力バッファに残っていた改行文字をそのまま読み取ってしまいます。

結果として、

```java
name = "";
```

となり、ユーザーが名前を入力する前に処理が終了してしまいます。

---

### 入力バッファとは？

入力バッファとは、キーボードから入力されたデータを一時的に保存しておく領域です。

例えば、

```text
20↵
```

を入力すると、

入力バッファには

```text
20\n
```

が保存されます。

`nextInt()` は

```text
20
```

だけを取得し、

```text
\n
```

は残したまま終了します。

そのため次の `nextLine()` が残っていた改行文字を読み取ってしまいます。

---

### 解決方法

`nextInt()` の後に `nextLine()` を一度実行して改行文字を読み捨てます。

```java
Scanner sc = new Scanner(System.in);

System.out.print("年齢：");
int age = sc.nextInt();

sc.nextLine();

System.out.print("名前：");
String name = sc.nextLine();

System.out.println(age);
System.out.println(name);
```

---

### 入力の流れ

入力：

```text
20↵
```

#### ① nextInt()

```java
int age = sc.nextInt();
```

↓

```text
20 を取得
改行文字は残る
```

---

#### ② nextLine()

```java
sc.nextLine();
```

↓

```text
改行文字を読み捨てる
```

---

#### ③ 名前入力

```java
String name = sc.nextLine();
```

↓

```text
Tanaka
```

を正常に取得できるようになります。

---

### next() と nextLine() の違い

| メソッド | 取得範囲 |
| :--- | :--- |
| `next()` | 空白まで |
| `nextLine()` | 改行まで |

入力：

```text
東京 太郎
```

#### next()

```java
String name = sc.next();
```

結果：

```text
東京
```

---

#### nextLine()

```java
String name = sc.nextLine();
```

結果：

```text
東京 太郎
```

---

## 8. 面接対策用：回答例

| 質問（Q） | 回答（A） |
| :--- | :--- |
| **Scannerクラスとは何ですか？** | キーボードやファイルなどから入力を受け取るためのクラスです。 |
| **System.inとは何ですか？** | 標準入力を表し、通常はキーボード入力を意味します。 |
| **nextInt()とは何ですか？** | 入力された整数を取得するメソッドです。 |
| **nextLine()とは何ですか？** | 改行までの文字列を取得するメソッドです。 |
| **next()とnextLine()の違いは何ですか？** | next()は空白まで、nextLine()は改行まで取得します。 |
| **Scannerを使う理由は何ですか？** | ユーザーからデータを入力してもらうためです。 |
| **Scannerはどのパッケージにありますか？** | java.utilパッケージです。 |

---

## 9. 面接でよく深掘りされる追加質問（実務知識）

### Q. ScannerとSystem.inの違いは何ですか？

**A.**

System.inは入力ストリームそのものです。

ScannerはSystem.inからデータを読み取り、必要な型へ変換して扱いやすくするためのクラスです。

```java
Scanner sc = new Scanner(System.in);
```

---

### Q. next()とnextLine()の違いは何ですか？

**A.**

* next() → 空白まで取得
* nextLine() → 改行まで取得

```text
Tanaka Suzuki
```

の場合、

```java
next()
```

は

```text
Tanaka
```

のみ取得します。

一方、

```java
nextLine()
```

は

```text
Tanaka Suzuki
```

全体を取得します。

---

### Q. なぜnextInt()の後にnextLine()で問題が起きるのですか？

**A.**

nextInt()が改行文字を入力バッファに残したまま終了するためです。

その結果、次のnextLine()がその改行文字を読み取り、空文字列を返してしまいます。

実務でも非常によく発生するScannerの代表的なトラブルです。

---

### Q. Scannerは使い終わったらclose()するべきですか？

**A.**

基本的にはclose()することが推奨されています。

```java
sc.close();
```

ただし学習用コードでは省略されることもあります。

---

## 10. 面接用まとめ

* Scanner：入力を受け取るクラス
* System.in：標準入力
* nextInt()：整数入力
* nextDouble()：小数入力
* next()：1単語取得
* nextLine()：1行取得
* 入力バッファ：入力データの一時保存領域
* close()：リソース解放

一言で言うと、

> **Scannerクラスは、キーボードなどから入力されたデータを読み取り、intやStringなどの型へ変換して利用するためのクラスです。また、nextInt()とnextLine()を連続して使用する際は、入力バッファに残る改行文字に注意する必要があります。**