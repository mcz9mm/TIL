### やったこと
- ButtonWidgetを0から構築する
- Navigate to a new screen and back
- Navigate with named routes
- 結果画面へ遷移する


### ButtonWidgetを0から構築する

<img width="131" alt="スクリーンショット 2020-01-01 17 08 53" src="https://user-images.githubusercontent.com/11751495/71639413-7adb8480-2cb9-11ea-900e-eafbf7a8c537.png">


https://api.flutter.dev/flutter/material/RawMaterialButton-class.html

```
class RoundIconButton extends StatelessWidget {

  RoundIconButton({this.icon});
  final IconData icon;

  @override
  Widget build(BuildContext context) {
    return RawMaterialButton(
      onPressed: () {

      },
      child: Icon(icon),
      elevation: 6.0,
      disabledElevation: 6.0,
      constraints: BoxConstraints.tightFor(
        width: 56.0,
        height: 56.0,
      ),
      shape: CircleBorder(),
      fillColor: Color(0xFF4C4F5E),
    );
  }
}
```

### 四角ベースにもできる

```
class RoundIconButton extends StatelessWidget {

  RoundIconButton({this.icon});
  final IconData icon;

  @override
  Widget build(BuildContext context) {
    return RawMaterialButton(
      onPressed: () {

      },
      child: Icon(icon),
      elevation: 6.0,
      disabledElevation: 6.0,
      constraints: BoxConstraints.tightFor(
        width: 56.0,
        height: 56.0,
      ),
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(10.0)), //四角の角丸
      fillColor: Color(0xFF4C4F5E),
    );
  }
}
```
<img width="127" alt="スクリーンショット 2020-01-01 17 09 18" src="https://user-images.githubusercontent.com/11751495/71639412-7adb8480-2cb9-11ea-8c74-de8912034e1b.png">


![Jan-01-2020 23-40-40](https://user-images.githubusercontent.com/11751495/71642534-27385d80-2cf0-11ea-951e-d50e0a60015a.gif)


### Navigate to a new screen and back

https://flutter.dev/docs/cookbook/navigation/navigation-basics

#### Push
```
// Within the `FirstRoute` widget
onPressed: () {
  Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => SecondRoute()),
  );
}
```

#### Pop

```
// Within the SecondRoute widget
onPressed: () {
  Navigator.pop(context);
}
```

### Navigate with named routes
https://flutter.dev/docs/cookbook/navigation/named-routes

```
MaterialApp(
  // Start the app with the "/" named route. In this case, the app starts
  // on the FirstScreen widget.
  initialRoute: '/',
  routes: {
    // When navigating to the "/" route, build the FirstScreen widget.
    '/': (context) => FirstScreen(),
    // When navigating to the "/second" route, build the SecondScreen widget.
    '/second': (context) => SecondScreen(),
  },
);
```

サンプルだとこんな感じ

https://github.com/londonappbrewery/Navigation-Flutter-Demo

ただし、homeとinitialRouteを両方設定すると競合してしまうので注意。
> home: Screen0(),
> initialRoute: '/',

```
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      initialRoute: '/',
      routes: {
        '/': (context) => Screen0(),
        '/first': (context) => Screen1(),
        '/second': (context) => Screen2(),
      },
    );
  }
}
```

#### Navigate to the second screen 

```
// Within the `FirstScreen` widget
onPressed: () {
  // Navigate to the second screen using a named route.
  Navigator.pushNamed(context, '/second');
}
```


#### Return to the first screen

```
// Within the SecondScreen widget
onPressed: () {
  // Navigate back to the first screen by popping the current route
  // off the stack.
  Navigator.pop(context);
}
```


### 結果画面へ遷移する
おさらい

![Jan-02-2020 00-45-47](https://user-images.githubusercontent.com/11751495/71643171-4687b880-2cf9-11ea-8653-7f9e342ac282.gif)

```
          GestureDetector(
            onTap: () {
              Navigator.push(context, MaterialPageRoute(builder: (context) {
                return ResultsPage();
              }));
            },
            child: Container(
              child: Text('CALCULATE'),
              color: kBottomContainerColor,
              margin: EdgeInsets.only(top: 10.0),
              width: double.infinity,
              height: kBottomContainerHeight,
            ),
          )
```
