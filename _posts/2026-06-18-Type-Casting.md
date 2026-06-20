---
title: "Java基礎知識：型変換（Type Casting）のまとめ"
date: 2026-06-18 11:12:00 +0900
categories: [JAVA‐入門]  
tags: [JAVA, 型変換, 変数]
---

# Java基礎知識：型変換（Type Casting）のまとめ

## 1. 型変換とは？

**型変換（Type Casting）**とは、あるデータ型の値を別のデータ型へ変換することです。

Javaでは異なるデータ型同士の代入や演算を行う際に型変換が発生します。

```java
int i = 100;
double d = i;
```

この場合、

```java
int → double
```

への型変換が行われています。

---

## 2. 型変換の種類

Javaの型変換は大きく2種類に分類されます。

* 自動型変換（暗黙的型変換）
* 明示的型変換（キャスト）

---

## 3. 自動型変換（暗黙的型変換）

小さい型から大きい型へ変換する場合は、自動的に型変換が行われます。

```java
int i = 100;
double d = i;
```

結果：

```text
i = 100
d = 100.0
```

---

### 型変換の順序

以下の順番で自動型変換が可能です。

```text
byte
  ↓
short
  ↓
int
  ↓
long
  ↓
float
  ↓
double
```

サイズの大きい型へ代入する場合は自動で変換されます。

---

### 自動型変換の例

```java
int num = 10;
long value = num;
```

```java
long value = 100;
double d = value;
```

どちらも自動型変換が行われます。

---

## 4. 明示的型変換（キャスト）

大きい型から小さい型へ変換する場合は、自分で型を指定する必要があります。

```java
double d = 3.99;
int num = (int)d;
```

結果：

```text
3
```

---

### キャストの基本構文

```java
(変換先の型)値
```

例：

```java
int num = (int)3.99;
```

---

### データ損失に注意

```java
double d = 3.99;
int num = (int)d;
```

結果：

```text
3
```

小数部分は切り捨てられます。

> キャストは四捨五入ではなく、小数部分を切り捨てます。

---

## 5. char型とint型の変換

Javaの文字は内部的にUnicodeコードで管理されています。

そのため、

```java
char → int
```

への変換が可能です。

---

### char → int

```java
char c = 'A';
int num = c;
```

結果：

```text
65
```

---

```java
char c = 'a';
int num = c;
```

結果：

```text
97
```

---

### int → char

```java
int num = 66;
char c = (char)num;
```

結果：

```text
B
```

---

### 具体例

```java
char c1 = 'A';
int num = c1;

System.out.println(num);
```

結果：

```text
65
```

---

## 6. Stringと数値の変換

実務でも非常によく使用される型変換です。

---

### String → int

```java
String str = "100";
int num = Integer.parseInt(str);
```

結果：

```text
100
```

---

### String → double

```java
String str = "3.14";
double num = Double.parseDouble(str);
```

結果：

```text
3.14
```

---

### 数値 → String

```java
int num = 100;
String str = String.valueOf(num);
```

結果：

```text
"100"
```

---

### ラッパークラス（Wrapper Class）

プリミティブ型に対応するクラスです。

| プリミティブ型 | ラッパークラス |
| :--- | :--- |
| byte | Byte |
| short | Short |
| int | Integer |
| long | Long |
| float | Float |
| double | Double |
| char | Character |
| boolean | Boolean |

例：

```java
Integer.parseInt("100");
Double.parseDouble("3.14");
```

---

## 7. 型変換を利用した計算

整数同士で割り算を行うと、小数部分は切り捨てられます。

```java
int a = 5;
int b = 2;

System.out.println(a / b);
```

結果：

```text
2
```

---

### 正確な小数を求める場合

```java
double result = (double)a / b;
```

結果：

```text
2.5
```

---

### なぜ2.5になるのか？

```java
(double)a
```

によって

```java
5 → 5.0
```

へ変換されます。

すると、

```java
5.0 / 2
```

となるため、小数計算が行われます。

---

## 8. 面接対策用：回答例

| 質問（Q） | 回答（A） |
| :--- | :--- |
| **型変換とは何ですか？** | あるデータ型の値を別のデータ型へ変換することです。 |
| **自動型変換とは何ですか？** | 小さい型から大きい型へ変換するときに自動的に行われる型変換です。 |
| **キャストとは何ですか？** | 大きい型から小さい型へ変換する際に明示的に型を指定することです。 |
| **なぜキャストが必要ですか？** | データ損失が発生する可能性があるためです。 |
| **Stringをintへ変換するには？** | `Integer.parseInt()` を使用します。 |
| **charをintへ変換できますか？** | 可能です。文字コードの数値が取得されます。 |
| **int同士の割り算の結果は？** | 小数部分が切り捨てられます。 |

---

## 9. 面接でよく深掘りされる追加質問（実務知識）

### Q. なぜ自動型変換は小さい型から大きい型だけなのですか？

**A.**
大きい型へ変換してもデータが失われないためです。

```java
int num = 100;
double d = num;
```

* **面接での補足ポイント:**
  安全な変換であるためJavaが自動で行います。

### Q. なぜ明示的型変換が必要なのですか？

**A.**
大きい型から小さい型へ変換するとデータ損失が発生する可能性があるためです。

```java
double d = 3.99;
int num = (int)d;
```

* **面接での補足ポイント:**
  小数部分は切り捨てられます。

### Q. Integer.parseInt() は何をするメソッドですか？

**A.**
文字列として表現された数値をint型へ変換するメソッドです。

```java
String str = "100";
int num = Integer.parseInt(str);
```

### Q. int同士の割り算で小数が出ないのはなぜですか？

**A.**
演算結果もint型として扱われるためです。

```java
5 / 2
```

結果：

```text
2
```

* **面接での補足ポイント:**
  小数を求める場合は少なくとも片方をdoubleへ変換します。

---

## 10. 面接用まとめ

* 型変換：データ型を別の型へ変換すること
* 自動型変換：小さい型から大きい型への変換
* キャスト：大きい型から小さい型への変換
* char → int：文字コードへ変換
* int → char：文字へ変換
* String → int：Integer.parseInt()
* int同士の割り算：小数部分切り捨て

一言で言うと、

> **型変換とは、あるデータ型を別のデータ型へ変換することです。小さい型から大きい型への変換は自動で行われますが、大きい型から小さい型への変換はキャストが必要になります。**