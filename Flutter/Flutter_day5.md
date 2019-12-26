### やったこと
- 課題「 Boss Level Challenge 1 - Magic 8 Ball」にチャレンジ
- Packageの追加
- Audioの再生
- Xylophone - Using Flutter and Dart Packages to Speed Up Development

### Boss Level Challenge 1 - Magic 8 Ball
前回までの内容の確認だったので５分ほどでできてしまった。
https://github.com/mcz9mm/magic-8-ball-flutter

<img width="200" alt="スクリーンショット 2019-12-25 18 30 31" src="https://user-images.githubusercontent.com/11751495/71457936-c981ae00-27e3-11ea-9388-e1ca6167ee84.png">



### Packageの追加（例）
https://pub.dev/flutter/packages?q=
スコアリングは
- Popularity:    
- Health:Code
- Maintenance
- Overall

４つの観点で設定されている。
もちろんスコアが高ければ高いほど頻繁に使われているし、
メンテナンス性が高く利用しやすい。

![スクリーンショット 2019-12-25 19 27 35](https://user-images.githubusercontent.com/11751495/71457978-f2a23e80-27e3-11ea-8dd2-86029b5f9afa.png)

https://pub.dev/packages/english_words#-installing-tab-

```
Use this package as a library
1. Depend on it
Add this to your package's pubspec.yaml file:


dependencies:
  english_words: ^3.1.5

2. Install it
You can install packages from the command line:

with pub:


$ pub get

with Flutter:


$ flutter pub get

Alternatively, your editor might support pub get or flutter pub get. Check the docs for your editor to learn more.

3. Import it
Now in your Dart code, you can use:

import 'package:english_words/english_words.dart';
```

### Audioの再生
https://pub.dev/packages/audioplayers

```
import 'package:audioplayers/audio_cache.dart';

child: FlatButton(
  onPressed: () {
    final player = AudioCache();
    player.play('note1.wav');
  },
  child: Text('Click Me'),
),
```

### メソッドに引数を持たせる
```
void playSound(int soundNumber) {
  final player = AudioCache();
  player.play('note$soundNumber.wav');
}
```

引数2つの場合

```
// 中括弧をつけることで呼び出しの際に引数名を指定できる
greet(greeting: 'How do you do',personToGreet: 'Jackie');

void greet({String personToGreet, String greeting}) {
  print('$personToGreet $greeting')
}
```

課題

ExpandedとColumnのCrossAxisAlignment.stretchを使う

<img width="200" alt="スクリーンショット 2019-12-26 12 51 12" src="https://user-images.githubusercontent.com/11751495/71457977-f2a23e80-27e3-11ea-8cbc-a9e299134f6e.png">

```
import 'package:flutter/material.dart';
import 'package:audioplayers/audio_cache.dart';

void main() => runApp(XylophoneApp());

class XylophoneApp extends StatelessWidget {

  void playSound({int soundNumber}) {
    final player = AudioCache();
    player.play('note$soundNumber.wav');
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.black,
        body: SafeArea(
          child: Column(
            mainAxisSize: MainAxisSize.max,
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: <Widget>[
              Expanded(
                child: FlatButton(
                  onPressed: () {
                    playSound(soundNumber: 1);
                  },
                  color: Colors.red,
                ),
              ),
              Expanded(
                child: FlatButton(
                  onPressed: () {
                    playSound(soundNumber: 2);
                  },
                  color: Colors.orange,
                ),
              ),
              Expanded(
                child: FlatButton(
                  onPressed: () {
                    playSound(soundNumber: 3);
                  },
                  color: Colors.yellow,
                ),
              ),
              Expanded(
                child: FlatButton(
                  onPressed: () {
                    playSound(soundNumber: 4);
                  },
                  color: Colors.green,
                ),
              ),
              Expanded(
                child: FlatButton(
                  onPressed: () {
                    playSound(soundNumber: 5);
                  },
                  color: Colors.teal,
                ),
              ),
              Expanded(
                child: FlatButton(
                  onPressed: () {
                    playSound(soundNumber: 6);
                  },
                  color: Colors.blue,
                ),
              ),
              Expanded(
                child: FlatButton(
                  onPressed: () {
                    playSound(soundNumber: 7);
                  },
                  color: Colors.purple,
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```
