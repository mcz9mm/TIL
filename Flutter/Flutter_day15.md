### やったこと
Section 13: Clima - Powering Your Flutter App with Live Weather Web Data

- 位置情報の取得
- 位置取得許可の設定
- 非同期処理について
- Widget LifeCycle


### 位置情報の取得

[geolocator](https://pub.dev/packages/geolocator)を利用する

非同期で取得する

```
  void getLocation() async {
    Position position = await Geolocator().getCurrentPosition(desiredAccuracy: LocationAccuracy.low);
    print(position);
  }
```



### 位置取得許可の設定
どちらもネイティブを触っていたので特に目新しいことはないが念のため。

#### Android
`AndroidManifest.xml`に記載

AndroidXで不具合が出る場合：https://flutter.dev/docs/development/androidx-migration

```
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```

#### iOS
`Info.plist`に記載

```
<key>NSLocationWhenInUseUsageDescription</key>
<string>This app needs access to location when open.</string>
```



### 非同期処理について

同期(1→2→3で実行される)
```
Void aFunction() {
  // 1
  print('Hello Moon!');
  // 2 時間がかかる処理
  syncLoad('image from NASA');
  // 3
  print('Hello Jupiter!');
}
```

非同期(1→3→2で実行される)
```
Void aFunction() {
  // 1
  print('Hello Moon!');
  // 3 時間がかかる処理
  syncLoad('image from NASA');
  // 2
  print('Hello Jupiter!');
}
```

#### 処理が完了したタイミングで何かを行いたい
Futureを使う
```
Duration threeSeconds = Duration(seconds: 3);
  Future.delayed(threeSeconds, (){
    String result = 'task 2 data';
    print('Task 2 complete');
  });
```

Future<String>
```
import 'dart:io';

void main() {
  performTasks();
}

void performTasks() async {
  task1();
  String task2Result = await task2();
  task3(task2Result);
}

void task1() {
  String result = 'task 1 data';
  print('Task 1 complete');
}

Future<String> task2() async {

  Duration threeSeconds = Duration(seconds: 3);

  String result;
  await Future.delayed(threeSeconds, (){
    result = 'task 2 data';
    print('Task 2 complete');
  });

  return result;
}

void task3(String task2Data) {
  String result = 'task 3 data';
  print('Task 3 complete with $task2Data');
}
```

### Widget LifeCycle

#### StatefulWidget
- initState：　オブジェクトが呼び出された時
- deactivate: オブジェクトの状態が破棄された時
- build: ビルド時（※一番呼ばれる。ウィジェットが依存していると何度も呼ばれる）

```
@override
void initState() {
  super.initState();
  // do something
}

@override
void deactivate() {
  super.deactivate();
  // do something
}

@override
Widget build(BuildContext context) {
  // do something
}
```

### 今回できたもの
起動時に位置情報を取得する
![Jan-04-2020 13-51-26](https://user-images.githubusercontent.com/11751495/71759958-566deb00-2ef9-11ea-9558-fa9eb6660e4e.gif)

### Repositories
git@github.com:mcz9mm/Clima-Flutter.git
