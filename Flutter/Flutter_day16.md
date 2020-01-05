### やったこと

- Exception Handling
- Null Aware Operators
- Location取得クラスを分離して位置情報を取得する
- Networking in Flutter Apps with the HTTP Package


### Exception Handling

try, cathch

```
try {
 double myStringAsADouble = double.parse('abc');
 print(myStringAsADouble + 5);
}
catch (e) {
  // FormatException: Invalid double abc
  print(e);
}
```

Example
```
@override
  Widget build(BuildContext context) {
    String myMargin = 'abc';
    double myMarginAsADouble;

    try {
      myMarginAsADouble = double.parse(myMargin);
    }
    catch (e) {
      print(e);
      myMarginAsADouble = 30;
    }

    return Scaffold(
      body: Container(
        margin: EdgeInsets.all(myMarginAsADouble),
        color: Colors.red,
      ),
    );
  }
```

これでも同様
```
EdgeInsets.all(myMarginAsADouble ?? 30.0),
```


### Null Aware Operators

throw

```
void getLocation() async {
    try {
      somethingThatExpectLessThan10(12);
//      Position position = await Geolocator().getCurrentPosition(
//          desiredAccuracy: LocationAccuracy.low);
//      print(position);
    }
    catch (e) {
      print(e);
    }
  }

  void somethingThatExpectLessThan10(int n) {
    if (n > 10) {
      throw 'n is grater than10, n should always be less than 10.';
    }
  }
```

### Location取得クラスを分離して位置情報を取得する


``` Location.dart
import 'package:geolocator/geolocator.dart';

class Location {

  double latitude;
  double longitude;


  Future<void> getCurrentLocation() async {
    try {
      Position position = await Geolocator().getCurrentPosition(
          desiredAccuracy: LocationAccuracy.low);

      latitude = position.latitude;
      longitude = position.longitude;
    }
    catch (e) {
      print(e);
    }
  }
}
```

利用部分
```
  void getLocation() async {
    Location location = Location();
    await location.getCurrentLocation();
    print(location.latitude); // 37.785834
    print(location.longitude); // -122.406417
  }
```

### Networking in Flutter Apps with the HTTP Package
https://flutter.dev/docs/cookbook/networking/fetch-data

https://pub.dev/packages/http

APIは下記のものを利用する(実際のデータを取得するのであればユーザー登録が必要)

https://openweathermap.org/current
```
// パッケージ名に名前をつける
import 'package:http/http.dart' as http;

// getだと他でも使用しており「http.」をつけることで可読性を上げる
void getData() async {
    http.Response response = await http.get('https://samples.openweathermap.org/data/2.5/weather?lat=35&lon=139&appid=b6907d289e10d714a6e88b30761fae22');
    print(response.body);
    if (response.statusCode == 200) {
      String data = response.body;
    } else {
      print(response.statusCode);
    }
  }
```

### JSONフォーマットに変換する

[JSON Viewer Awesome](https://chrome.google.com/webstore/detail/json-viewer-awesome/iemadiahhbebdklepanmkjenfdebfpfe)が便利だった。

![Jan-05-2020 12-24-28](https://user-images.githubusercontent.com/11751495/71774735-57655200-2fb7-11ea-99cf-65c335352968.gif)

```
import 'dart:convert';

String data = response.body;
print(data);
var longitude = jsonDecode(data)['coord']['lon'];
print(longitude); //139.01
var id = jsonDecode(data)['weather'][0]['id'];
var temp = jsonDecode(data)['main']['temp'];
var name = jsonDecode(data)['name'];
print('$id, $temp, $name');
```

decodeされたdataはdynamicなのでvar,もしくは型を確認してつけてあげる
```
// dynamic type
var decodesData = jsonDecode(data);
int condition = jsonDecode(data)['weather'][0]['id'];
ouble temperature = jsonDecode(data)['main']['temp'];
String cityName = jsonDecode(data)['name'];
print('$condition, $temperature, $cityName');
```


### Repositories
https://github.com/mcz9mm/Clima-Flutter

