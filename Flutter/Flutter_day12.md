
### やったこと
- Functions as First Order Objects
- Constants
- Slider Widget
- Slider ThemeData

### Functions as First Order Objects


```
void main() {

  int result = calculator(3, 2, multiply);
  print(result); // 6
  
}

int calculator(int n1, int n2, Function calculation) {
  return calculation(n1, n2);
}

int add(int n1, int n2) {
  return n1 + n2;
}

int multiply(int n1, int n2) {
  return n1 * n2;
}
```


Functionを変数化することも可能
```
Function calculator = (int n1, int n2, Function calculation) {
  return calculation(n1, n2);
};
```

```
void main() {

  Car myCar = Car(drive: slowDrive);
  myCar.drive(); //slowDrive
  myCar.drive = fastDrive;
  myCar.drive(); //fastDrive
}

class Car {
  
  Car({this.drive});
    
  Function drive;  
}

void slowDrive() {
  print('slowDrive');
}

void fastDrive() {
  print('fastDrive');
}
```

#### ReusableCardに関数を受け取るように修正

```
class ReusableCard extends StatelessWidget {

  ReusableCard({@required this.colour, this.cardChild, this.onPress});

  final Color colour;
  final Widget cardChild;
  final Function onPress;

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: onPress,
      child: Container(
        child: cardChild,
        margin: EdgeInsets.all(15.0),
        decoration: BoxDecoration(
          color: colour,
          borderRadius: BorderRadius.circular(10.0),
        ),
      ),
    );
  }
}
```

GestureDetector内にReusableCardを入れていたものをReusableCard内で行うように修正。
onPressの処理をコンストラクタに設定。
```
Expanded(
                  child: ReusableCard(
                    onPress: () {
                      setState(() {
                        selectedGender = Gender.male;
                      });
                    },
                    colour: selectedGender == Gender.male ? activeCardColor : inactiveCardColor,
                    cardChild: IconContent(
                      iconData: FontAwesomeIcons.mars,
                      iconText: 'MALE',
                    ),
                  ),
                ),
```


### Constants
プロジェクト全体で利用するconstantsの定数にはkを前置詞に置くと便利

<img width="372" alt="スクリーンショット 2020-01-01 14 20 06" src="https://user-images.githubusercontent.com/11751495/71638377-d3068c80-2ca1-11ea-8a14-1142c435f6c8.png">

```
import 'package:flutter/material.dart';

const kLabelTextStyle = TextStyle(
  fontSize: 18.0,
  color: Color(0xFF8D8E98),
);

const kBottomContainerHeight = 80.0;
const kActiveCardColor =  Color(0xFF1D1E33);
const kInactiveCardColor =  Color(0xFF111328);
const kBottomContainerColor = Color(0xFFEB1555);
```


### Slider Widget
https://api.flutter.dev/flutter/material/Slider-class.html

![Jan-01-2020 14-47-22](https://user-images.githubusercontent.com/11751495/71638529-b0767280-2ca5-11ea-99ab-82943ed38ad1.gif)

```
Slider(
  value: height.toDouble(),
  min: 120.0,
  max: 220.0,
  activeColor: Color(0xFFEB1555),
  inactiveColor: Color(0xFF8D8E98),
  onChanged: (double newValue) {
    print(newValue);
    setState(() {
      height = newValue.round();
    });
  },
),
```

### Slider ThemeData

![Jan-01-2020 15-17-47](https://user-images.githubusercontent.com/11751495/71638677-e74e8780-2ca9-11ea-832b-430554005283.gif)

https://api.flutter.dev/flutter/material/SliderThemeData-class.html

```
SliderTheme(
  data: SliderTheme.of(context).copyWith(
    activeTrackColor: Colors.white,
    inactiveTrackColor: Color(0xFF8D8E98),
    overlayColor: Color(0x29EB1555),
    thumbColor: Color(0xFFEB1555),
    thumbShape: RoundSliderThumbShape(enabledThumbRadius: 15.0),
    overlayShape: RoundSliderOverlayShape(overlayRadius: 30.0),
  ),
  child: Slider(
    value: height.toDouble(),
    min: 120.0,
    max: 220.0,
    onChanged: (double newValue) {
      print(newValue);
      setState(() {
        height = newValue.round();
      });
    },
  ),
),
```

#### アプリ全体で使う場合

```
class BMICalculator extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData.dark().copyWith(
        sliderTheme: SliderTheme.of(context).copyWith(
          activeTrackColor: Colors.white,
          inactiveTrackColor: Color(0xFF8D8E98),
          overlayColor: Color(0x29EB1555),
          thumbColor: Color(0xFFEB1555),
          thumbShape: RoundSliderThumbShape(enabledThumbRadius: 15.0),
          overlayShape: RoundSliderOverlayShape(overlayRadius: 30.0),
        ),
        primaryColor: Color(0xFF0A0E21),
        scaffoldBackgroundColor: Color(0xFF0A0E21),
      ),
      home: InputPage(),
    );
  }
}
```

### Repositories
https://github.com/mcz9mm/bmi-calculator-flutter
