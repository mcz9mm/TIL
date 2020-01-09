### やったこと
Flash Chat - A Lightning Fast Messaging App

- mixins
- Prepackaged Flutter Animations
- 現段階でのリファクタ

### mixins

extendsは１つまでしかできないが、mixinsはクラスを複数のクラス階層でコードを再利用できる。
mixin使うと多くの機能やプロパティを持つクラスを作成するモジュールを作成するのに使えそう

https://dart.dev/guides/language/language-tour#adding-features-to-a-class-mixins

```
 Duck().swim();
 Duck().fly();


class Duck extends Animal with CanSwim, CanFly {
  
}

mixin CanSwim {
  void swim() {
    print('Changing position by swimming');
  }
}


mixin CanFly {
  void fly() {
    print('Changing position by flying');
  }
}
```


### Prepackaged Flutter Animations
Udemyの動画内で取り上げられていたパッケージ


#### [flutter_sequence_animation](https://pub.dev/packages/flutter_sequence_animation)
複数のアニメーション可能な同じ変数をアニメーション化する

変形しながら色を変えたりとか

[DEMO](https://pub.dev/packages/flutter_sequence_animation#demo)

#### [rubber](https://pub.dev/packages/rubber)
ウィジェットやコンポーネントに適用できるアニメーションが作れる

#### [sprung](https://pub.dev/packages/sprung)
弾力のあるアニメーションを実装できる


#### [animated_text_kit](https://pub.dev/packages/animated_text_kit)
テキストアニメーション

```
TypewriterAnimatedTextKit(
  text: ['Flash Chat'],
  textStyle: TextStyle(
    fontSize: 45.0,
    fontWeight: FontWeight.w900,
  ),
),
```
![Jan-10-2020 07-20-59](https://user-images.githubusercontent.com/11751495/72110647-10db7300-337c-11ea-87d9-681b8e3c0968.gif)


### 現段階でのリファクタ

#### RoundedButton作成

```
import 'package:flutter/material.dart';

class RoundedButton extends StatelessWidget {

  RoundedButton({@required this.onPress, this.title, this.colour});

  final Function onPress;
  final String title;
  final Color colour;

  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: EdgeInsets.symmetric(vertical: 16.0),
      child: Material(
        elevation: 5.0,
        color: colour,
        borderRadius: BorderRadius.circular(30.0),
        child: MaterialButton(
          onPressed: onPress,
          minWidth: 200.0,
          height: 42.0,
          child: Text(
            title,
            style: TextStyle(
              color: Colors.white,
            ),
          ),
        ),
      ),
    );
  }
}
```
<img width="210" alt="スクリーンショット 2020-01-10 8 38 20" src="https://user-images.githubusercontent.com/11751495/72113697-9105d680-3384-11ea-947c-804b51ae7899.png">

#### TextFieldのDecoration

```
const kTextFieldDecoration = InputDecoration(
  hintText: 'Enter a value',
  contentPadding:
  EdgeInsets.symmetric(vertical: 10.0, horizontal: 20.0),
  border: OutlineInputBorder(
    borderRadius: BorderRadius.all(Radius.circular(32.0)),
  ),
  enabledBorder: OutlineInputBorder(
    borderSide:
    BorderSide(color: Colors.lightBlueAccent, width: 1.0),
    borderRadius: BorderRadius.all(Radius.circular(32.0)),
  ),
  focusedBorder: OutlineInputBorder(
    borderSide:
    BorderSide(color: Colors.lightBlueAccent, width: 2.0),
    borderRadius: BorderRadius.all(Radius.circular(32.0)),
  ),
);
```

copyWithでデフォルト値を上書き
```
decoration: kTextFieldDecoration.copyWith(hintText: 'Enter your password'),
```
<img width="210" alt="スクリーンショット 2020-01-10 8 38 40" src="https://user-images.githubusercontent.com/11751495/72113716-9d8a2f00-3384-11ea-8542-987759ac297b.png">


### Repositories
https://github.com/mcz9mm/flash-chat-flutter
