
### やったこと
- Shared preferencesで初回インストール時画面を表示
- Splash画面を用意して初回設定を行う

#### Shared preferencesで初回インストール時画面を表示
[FlutterでSharedPreferencesを使ってローカルにデータを保存する](https://www.virment.com/how-to-use-shared-preferences-in-flutter/)
[shared_preferences | Flutter Package](https://pub.dev/packages/shared_preferences#-readme-tab-)

KeyValueで保存できる
##### 保存できる型
- int
* double
* bool
* String
* List<String>

らしい
> SQLiteのようなデータベースを想定して使うものではないです。  

##### 起動判定(取得)
初回インストールであればtrueを返す
```
Future<bool> _checkFirstInstall() async {
  final SharedPreferences prefs = await SharedPreferences.getInstance();
  return prefs.getBool(kFirstInstallKey) ?? true;
}
```

##### 保存
```
_setFirstInstall() async {
  final SharedPreferences prefs = await SharedPreferences.getInstance();
  prefs.setBool(kFirstInstallKey, false);
}
```

#### Splash画面を用意して初回設定を行う
初回画面の切り分けを行う際に必要になったので調べてみると、スプラッシュ画面を用意しておき、その際に起動直後に行う処理を設定すると良いらしい。
[Flutter スプラッシュ画面の作り方 | Qrunch（クランチ）](https://qrunch.net/@chihara/entries/O5YDL5yF0lBbBo4K)

↑↑のリンク先とほぼ同様の実装になっているが、
タイマーは実際なくても大丈夫。`_initialize()`で主に行いたいことを書く。
```
import ‘dart:async’;
import ‘package:flutter/material.dart’;
import ‘package:shared_preferences/shared_preferences.dart’;
import ‘package:saving_money/pages/root_page.dart’;
import ‘package:saving_money/pages/introduce_page.dart’;
import ‘package:saving_money/constants.dart’;

class SplashPage extends StatefulWidget {
  @override
  State<StatefulWidget> createState() => _SplashPage();
}

class _SplashPage extends State<SplashPage> {

  bool _expired = false;
  bool _initialized = false;
  bool isFirstInstall;

  Future<bool> _checkFirstInstall() async {
    final SharedPreferences prefs = await SharedPreferences.getInstance();
    isFirstInstall = prefs.getBool(kFirstInstallKey) ?? true;
    return isFirstInstall;
  }

  @override
  void initState() {
    super.initState();
    _initialize();
    _startTimer();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Container(
        color: kFloatingButtonColor,
        child: Center(
          child: Container(
            width: 100,
            height: 100,
            child: Image.asset(
              ‘assets/png/logo.png’,
              fit: BoxFit.fill,
            ),
          )
        ),
      ),
    );
  }

  // 初期化処理
  _initialize() async {
    isFirstInstall = await _checkFirstInstall();
    _initialized = true;
    _moveToMainScreen();
  }

  _startTimer() async {
    Timer(Duration(seconds: 2), () {
      _expired = true;
      _moveToMainScreen();
    });
  }

  _moveToMainScreen() {
    if (_initialized && _expired) {
      Navigator.pushReplacement(context, MaterialPageRoute(
          builder: (context) => isFirstInstall ? IntroducePage() : RootPage(),
      ));
    }
  }
}

```
