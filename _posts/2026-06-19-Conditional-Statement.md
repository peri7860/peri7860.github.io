---
title: "Java基礎知識：条件文（Conditional Statement）のまとめ"
date: 2026-06-19 22:52:00 +0900
categories: [JAVA‐入門]  
tags: [JAVA, String, 参照型, equals()]
---

# Java基礎知識：条件文（Conditional Statement）のまとめ

## 1. 条件文とは？

**条件文（Conditional Statement）**とは、指定した条件が真（true）か偽（false）かによって、実行する処理を分岐させるための構文です。

プログラムでは、

* ログイン成功・失敗
* 点数による合否判定
* 年齢による利用制限
* メニュー選択

など、状況によって異なる処理を行う場面が多くあります。

そのような場合に条件文を使用します。

---

## 2. 条件文の種類

Javaには主に以下の条件分岐があります。

| 種類 | 説明 |
| :--- | :--- |
| if文 | 条件がtrueのときだけ実行 |
| if-else文 | trueとfalseで処理を分岐 |
| if-else if-else文 | 複数条件を判定 |
| ネストしたif文 | if文の中にif文を書く |
| switch文 | 値によって処理を分岐 |
| 三項演算子 | 条件によって値を選択 |

---

## 3. if文

最も基本的な条件文です。

条件がtrueの場合のみ処理を実行します。

### 基本構文

```java
if(条件式){
    実行文;
}
```

---

### 使用例

```java
int score = 80;

if(score >= 60){
    System.out.println("合格");
}
```

結果：

```text
合格
```

---

### 条件がfalseの場合

```java
int score = 50;

if(score >= 60){
    System.out.println("合格");
}
```

結果：

```text
（何も出力されない）
```

条件がfalseの場合、ifブロック内の処理は実行されません。

---

## 4. 条件式とは？

if文の括弧内には、

```java
true
```

または

```java
false
```

を返す式を書きます。

例：

```java
score >= 60
```

```java
age >= 20
```

```java
name.equals("Tanaka")
```

---

### 比較演算子の例

| 演算子 | 意味 |
| :--- | :--- |
| == | 等しい |
| != | 等しくない |
| > | より大きい |
| < | より小さい |
| >= | 以上 |
| <= | 以下 |

---

### 使用例

```java
int age = 20;

if(age >= 18){
    System.out.println("成人です");
}
```

---

### boolean型の変数をそのまま使う

boolean型の場合は、比較せずそのまま条件式に書くことができます。

```java
boolean flag = true;

if(flag){
    System.out.println("実行");
}
```

初心者は次のように書くことがあります。

```java
if(flag == true){
    System.out.println("実行");
}
```

動作に問題はありませんが、

```java
if(flag)
```

の方が簡潔で読みやすいため、実務ではこちらが一般的です。

falseの場合は、

```java
if(!flag)
```

と書きます。

---

## 5. if文で複数の処理を書く

波括弧 `{}` の中には複数の文を書くことができます。

```java
int score = 90;

if(score >= 60){
    System.out.println("合格");
    System.out.println("おめでとうございます");
}
```

結果：

```text
合格
おめでとうございます
```

---

## 6. ブロック（{}）について

if文で実行される範囲をブロックと呼びます。

```java
if(score >= 60){
    System.out.println("合格");
    System.out.println("おめでとう");
}
```

この場合、

```java
{
    System.out.println("合格");
    System.out.println("おめでとう");
}
```

の部分がブロックです。

---

### 1行だけの場合

```java
if(score >= 60)
    System.out.println("合格");
```

このように波括弧を省略することもできます。

しかし実務では可読性や保守性のため、

```java
if(score >= 60){
    System.out.println("合格");
}
```

のように波括弧を付けることが推奨されています。

---

## 7. if-else文

条件がtrueかfalseかによって処理を分岐する構文です。

### 基本構文

```java
if(条件式){
    trueの場合の処理
}else{
    falseの場合の処理
}
```

