### やったこと
- メソッドにreturnをもたせる
- arrow function
- セクション9: Xylophoneの完成


### メソッドにreturnをもたせる
```
double result = myFunction();
print(result);

double myFunction() {
    double pi = 3.14159;
    return pi * 2;
}

int addResult = add(n1: 5, n2: 9); // 14

int add({int n1, int n2}) {
    return n1 + n2;
}
```

Widgetもreturnに持たせられる

```
Expanded buildKey({Color color, int soundNumber}) {
    return Expanded(
      child: FlatButton(
        onPressed: () {
          playSound(soundNumber: soundNumber);
        },
        color: color,
      ),
    );
  }
```

### arrow function
中括弧で囲むのと同じ
arrow functionの場合は１行のみ(連結ができない)

```
int add() {
    return 5 + 2;
}
// 上と同じ
int add() => 5 + 2;

int add(int n1, int n2) => n1 + n2;

//=======================
void main() => runApp(XylophoneApp());

// 上と同じ
void main() {
  runApp(
      XylophoneApp()
  );
}
```

### セクション9: Xylophoneの完成

```
import 'package:flutter/material.dart';
import 'package:audioplayers/audio_cache.dart';

void main() => runApp(XylophoneApp());

class XylophoneApp extends StatelessWidget {

  void playSound({int soundNumber}) {
    final player = AudioCache();
    player.play('note$soundNumber.wav');
  }

  Expanded buildKey({Color color, int soundNumber}) {
    return Expanded(
      child: FlatButton(
        onPressed: () {
          playSound(soundNumber: soundNumber);
        },
        color: color,
      ),
    );
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
              buildKey(color: Colors.red, soundNumber: 1),
              buildKey(color: Colors.orange, soundNumber: 2),
              buildKey(color: Colors.yellow, soundNumber: 3),
              buildKey(color: Colors.green, soundNumber: 4),
              buildKey(color: Colors.teal, soundNumber: 5),
              buildKey(color: Colors.blue, soundNumber: 6),
              buildKey(color: Colors.purple, soundNumber: 7),
            ],
          ),
        ),
      ),
    );
  }
}
```
