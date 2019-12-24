
## やったこと
- アバター画像の設定
- 画像読み込み
- アイコン
- Card View

### 画像読み込み
New→Directoryでimagesふぉるだを作成
画像を加える
pubspec.yamlに追記

```
flutter:
  uses-material-design: true
  assets:
    - images/ramu.jpg
```
   
### Fontを変更
ここが基本無料で使えるらしい
https://fonts.google.com/

```
  fonts:
  - family: Pacifico
    fonts:
    - asset: fonts/Pacifico-Regular.ttf

  - family: Source Sans Pro
    fonts:
    - asset: fonts/SourceSansPro-Regular.ttf
```

```
Text{
  'FLUTTER DEVELOPER',
  style: TextStyle(
    fontFamily: 'Source Sans Pro',
    color: Colors.teal.shade100,
    fontSize: 20.0,
    letterSpacing: 2.5,
    fontWeight: FontWeight.bold,
  ),
)
```

### Icon
https://www.materialpalette.com/

```
Icon(Icons.add_shopping_cart)
```

### Card
https://api.flutter.dev/flutter/material/Card-class.html

#### ListTile
https://api.flutter.dev/flutter/material/ListTile-class.html

```
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.teal,
        body: SafeArea(
          child: Column(
            children: <Widget>[
              CircleAvatar(
                radius: 50.0,
                backgroundColor: Colors.red,
                backgroundImage: AssetImage('images/ramu.jpg'),
              ),
              Text(
                'mcz9mm',
                style: TextStyle(
                  fontFamily: 'Pacifico',
                  fontSize: 40.0,
                  color: Colors.white,
                  fontWeight: FontWeight.bold,
                ),
              ),
              Text(
                'FLUTTER DEVELOPER',
                style: TextStyle(
                  fontFamily: 'Source Sans Pro',
                  color: Colors.teal.shade100,
                  fontSize: 20.0,
                  letterSpacing: 2.5,
                  fontWeight: FontWeight.bold,
                ),
              ),
              Card(
                margin: EdgeInsets.symmetric(vertical: 10.0, horizontal: 25.0),
                child: ListTile(
                  leading: Icon(
                    Icons.phone,
                    color: Colors.teal,
                  ),
                  title: Text(
                      '080 4671 4096',
                      style: TextStyle(
                        color: Colors.teal.shade900,
                        fontFamily: 'Source Sans Pro',
                        fontSize: 20.0
                      ),
                  ),
                ),
              ),
              Card(
                margin: EdgeInsets.symmetric(vertical: 10.0, horizontal: 25.0),
                child: ListTile(
                  leading: Icon(
                    Icons.email,
                    color: Colors.teal,
                  ),
                  title: Text(
                    'Matarai@shinonome.io',
                    style: TextStyle(
                      color: Colors.teal.shade900,
                      fontFamily: 'Source Sans Pro',
                      fontSize: 20.0,
                    ),
                  ),
                ),
              )
            ],
          )
        ),
      ),
    );
  }
}
```

### 最終型

```
https://api.flutter.dev/flutter/material/Divider-class.html
SizedBox(
  height: 20.0,
  width: 150.0,
  child: Divider(
    color: Colors.teal.shade100,
  ),
),
```

```
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.teal,
        body: SafeArea(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              CircleAvatar(
                radius: 50.0,
                backgroundColor: Colors.red,
                backgroundImage: AssetImage('images/ramu.jpg'),
              ),
              Text(
                'mcz9mm',
                style: TextStyle(
                  fontFamily: 'Pacifico',
                  fontSize: 40.0,
                  color: Colors.white,
                  fontWeight: FontWeight.bold,
                ),
              ),
              Text(
                'FLUTTER DEVELOPER',
                style: TextStyle(
                  fontFamily: 'Source Sans Pro',
                  color: Colors.teal.shade100,
                  fontSize: 20.0,
                  letterSpacing: 2.5,
                  fontWeight: FontWeight.bold,
                ),
              ),
              SizedBox(
                height: 20.0,
                width: 150.0,
                child: Divider(
                  color: Colors.teal.shade100,
                ),
              ),
              Card(
                margin: EdgeInsets.symmetric(vertical: 10.0, horizontal: 25.0),
                child: ListTile(
                  leading: Icon(
                    Icons.phone,
                    color: Colors.teal,
                  ),
                  title: Text(
                      '080 4671 4096',
                      style: TextStyle(
                        color: Colors.teal.shade900,
                        fontFamily: 'Source Sans Pro',
                        fontSize: 20.0
                      ),
                  ),
                ),
              ),
              Card(
                margin: EdgeInsets.symmetric(vertical: 10.0, horizontal: 25.0),
                child: ListTile(
                  leading: Icon(
                    Icons.email,
                    color: Colors.teal,
                  ),
                  title: Text(
                    'Matarai@shinonome.io',
                    style: TextStyle(
                      color: Colors.teal.shade900,
                      fontFamily: 'Source Sans Pro',
                      fontSize: 20.0,
                    ),
                  ),
                ),
              )
            ],
          )
        ),
      ),
    );
  }
}
```

<img width="200" alt="スクリーンショット 2019-12-24 16 02 48" src="https://user-images.githubusercontent.com/11751495/71400140-31f85000-2669-11ea-8647-5a051e9a11fe.png">


