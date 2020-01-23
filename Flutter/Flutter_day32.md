### やったこと
- flutter_datetime_pickerの導入
- datetime_picker_formfieldの導入
- DatePickerをOS毎に切り替え表示

### flutter_datetime_pickerの導入
https://pub.dev/packages/flutter_datetime_picker#-readme-tab-


READMEにほぼ載っているので引用になるが
https://pub.dev/packages/flutter_datetime_picker#usage

```
flutter_datetime_picker: ^1.3.4
```

```
import 'package:flutter_datetime_picker/flutter_datetime_picker.dart';
```

```
FlatButton(
    onPressed: () {
        DatePicker.showDatePicker(context,
                              showTitleActions: true,
                              minTime: DateTime(2018, 3, 5),
                              maxTime: DateTime(2019, 6, 7), onChanged: (date) {
                            print('change $date');
                          }, onConfirm: (date) {
                            print('confirm $date');
                          }, currentTime: DateTime.now(), locale: LocaleType.zh);
    },
    child: Text(
        'show date time picker (Chinese)',
        style: TextStyle(color: Colors.blue),
    ));
```

minTimeとmaxTimeは前後一年で表示するように修正した

```
minTime: DateTime.now().subtract(Duration(days: 365)),
maxTime: DateTime.now().add(Duration(days: 365)),
```

### datetime_picker_formfieldの導入
https://pub.dev/packages/datetime_picker_formfield#-readme-tab-

```
datetime_picker_formfield: ^1.0.0
```

```
import 'package:datetime_picker_formfield/datetime_picker_formfield.dart';
```

```
final format = DateFormat("yyyy-MM-dd");
DateTimeField(
  format: format,
  onShowPicker: (context, currentValue) {
    return showDatePicker(
      context: context,
      firstDate: DateTime(1900),
      initialDate: currentValue ?? DateTime.now(),
      lastDate: DateTime(2100));
      },
),
```

### DatePickerをOS毎に切り替え表示

```
import 'dart:io' show Platform;
```
あとはiOSかAndroidか確認するだけ

```
Platform.isIOS ? foo : hoge
```

<img width="400" alt="スクリーンショット 2020-01-23 10 39 00" src="https://user-images.githubusercontent.com/11751495/72950149-d20ed980-3dcd-11ea-9263-ad41e57d76f1.png">

