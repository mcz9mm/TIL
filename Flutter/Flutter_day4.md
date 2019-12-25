### やったこと

- Expandedでエリア内にパーツを広げる
- クリック判定をつける
- ランダム値を扱う

### Expanded
https://api.flutter.dev/flutter/widgets/Expanded-class.html

```
children: <Widget>[
  Expanded(
    flex: 2, // 2:1で描画
    child: Image.asset('images/dice1.png'),
  ),
  Expanded(
    flex: 1　// 1:2で描画
    child: Image.asset('images/dice1.png'),
  ),
],
```

### クリック判定をつける(FlatButton)
https://api.flutter.dev/flutter/material/FlatButton-class.html

```
child: FlatButton(
  onPressed: () {
    print('Left button got pressed');
  },
  child: Image.asset('images/dice1.png'),
),
```

setState()でUIの変更を行う

```
child: FlatButton(
  onPressed: () {
    setState(() {
      leftDiceNumber = 5;
    });
    print('Left button got pressed');
  },
  child: Image.asset('images/dice$leftDiceNumber.png'),
),
```


StatelessWidget→StatefulWidgeに変更

```
class DicePage extends StatefulWidget {
  @override
  _DicePageState createState() => _DicePageState();
}

class _DicePageState extends State<DicePage> {
  int leftDiceNumber = 1;
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Row(
        children: <Widget>[
          Expanded(
            child: FlatButton(
              onPressed: () {
                setState(() {
                  leftDiceNumber = 5;
                });
                print('Left button got pressed');
              },
              child: Image.asset('images/dice$leftDiceNumber.png'),
            ),
          ),
          Expanded(
            child: FlatButton(
              onPressed: (){
                print('Right button got pressed');
              },
              child: Image.asset('images/dice1.png'),
            ),
          ),
        ],
      ),
    );
  }
}
```

### ランダム値を扱う

```
import 'dart:math';

leftDiceNumber = Random().nextInt(6); // 0-5
leftDiceNumber = Random().nextInt(6) + 1; // 1-6
```

### できたもの

```
class DicePage extends StatefulWidget {
  @override
  _DicePageState createState() => _DicePageState();
}

class _DicePageState extends State<DicePage> {
  int leftDiceNumber = 1;
  int rightDiceNumber = 1;

  void changeDiceFace() {
    setState(() {
      leftDiceNumber = Random().nextInt(6) + 1;
      rightDiceNumber = Random().nextInt(6) + 1;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Center(
      child: Row(
        children: <Widget>[
          Expanded(
            child: FlatButton(
              onPressed: () {
                changeDiceFace();
                print('Left button got pressed');
              },
              child: Image.asset('images/dice$leftDiceNumber.png'),
            ),
          ),
          Expanded(
            child: FlatButton(
              onPressed: (){
                changeDiceFace();
                print('Right button got pressed');
              },
              child: Image.asset('images/dice$rightDiceNumber.png'),
            ),
          ),
        ],
      ),
    );
  }
}
```

![Dec-25-2019 13-26-09](https://user-images.githubusercontent.com/11751495/71438999-2ffec180-273b-11ea-9cee-428636a5e27e.gif)

