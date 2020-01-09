### やったこと
Flash Chat - A Lightning Fast Messaging App

- routesの設定
- Hero Animation
- Custom Flutter Animations with the Animation Controller


### routesの設定

```
class WelcomeScreen extends StatefulWidget {
　// WelcomeScreenのidを設定
  static const String id = 'welcome_screen';

  @override
  _WelcomeScreenState createState() => _WelcomeScreenState();
}


//===============================
initialRoute: WelcomeScreen.id,
routes: {
  WelcomeScreen.id: (context) => WelcomeScreen(),
  LoginScreen.id: (context) => LoginScreen(),
  RegistrationScreen.id: (context) => RegistrationScreen(),
  ChatScreen.id: (context) => ChatScreen(),
},
```


### Hero Animation
https://flutter.dev/docs/development/ui/animations/hero-animations

- Hero Widget (遷移前と遷移後の画面にそれぞれ配置)
- Shared tag property (Hero Widgetを識別する上で同じ値を設定)
- Navigator-based Screen Transitions (プッシュやポップを使って遷移)

遷移前の画面
```
Hero(
  tag: 'logo',
  child: Container(
    child: Image.asset('images/logo.png'),
    height: 60.0,
  ),
),
```

遷移後の画面
```
Hero(
  tag: 'logo',
  child: Container(
    height: 200.0,
    child: Image.asset('images/logo.png'),
   ),
),
```

![Jan-08-2020 09-58-54](https://user-images.githubusercontent.com/11751495/71941557-853bd800-31fd-11ea-95ac-17ecb1e9ac97.gif)


### Custom Flutter Animations with the Animation Controller

- A Ticker(時間、時間毎にアニメーションを伝える、形や色の変化)
- Animation Controller(アニメーションの停止や開始など管理をしている)
- An Animation Value(実際にアニメーション化するもの)

透明度を使ったアニメーション
```
class _WelcomeScreenState extends State<WelcomeScreen> with SingleTickerProviderStateMixin {

  AnimationController controller;

@override
  void initState() {
    super.initState();

    controller = AnimationController(
      duration: Duration(seconds: 1),
      vsync: this,
    );

    controller.forward();

    controller.addListener(() {
      setState(() {

      });
      print(controller.value);
    });
  }
  
// ScaffoldのbackgroundColorの透明度をアニメーションさせる
backgroundColor: Colors.red.withOpacity(controller.value),
```

![Jan-09-2020 08-33-51](https://user-images.githubusercontent.com/11751495/72025241-ce9e2d00-32ba-11ea-93cc-8c689ac572df.gif)


upperBoundを設定すれば0から任意の数値に変更できる(この場合0~100)
下限(lowerBound)も設定可能
```
controller = AnimationController(
      duration: Duration(seconds: 1),
      vsync: this,
      upperBound: 100.0,
      // lowerBound: 30.0,
    );
```

![Jan-09-2020 08-46-11](https://user-images.githubusercontent.com/11751495/72025762-85e77380-32bc-11ea-93bd-bd47ded6db3d.gif)

#### CurvedAnimation

直線的にアニメーションするのではなく、曲線でアニメーションさせる
https://api.flutter.dev/flutter/animation/CurvedAnimation-class.html

https://api.flutter.dev/flutter/animation/Curves-class.html

```
// Animationを作成
Animation animation;

// CurvedAnimationは0-1の間で動くのでその範囲を超えるupperBoundは使えない
controller = AnimationController(
      duration: Duration(seconds: 1),
      vsync: this,
    );

animation = CurvedAnimation(parent: controller, curve: Curves.decelerate);

// 0~1なので高さを100倍にする
height: animation.value * 100,
```


![Jan-09-2020 08-59-15](https://user-images.githubusercontent.com/11751495/72026302-605b6980-32be-11ea-88b1-661d2e11e620.gif)

#### アニメーションを逆再生する

```
controller.reverse(from: 1.0);
```

#### addStatusListenerでステータスを確認しループさせる
```
animation.addStatusListener((status) {
  if (status == AnimationStatus.completed) {
    controller.reverse(from: 1.0);
  } else if (status == AnimationStatus.dismissed) {
    controller.forward();
  }
});
```

![Jan-09-2020 09-31-22](https://user-images.githubusercontent.com/11751495/72027553-d8c42980-32c2-11ea-8cf2-28d8778f935d.gif)

#### 画面が閉じられるタイミングでdispose

別画面へ遷移してもアニメーションのリソースは消費したままなので
明示的に終了させる必要がある。
```
@override
void dispose() {
  controller.dispose();   
  super.dispose();
}
```

### Repositories
https://github.com/mcz9mm/flash-chat-flutter


