### やったこと
- fab_circular_menuを使う
- TextFieldの入力を数値のみ受け入れる
- TextFieldのInputDecoration
- showModalBottomSheetのheightを変更する

### fab_circular_menuを使う
https://pub.dev/packages/fab_circular_menu#-readme-tab-

```
floatingActionButton: FabCircularMenu(
        ringDiameter: 150.0,
        ringColor: kFloatingButtonColor,
        fabColor: kFloatingButtonColor,
        child: Container(
          color: Color(0x00000000),
        ),
          options: <Widget>[
            IconButton(
              color: Colors.white,
              icon: Icon(Icons.add), onPressed: () {
                print('onPressed');
            }),
            IconButton(
              color: Colors.white,
              icon: Icon(Icons.data_usage), onPressed: () {
                print('onPressed');
            }),
          ],
      ),
```

![Jan-19-2020 22-21-49](https://user-images.githubusercontent.com/11751495/72681774-300b9a80-3b0a-11ea-907b-3d54703b312b.gif)

### TextFieldの入力を数値のみ受け入れる
https://api.flutter.dev/flutter/services/TextInputFormatter-class.html

```
TextField(
  keyboardType: TextInputType.number,
  inputFormatters: [
    WhitelistingTextInputFormatter.digitsOnly
  ],
  onChanged: (newValue) {
    // こいつはintにパースする必要ありそう
    newMoneyValue = int.parse(newValue);
  },
```

![Jan-19-2020 22-09-19](https://user-images.githubusercontent.com/11751495/72681594-75c76380-3b08-11ea-9519-59111ad40017.gif)


### TextFieldのInputDecoration
https://api.flutter.dev/flutter/material/InputDecoration-class.html

```
TextFormField(
  decoration: InputDecoration(
    labelText: 'Enter your username'
  ),
);
```

![スクリーンショット 2020-01-19 22 09 49](https://user-images.githubusercontent.com/11751495/72681592-719b4600-3b08-11ea-95f9-cef46b6c2ac6.png)


### showModalBottomSheetのheightを変更する

この辺で議論されていた。↓↓

https://github.com/flutter/flutter/issues/32747

やり方はいくつかあるみたいだが`FractionallySizedBox`を利用してみた。

https://api.flutter.dev/flutter/widgets/FractionallySizedBox-class.html

> A widget that sizes its child to a fraction of the total available space. 

```
showModalBottomSheet(
  context: context,
  isScrollControlled: true,
  builder: (context) {
    return FractionallySizedBox(
      heightFactor: 0.7,
      child: AddMoneyPage(),
    );
});
```

![Jan-19-2020 22-17-43](https://user-images.githubusercontent.com/11751495/72681707-8af0c200-3b09-11ea-840a-1b352f7b469f.gif)

