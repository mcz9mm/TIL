### やったこと

- Flutter Themesを利用する
  - CustomColorを設定
  - ThemeDataを自作する場合
  - Themeを元に編集する
  - 一部のウィジェットだけThemeをあてる
- 構成メモ


### Flutter Themesを利用する
https://flutter.dev/docs/cookbook/design/themes

[ThemeData](https://api.flutter.dev/flutter/material/ThemeData-class.html)が必要。
アプリ全体のテーマを設定することができる。フォントやボタンをデフォルトで統一したりすることができる。

<img width="200" alt="スクリーンショット 2019-12-30 12 44 54" src="https://user-images.githubusercontent.com/11751495/71567419-3bb70300-2b02-11ea-847d-6556aadf9380.png">

```
class BMICalculator extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData.dark(),
      home: InputPage(),
    );
  }
}
```

#### CustomColorを設定
https://api.flutter.dev/flutter/dart-ui/Color-class.html

```
Color c = const Color(0xFF42A5F5);
Color c = const Color.fromARGB(0xFF, 0x42, 0xA5, 0xF5);
Color c = const Color.fromARGB(255, 66, 165, 245);
Color c = const Color.fromRGBO(66, 165, 245, 1.0);

```

#### ThemeDataを自作する場合
ThemeDataのProperties利用してカスタムできる

<img width="200" alt="スクリーンショット 2019-12-30 13 05 45" src="https://user-images.githubusercontent.com/11751495/71567806-2099c280-2b05-11ea-98c3-26b9159b541b.png">

```
theme: ThemeData(
        primaryColor: Color(0xFF0A0E21),
        scaffoldBackgroundColor: Color(0xFF0A0E21),
        accentColor: Colors.purple,
        textTheme: TextTheme(
            body1: TextStyle(color: Color(0xFFFFFFFF)),
        )
      ),
```



### ThemeDataを元に編集する場合

<img width="200" alt="スクリーンショット 2019-12-30 13 13 57" src="https://user-images.githubusercontent.com/11751495/71567935-57bca380-2b06-11ea-9ba4-3f8117135a43.png">

```
theme: ThemeData.dark().copyWith(
          primaryColor: Color(0xFF0A0E21),
          scaffoldBackgroundColor: Color(0xFF0A0E21),
      ),
```


### 一部のウィジェットだけThemeをあてる

「ThemeDataを元に編集する場合」で全体にテーマを設定し、さらに一部変更したい場合、WidgetをThemeWidget内に
ラップするだけでWidgetのThemeを変更することができる。


<img width="200" alt="スクリーンショット 2019-12-30 13 14 07" src="https://user-images.githubusercontent.com/11751495/71567934-57bca380-2b06-11ea-9776-fe5905e40585.png">

```
import 'package:flutter/material.dart';

void main() => runApp(BMICalculator());

class BMICalculator extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData.dark().copyWith(
          primaryColor: Color(0xFF0A0E21),
          scaffoldBackgroundColor: Color(0xFF0A0E21),
      ),
      home: InputPage(),
    );
  }
}

class InputPage extends StatefulWidget {
  @override
  _InputPageState createState() => _InputPageState();
}

class _InputPageState extends State<InputPage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('BMI CALCULATOR'),
      ),
      body: Center(
        child: Text('Body Text'),
      ),
      floatingActionButton: Theme(
        data: ThemeData(accentColor: Colors.purple),
        child: FloatingActionButton(
          child: Icon(Icons.add),
        ),
      ),
    );
  }
}
```

### 構成メモ

Flutterプロジェクトの構成は基本的に下記のような感じが多いらしい。
アプリのテーマや最初の画面の呼び出しなど。

```
void main() => runApp(BMICalculator());

class BMICalculator extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData.dark().copyWith(
          primaryColor: Color(0xFF0A0E21),
          scaffoldBackgroundColor: Color(0xFF0A0E21),
      ),
      home: InputPage(),
    );
  }
}

```


### Repositories
https://github.com/mcz9mm/bmi-calculator-flutter
