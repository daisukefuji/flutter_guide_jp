---
title: "External package"
date: 2019-02-08T00:00:00+09:00
draft: false
weight: 24
---

## Step2

1.次に外部パッケージの取り込み方法を学びましょう。```/pubspec.yaml```で依存関係を管理するので、以下のように編集します。   

```yaml
  dependencies:
     flutter:
       sdk: flutter
     cupertino_icons: ^0.1.2
+    english_words: ^3.1.0
```

今回取り込むのは```english_words```というパッケージです。
このパッケージはランダムに英単語を生成するためのライブラリで、デモやテストなどランダムに文字列を取得したいときに利用します。   
[english_words](https://pub.dartlang.org/packages/english_words)

Flutterで使える外部パッケージは[Flutter Paclages](https://pub.dartlang.org/flutter)で手に入るので、何か作るときは一度パッケージがないか探してみるといいと思います。

2.通常は```/pubspec.yaml```に変更を加え保存すると同時にパッケージがダウンロードされます。
もしダウンロードされない場合は直接以下コマンドを叩いてパッケージを取得してください。
```bash
$ flutter packages get
```

3.```lib/main.dart```に先ほど取得した外部パッケージをimportします。
```dart
  import 'package:flutter/material.dart';
+ import 'package:english_words/english_words.dart';
```

4.固定で表示していた文字列をランダムな英語に変更しましょう。

```dart
  @override
  Widget build(BuildContext context) {
+    final wordPair = WordPair.random();
    return MaterialApp(
      title: 'Welcome to Flutter',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Welcome to Flutter'),
        ),
        body: Center(
-          child: Text('Hello World'),
+          child: Text(wordPair.asPascalCase),
        ),
      ),
    );
  }
```

5.変更したらソースを保存してみてください。
ホットリロードのタイミングで表示される単語が変わるようになったかと思います。
これは、buildメソッド内で「MaterialApp」がレンダリングが必要になるたびに、生成されているためです。

<img src="http://flutter.ctrnost.com/images/tutorial/04/01_english_words.png" width="600px"  alt="English Words">
