### やったこと
- Spinnerを利用してローディングの表示
- 気象情報を受け取ってUI更新
- TextFieldの設定
- ナビゲーションで戻る際にデータを渡す


### Spinnerを利用してローディングの表示

https://pub.dev/packages/flutter_spinkit

![Jan-05-2020 16-39-01](https://user-images.githubusercontent.com/11751495/71776766-f9963180-2fd9-11ea-94e7-6bd62c475558.gif)


```
Widget build(BuildContext context) {
    return Scaffold(body:
    Center(
      child: SpinKitDoubleBounce(
        color: Colors.white,
        size: 100.0,
        ),
      ),
    );
  }
```

![Jan-05-2020 16-45-03](https://user-images.githubusercontent.com/11751495/71776811-c3a57d00-2fda-11ea-9d60-47f4b506dab2.gif)


### 気象情報を受け取ってUI更新

initState内で「widget」を使えば内部メソッドを呼び出せる

```
class _LocationScreenState extends State<LocationScreen> {

  WeatherModel weather = WeatherModel();

  int temperature;
  String weatherIcon;
  String message;
  String cityName;


  @override
  void initState() {
    super.initState();

    updateUI(widget.locationWeather);
  }
```

<img width="405" alt="スクリーンショット 2020-01-05 17 42 06" src="https://user-images.githubusercontent.com/11751495/71777398-b3919b80-2fe2-11ea-8f9b-14de68c2e173.png">

### TextFieldの設定

```
child: TextField(
  style: TextStyle(
    color: Colors.black,
  ),
  decoration: kTextFieldInputDecoration,
  onChanged: (changedValue) {
    print(changedValue);
  },
),
```


``` constants.dart
const kTextFieldInputDecoration = InputDecoration(
  filled: true,
  fillColor: Colors.white,
  icon: Icon(
    Icons.location_city,
    color: Colors.white,
  ),
  hintText: 'Enter City Name',
  hintStyle: TextStyle(
    color: Colors.grey,
  ),
  border: OutlineInputBorder(
    borderRadius: BorderRadius.all(
        Radius.circular(10)
    ),
    borderSide: BorderSide.none,
  ),
);
```

![Jan-05-2020 18-15-44](https://user-images.githubusercontent.com/11751495/71777736-72e85100-2fe7-11ea-877e-58f755cd06fa.gif)


### ナビゲーションで戻る際にデータを渡す

Navigatorのpopにはcontextの他に、オプションでデータを付与することができる。
```
  @optionalTypeArgs
  static bool pop<T extends Object>(BuildContext context, [ T result ]) {
    return Navigator.of(context).pop<T>(result);
  }
```

NavigatorのpushにはFuture<T>を返すことができる
```
  @optionalTypeArgs
  static Future<T> push<T extends Object>(BuildContext context, Route<T> route) {
    return Navigator.of(context).push(route);
  }
```

```
// push: 受け取る処理
var typedName = await Navigator.push(context, MaterialPageRoute(builder: (context) {
  return CityScreen();
}));
print(typedName);
if (typedName != null) {
   var weatherData = await weather.getCityWeather(typedName);
   updateUI(weatherData);
}

// pop:戻る処理
Navigator.pop(context, cityName);
```


![Jan-05-2020 19-14-55](https://user-images.githubusercontent.com/11751495/71778326-c6f73380-2fef-11ea-8482-3de633fa5ca6.gif)

### Repositories
https://github.com/mcz9mm/Clima-Flutter

