# Re:ゼロから始めるFlutter生活(TIL day2)
#flutter

### Container
[Container class - widgets library - Dart API](https://api.flutter.dev/flutter/widgets/Container-class.html)

### SafeArea

1. option+enter 
2. Wrap with new widget
3. widget→SafeAreaに変更

![](Re:%E3%82%BB%E3%82%99%E3%83%AD%E3%81%8B%E3%82%89%E5%A7%8B%E3%82%81%E3%82%8BFlutter%E7%94%9F%E6%B4%BB(TIL%20day2)/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202019-12-22%2010.17.51.png)

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
![](Re:%E3%82%BB%E3%82%99%E3%83%AD%E3%81%8B%E3%82%89%E5%A7%8B%E3%82%81%E3%82%8BFlutter%E7%94%9F%E6%B4%BB(TIL%20day2)/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202019-12-22%2010.47.12.png)
``` 
verticalDirection: VerticalDirection.down,
```
![](Re:%E3%82%BB%E3%82%99%E3%83%AD%E3%81%8B%E3%82%89%E5%A7%8B%E3%82%81%E3%82%8BFlutter%E7%94%9F%E6%B4%BB(TIL%20day2)/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202019-12-22%2010.48.21.png)
#### crossAxisAlignment
交差軸に沿って子を配置する方法。
[crossAxisAlignment property - RenderFlex class - rendering library - Dart API](https://api.flutter.dev/flutter/rendering/RenderFlex/crossAxisAlignment.html)

開始寄せ
``` 
crossAxisAlignment: CrossAxisAlignment.start,
```
![](Re:%E3%82%BB%E3%82%99%E3%83%AD%E3%81%8B%E3%82%89%E5%A7%8B%E3%82%81%E3%82%8BFlutter%E7%94%9F%E6%B4%BB(TIL%20day2)/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202019-12-22%2010.52.02.png)
後ろ寄せ
``` 
crossAxisAlignment: CrossAxisAlignment.end,
```
![](Re:%E3%82%BB%E3%82%99%E3%83%AD%E3%81%8B%E3%82%89%E5%A7%8B%E3%82%81%E3%82%8BFlutter%E7%94%9F%E6%B4%BB(TIL%20day2)/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202019-12-22%2010.51.25.png)
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

![](Re:%E3%82%BB%E3%82%99%E3%83%AD%E3%81%8B%E3%82%89%E5%A7%8B%E3%82%81%E3%82%8BFlutter%E7%94%9F%E6%B4%BB(TIL%20day2)/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202019-12-22%2010.55.02.png)

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

![](Re:%E3%82%BB%E3%82%99%E3%83%AD%E3%81%8B%E3%82%89%E5%A7%8B%E3%82%81%E3%82%8BFlutter%E7%94%9F%E6%B4%BB(TIL%20day2)/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202019-12-22%2010.58.26.png)

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
![](Re:%E3%82%BB%E3%82%99%E3%83%AD%E3%81%8B%E3%82%89%E5%A7%8B%E3%82%81%E3%82%8BFlutter%E7%94%9F%E6%B4%BB(TIL%20day2)/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%202019-12-22%2011.03.14.png)

#### 課題

![](Re:%E3%82%BB%E3%82%99%E3%83%AD%E3%81%8B%E3%82%89%E5%A7%8B%E3%82%81%E3%82%8BFlutter%E7%94%9F%E6%B4%BB(TIL%20day2)/Layout-Challenge-Specs.png)

作ったもの
![](Re:%E3%82%BB%E3%82%99%E3%83%AD%E3%81%8B%E3%82%89%E5%A7%8B%E3%82%81%E3%82%8BFlutter%E7%94%9F%E6%B4%BB(TIL%20day2)/Simulator%20Screen%20Shot%20-%20iPhone%2011%20Pro%20Max%20-%202019-12-22%20at%2014.35.02.png)

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
