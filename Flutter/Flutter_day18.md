### やったこと
Bitcoin Ticker - A Simple Cryptocurrency Price Tracker

- DropdownButton
- Cupertino Widgets(iOS-style) 
- iOS用のPicker
- Android用のPicker
- OS毎に表示を切り替える

### DropdownButton

https://api.flutter.dev/flutter/material/DropdownButton-class.html

選択肢が少ない場合ならこれでも良い。

```
child: DropdownButton<String>(
  value: selectedCurrency,
  items: [
    DropdownMenuItem(
      child: Text('USD'),
      value: 'USD',),
    DropdownMenuItem(
      child: Text('EUR'),
      value: 'EUR',),
    DropdownMenuItem(
      child: Text('GBP'),
      value: 'GBP',),
  ],
  onChanged: (value) {
    print(value);
    setState(() {
      selectedCurrency = value;
    });
  },
),
```

![Jan-06-2020 08-38-29](https://user-images.githubusercontent.com/11751495/71787852-f5145c00-305f-11ea-8a97-75953a9de362.gif)


#### 選択肢が多い場合
List<DropdownMenuItem>を返すメソッドを作成する。

`List<DropdownMenuItem<String>>`の`<String>`がないとdynamicの型になって
怒られるので注意。

```
List<DropdownMenuItem> getDropdownItems() {
  List<DropdownMenuItem<String>> dropdownItems = [];

  for (String currency in currenciesList) {
    var newItem = DropdownMenuItem(
      child: Text(currency),
      value: currency,
    );

    dropdownItems.add(newItem)
  }
  
  return dropdownItems;
}
```

### Cupertino Widget
https://flutter.dev/docs/development/ui/widgets/cupertino

```
import 'package:flutter/cupertino.dart';

List<Widget> getPickerItems() {

  List<Text> pickerItems = [];
  
  for (String currency in currenciesList) {

    pickerItems.add(Text(currency));
  }

  return pickerItems;
 }

child: CupertinoPicker(
  backgroundColor: Colors.lightBlue,
  itemExtent: 32.0,
  onSelectedItemChanged: (selectedIndex) {
    print(selectedIndex);
  },
  children: getPickerItems(),
),
```


### iOS用のPicker

```
CupertinoPicker iOSPicker() {

    List<Text> pickerItems = [];

    for (String currency in currenciesList) {

      pickerItems.add(Text(currency));
    }

    return CupertinoPicker(
      backgroundColor: Colors.lightBlue,
      itemExtent: 32.0,
      onSelectedItemChanged: (selectedIndex) {
        print(selectedIndex);
      },
      children: pickerItems,
    );
  }
```

<img width="351" alt="スクリーンショット 2020-01-06 22 25 26" src="https://user-images.githubusercontent.com/11751495/71820752-71945280-30d3-11ea-83a1-e99a6aa91bc9.png">


### Android用のPicker

```
DropdownButton<String> androidDropdown() {

    List<DropdownMenuItem<String>> dropdownItems = [];

    for (String currency in currenciesList) {
      var newItem = DropdownMenuItem(
        child: Text(currency),
        value: currency,
      );

      dropdownItems.add(newItem);
    }

    return DropdownButton<String>(
      value: selectedCurrency,
      items: dropdownItems,
      onChanged: (value) {
        print(value);
        setState(() {
          selectedCurrency = value;
        });
      },
    );
  }
```
<img width="351" alt="スクリーンショット 2020-01-06 22 27 02" src="https://user-images.githubusercontent.com/11751495/71820808-abfdef80-30d3-11ea-8485-37dbf8e06fee.png">

### OS毎に表示を切り替える

```
// dart:ioの中身のPlatformだけimport
import 'dart:io' show Platform;

if (Platform.isIOS) {
  // iOS
} else if (Platform.isAndroid) {
  // Android
}
```

### Repositories
https://github.com/mcz9mm/bitcoin-ticker-flutter