---

### 使用例

```java
int score = 50;

if(score >= 60){
    System.out.println("合格");
}else{
    System.out.println("不合格");
}
```

結果：

```text
不合格
```

---

## 8. if-else if-else文

複数の条件を順番に判定したい場合に使用します。

### 基本構文

```java
if(条件1){
    処理1
}else if(条件2){
    処理2
}else{
    その他の処理
}
```

---

### 使用例

```java
int score = 85;

if(score >= 90){
    System.out.println("A");
}else if(score >= 80){
    System.out.println("B");
}else if(score >= 70){
    System.out.println("C");
}else{
    System.out.println("D");
}
```

結果：

```text
B
```

---

### 判定順序に注意

条件は上から順番に評価されます。

```java
if(score >= 60){
    System.out.println("合格");
}else if(score >= 90){
    System.out.println("優秀");
}
```

この場合、90点でも最初の条件で判定が終了するため、

```java
優秀
```

は出力されません。

条件は狭い範囲から広い範囲へ書くのが基本です。

---

## 9. ネストしたif文（Nested if）

if文の中にif文を書くこともできます。

```java
if(id.equals("admin")){
    if(pw.equals("1234")){
        System.out.println("ログイン成功");
    }
}
```

---

### ネストしすぎに注意

ネストが深くなるとコードが読みにくくなります。

```java
if(a){
    if(b){
        if(c){
            if(d){
            }
        }
    }
}
```

実務ではネストを浅く保つことが重要です。

---

## 10. 論理演算子を使った条件式

複数の条件を組み合わせることもできます。

---

### AND（&&）

両方の条件がtrueの場合のみtrueになります。

```java
int age = 25;

if(age >= 20 && age <= 30){
    System.out.println("20代です");
}
```

---

### OR（||）

どちらか一方がtrueならtrueになります。

```java
if(score >= 90 || rank == 1){
    System.out.println("優秀");
}
```

---

### NOT（!）

trueとfalseを反転します。

```java
boolean flag = true;

if(!flag){
    System.out.println("実行");
}
```

---

## 11. Stringの比較に注意

初心者がよく間違えるポイントです。

文字列比較では

```java
==
```

ではなく

```java
equals()
```

を使用します。

---

### 悪い例

```java
String id = "admin";

if(id == "admin"){
}
```

---

### 良い例

```java
String id = "admin";

if(id.equals("admin")){
}
```

---

### 実務で推奨される書き方

```java
if("admin".equals(id)){
}
```

この書き方なら、

```java
id == null
```

の場合でも安全です。

---

## 12. switch文

特定の値によって処理を分岐する構文です。

### 基本構文

```java
switch(変数){
    case 値1:
        処理;
        break;

    case 値2:
        処理;
        break;

    default:
        処理;
}
```

---

### 使用例

```java
int menu = 2;

switch(menu){
    case 1:
        System.out.println("コーヒー");
        break;

    case 2:
        System.out.println("ジュース");
        break;

    default:
        System.out.println("その他");
}
```

結果：

```text
ジュース
```

---

### breakの役割

breakを書かないと次のcaseまで実行されます。

```java
case 1:
    System.out.println("A");

case 2:
    System.out.println("B");
```

結果：

```text
A
B
```

---

## 13. 三項演算子

条件によって値を選択する演算子です。

### 基本構文

```java
条件 ? 真の場合 : 偽の場合
```

---

### 使用例

```java
int score = 80;

String result =
    score >= 60 ? "合格" : "不合格";
```

結果：

```text
合格
```

---

## 14. if文の実務での利用例

### ログイン判定

```java
String id = "admin";
String pw = "1234";

if("admin".equals(id) &&
   "1234".equals(pw)){
    System.out.println("ログイン成功");
}
```

---

### 年齢判定

```java
int age = 20;

if(age >= 18){
    System.out.println("利用可能");
}
```

---

### 偶数判定

