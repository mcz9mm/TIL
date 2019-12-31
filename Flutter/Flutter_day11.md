### やったこと

CardViewにコンテンツをいれて、ボタン化する

- CustomWidgetの作成
- GestureDetectorの追加
- Enum

### CustomWidgetの作成
[前回](https://github.com/mcz9mm/TIL/blob/master/Flutter/Flutter_day10.md)作成したReusableCardの中にコンテンツを追加する

<img width="273" alt="スクリーンショット 2019-12-31 22 02 31" src="https://user-images.githubusercontent.com/11751495/71622468-40baa600-2c19-11ea-84cf-3d5e8852bfef.png">


#### ReusableCardにcardChildを追加
```
class ReusableCard extends StatelessWidget {

  ReusableCard({@required this.colour, this.cardChild});

  final Color colour;
  final Widget cardChild;

  @override
  Widget build(BuildContext context) {
    return Container(
      child: cardChild,
      margin: EdgeInsets.all(15.0),
      decoration: BoxDecoration(
        color: colour,
        borderRadius: BorderRadius.circular(10.0),
      ),
    );
  }
}
```

#### IconContentの作成、追加

```
class IconContent extends StatelessWidget {

  IconContent({@required this.iconData, @required this.iconText});

  final IconData iconData;
  final String iconText;

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        Icon(
          iconData,
          size: 80.0,
        ),
        SizedBox(
          height: 15.0,
        ),
        Text(
          iconText,
          style: TextStyle(
            fontSize: 18.0,
            color: Color(0xFF8D8E98),
          ),
        )
      ],
    );
  }
}
```


#### 完成

```
Expanded(
            child: Row(
              crossAxisAlignment: CrossAxisAlignment.stretch,
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: <Widget>[
                Expanded(
                  child: ReusableCard(
                    colour: activeCardColor,
                    cardChild: IconContent(
                      iconData: FontAwesomeIcons.mars,
                      iconText: 'MALE',
                    ),
                  ),
                ),
                Expanded(
                  child: ReusableCard(
                    colour: activeCardColor,
                    cardChild: IconContent(
                      iconData: FontAwesomeIcons.venus,
                      iconText: 'FEMALE',
                    ),
                  ),
                ),
              ],
            )
          ),
```


### GestureDetectorの追加
タップをはじめ、長押しやドラッグ、強制押しなども可能

https://api.flutter.dev/flutter/widgets/GestureDetector-class.html

```
child: GestureDetector(
                    onTap: () {
                      print('Pressed')
                    },
                    child: ReusableCard(
                      colour: activeCardColor,
                      cardChild: IconContent(
                        iconData: FontAwesomeIcons.mars,
                        iconText: 'MALE',
                      ),
                    ),
                  ),
```


### Enum

```
enum Gender {
  male,
  female,
}
```

### できたもの

![Jan-01-2020 00-18-37](https://user-images.githubusercontent.com/11751495/71625648-4b326b00-2c2c-11ea-9c81-289ad6fc69a6.gif)


### Repositories
https://github.com/mcz9mm/bmi-calculator-flutter
