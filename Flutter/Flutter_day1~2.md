# flutter TIL day1,2

### Container
[Container class - widgets library - Dart API](https://api.flutter.dev/flutter/widgets/Container-class.html)

### SafeArea

1. option+enter 
2. Wrap with new widget
3. widget→SafeAreaに変更

<img width="353" alt="スクリーンショット 2019-12-22 10 17 51" src="https://user-images.githubusercontent.com/11751495/71317831-f7f14780-24ca-11ea-9825-6dbe901f690c.png">


``` dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.teal,
        body: SafeArea(
          child: Container(
            color: Colors.white,
            child: Text('Hello'),
          ),
        ),
      ),
    );
  }
}
```

### margin, padding
[EdgeInsets class - painting library - Dart API](https://api.flutter.dev/flutter/painting/EdgeInsets-class.html)

上下左右20.0
``` 
margin: EdgeInsets.all(20.0),
```

垂直に50.0, 水平に10.0
``` 
margin: EdgeInsets.symmetric(vertical: 50.0, horizontal: 10.0),
```

左に40.0のみ
``` 
margin: EdgeInsets.only(left: 40.0)
```

上下左右全て指定する場合(Left, Top, Right, Bottom)
``` 
margin: EdgeInsets.fromLTRB(20.0, 10.0, 10.0, 20.0),
```

### Column
#### mainAxisSize
メイン軸でどれだけのスペースを占有する必要があるか。
入力されるレイアウトの制約に従って、空き領域を最大化するか最小化するかを制御する。
[MainAxisSize enum - rendering library - Dart API](https://api.flutter.dev/flutter/rendering/MainAxisSize-class.html)
最小、最大
``` 
mainAxisSize: MainAxisSize.min, // max
```

#### mainAxisAlignment
子を主軸に沿って配置する。
[mainAxisAlignment property - RenderFlex class - rendering library - Dart API](https://api.flutter.dev/flutter/rendering/RenderFlex/mainAxisAlignment.html)
均等配置
``` 
mainAxisAlignment: MainAxisAlignment.spaceEvenly
```
上寄せ, 下寄せ
``` 
mainAxisAlignment: MainAxisAlignment.top //end
```
中央
``` 
mainAxisAlignment: MainAxisAlignment.center
```

### verticalDirection
わかりづらいのでスクショつき
子を垂直にレイアウトする順序
[verticalDirection property - RenderFlex class - rendering library - Dart API](https://api.flutter.dev/flutter/rendering/RenderFlex/verticalDirection.html)

``` 
verticalDirection: VerticalDirection.up,
```

![スクリーンショット 2019-12-22 10 47 12](https://user-images.githubusercontent.com/11751495/71317835-10f9f880-24cb-11ea-8100-83b00051ccf8.png)

``` 
verticalDirection: VerticalDirection.down,
```

![スクリーンショット 2019-12-22 10 48 21](https://user-images.githubusercontent.com/11751495/71317839-23743200-24cb-11ea-9d50-a282a8c39396.png)

#### crossAxisAlignment
交差軸に沿って子を配置する方法。
[crossAxisAlignment property - RenderFlex class - rendering library - Dart API](https://api.flutter.dev/flutter/rendering/RenderFlex/crossAxisAlignment.html)

開始寄せ
``` 
crossAxisAlignment: CrossAxisAlignment.start,
```
![スクリーンショット 2019-12-22 10 51 25](https://user-images.githubusercontent.com/11751495/71317843-32f37b00-24cb-11ea-8f2a-b34a96a860e2.png)

後ろ寄せ
``` 
crossAxisAlignment: CrossAxisAlignment.end,
```

![スクリーンショット 2019-12-22 10 52 02](https://user-images.githubusercontent.com/11751495/71317848-3f77d380-24cb-11ea-97a7-9ee74451382f.png)

##### Containerに画面幅いっぱいに横に広げる
``` 
width: double.infinity,
```

``` 
children: <Widget>[
              Container(
                height: 100.0,
                width: 100.0,
                color: Colors.white,
                child: Text('Container1'),
              ),
              Container(
                width: 100.0,
                height: 100.0,
                color: Colors.blue,
                child: Text('Container 2'),
              ),
              Container(
                width: 100.0,
                height: 100.0,
                color: Colors.red,
                child: Text(‘Container 3’),
              ),
              Container(
                width: double.infinity,
                height: 10.0,
              )
            ],
```

![スクリーンショット 2019-12-22 10 55 02](https://user-images.githubusercontent.com/11751495/71317851-50c0e000-24cb-11ea-8643-4718d0ca3a54.png)

##### widthの指定をせずに親のColumnの幅に合わせて伸びるようにする
``` 
crossAxisAlignment: CrossAxisAlignment.stretch,
```

``` 
child: Column(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: <Widget>[
              Container(
                height: 100.0,
                color: Colors.white,
                child: Text('Container1'),
              ),
              Container(
                height: 100.0,
                color: Colors.blue,
                child: Text('Container 2'),
              ),
              Container(
                height: 100.0,
                color: Colors.red,
                child: Text(‘Container 3’),
              ),
            ],
          ),
```

![スクリーンショット 2019-12-22 10 58 26](https://user-images.githubusercontent.com/11751495/71317855-5c140b80-24cb-11ea-913e-3f82f179e0a2.png)

#### SizedBox
Children同士にスペースを置く

``` 
Container(
                height: 100.0,
                color: Colors.white,
                child: Text(‘Container1’),
              ),
              SizedBox(
                height: 20.0,
              ),
              Container(
                height: 100.0,
                color: Colors.blue,
                child: Text('Container 2'),
              ),
```

### Rowも基本的にはColumnと一緒
``` 
child: Row(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: <Widget>[
              Container(
                width: 30.0,
                color: Colors.white,
                child: Text('Container1'),
              ),
              SizedBox(
                width: 20.0,
              ),
              Container(
                color: Colors.blue,
                child: Text('Container 2'),
              ),
              Container(
                color: Colors.red,
                child: Text(‘Container 3’),
              ),
            ],
          ),
```

![スクリーンショット 2019-12-22 11 03 14](https://user-images.githubusercontent.com/11751495/71317862-6a622780-24cb-11ea-852c-34b5b122df8d.png)

#### 課題

![Layout-Challenge-Specs](https://user-images.githubusercontent.com/11751495/71317866-75b55300-24cb-11ea-8f53-002e6c958a8a.png)

作ったもの

![Simulator Screen Shot - iPhone 11 Pro Max - 2019-12-22 at 14 35 02](https://user-images.githubusercontent.com/11751495/71317867-78b04380-24cb-11ea-8d5b-09ba7b38fe56.png)

spaceBetweenを使わないと左右の端にマージンができてしまうので注意
``` 
mainAxisAlignment: MainAxisAlignment.spaceBetween
```

``` dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.teal,
        body: SafeArea(
          child: Row(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            children: <Widget>[
              Container(
                width: 100.0,
                color: Colors.red,
              ),
              Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: <Widget>[
                  Container(
                    width: 100.0,
                    height: 100.0,
                    color: Colors.yellow,
                  ),
                  Container(
                    width: 100.0,
                    height: 100.0,
                    color: Colors.green,
                  ),
                ],
              ),
              Container(
                width: 100.0,
                color: Colors.blue,
              ),
            ],
          ),
        ),
      ),
    );
  }
}

```