```java
int num = 8;

if(num % 2 == 0){
    System.out.println("偶数");
}
```

---

## 15. 面接対策用：回答例

| 質問（Q） | 回答（A） |
| :--- | :--- |
| 条件文とは何ですか？ | 条件によって実行する処理を分岐させる構文です。 |
| if文とは何ですか？ | 条件がtrueの場合のみ処理を実行する条件文です。 |
| if-else文とは何ですか？ | trueとfalseで処理を分岐する条件文です。 |
| else if文とは何ですか？ | 複数の条件を順番に判定する条件文です。 |
| switch文とは何ですか？ | 値によって処理を分岐する条件文です。 |
| 条件式とは何ですか？ | trueまたはfalseを返す式です。 |
| Stringの比較はどうしますか？ | equals()を使用します。 |
| &&とは何ですか？ | 両方がtrueの場合のみtrueになる論理演算子です。 |
| \|\|とは何ですか？ | どちらか一方がtrueならtrueになる論理演算子です。 |

---

## 16. 面接でよく深掘りされる追加質問（実務知識）

### Q. if文の条件には何を書けますか？

**A.**

最終的にboolean型（trueまたはfalse）になる式を書きます。

```java
if(score >= 60){
}
```

```java
if(age >= 20){
}
```

```java
if(flag){
}
```

* **面接での補足ポイント**

  JavaではC言語のように数値を条件式として扱うことはできません。

```java
if(1)
```

はコンパイルエラーになります。

---

### Q. if文とswitch文の違いは何ですか？

**A.**

if文は条件式を自由に記述できますが、switch文は特定の値との一致判定に使用します。

```java
if(score >= 60){
}
```

```java
switch(menu){
    case 1:
        break;
}
```

* **面接での補足ポイント**

  範囲判定にはif文、固定値の分岐にはswitch文が適しています。

---

### Q. なぜ波括弧 {} を省略しない方が良いのですか？

**A.**

保守性と可読性が向上するためです。

```java
if(score >= 60)
    System.out.println("合格");
```

後から処理を追加するとバグの原因になることがあります。

```java
if(score >= 60){
    System.out.println("合格");
}
```

のように書くのが一般的です。

---

### Q. 実務でよく使うif文の書き方はありますか？

**A.**

NullPointerExceptionを防ぐため、

```java
if("admin".equals(id)){
}
```

のように定数側からequals()を呼び出す書き方がよく使われます。

---

### Q. Early Returnとは何ですか？

**A.**

条件を満たさない場合に先に処理を終了し、ネストを減らす書き方です。

```java
public void login(String id){

    if(id == null){
        return;
    }

    System.out.println(id);
}
```

---

#### あまり良くない例

```java
public void login(String id){

    if(id != null){

        if(id.length() > 0){

            System.out.println(id);

        }

    }
}
```

---

#### Early Returnを使った例

```java
public void login(String id){

    if(id == null){
        return;
    }

    if(id.length() == 0){
        return;
    }

    System.out.println(id);
}
```

* **面接での補足ポイント**

  実務ではネストを減らし、コードの可読性を向上させるためにEarly Returnがよく使用されます。

---

## 17. 面接用まとめ

* 条件文：条件によって処理を分岐する構文
* if文：条件がtrueの場合のみ実行
* if-else文：trueとfalseで分岐
* else if文：複数条件を判定
* switch文：値による分岐
* 条件式：trueまたはfalseを返す式
* 比較演算子：==、 !=、 >、 <、 >=、 <=
* 論理演算子：&&、||、 !
* String比較：equals()
* 実務では波括弧を省略しない
* Null対策として `"文字列".equals(変数)` を使用する
* ネストを減らすためにEarly Returnを活用する

一言で言うと、

> **条件文は、条件の真偽によって実行する処理を切り替えるための構文です。Javaではif文、if-else文、switch文を適切に使い分け、実務では可読性・保守性・安全性を意識したコードを書くことが重要です。**