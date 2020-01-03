### やったこと
- Map
- 結果画面のデザイン
- BMIの計算
- 結果画面にデータを渡す


### Map

```
Map<String, int> phoneBook = {
  'Kyle': 12719713,
  'Amy': 11220333,
  'Tim': 93232842,
  'Kaoru': 7389371,
};

void main() {

  // 7389371
  print(phoneBook['Kaoru']);
  // null
  print(phoneBook['Hoge']);
  phoneBook['Kaoru'] = 11111;
  // 11111
  print(phoneBook['Kaoru']);
  // (12719713, 11220333, 93232842, 11111)
  print(phoneBook.values);
  // (Kyle, Amy, Tim, Kaoru)
  print(phoneBook.keys);
}

```


### 結果画面のデザイン
<img width="200" alt="スクリーンショット 2020-01-02 2 10 31" src="https://user-images.githubusercontent.com/11751495/71644026-17774400-2d05-11ea-9eb0-5ac25c8a708a.png">

```
import 'package:bmi_calculator/constants.dart';
import 'package:flutter/material.dart';
import 'package:bmi_calculator/components/reusable_card.dart';
import 'package:bmi_calculator/components/bottom_button.dart';

class ResultsPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('BMI CALCULATOR'),
      ),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.spaceEvenly,
        crossAxisAlignment: CrossAxisAlignment.stretch,
        children: <Widget>[
          Expanded(
            child: Container(
              padding: EdgeInsets.all(15.0),
              alignment: Alignment.bottomLeft,
              child: Text(
                'Your Result',
                style: kTitleTextStyle,
              ),
            ),
          ),
          Expanded(
            flex: 5,
            child: ReusableCard(
              colour: kActiveCardColor,
              cardChild: Column(
                mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                crossAxisAlignment: CrossAxisAlignment.center,
                children: <Widget>[
                  Text(
                    'Normal',
                    style: kResultTextStyle,
                  ),
                  Text(
                    '18.3',
                    style: kBMITextStyle,
                  ),
                  Text(
                    'Your BMI result is quite low, you should eat more!',
                    style: kBodyTextStyle,
                    textAlign: TextAlign.center,
                  ),
                ],
              ),
            ),
          ),
          BottomButton(
            buttonTitle: 'RE-CALCULATE',
            onTap: () {
              Navigator.pop(context);
            },
          )
        ],
      ),
    );
  }
}
```


### BMIの計算

```
import 'dart:math';

class CalculatorBrain {

  CalculatorBrain({this.height, this.weight});

  final int height;
  final int weight;

  double _bmi;

  String calculateBMI() {
    _bmi = weight / pow(height/100, 2);
    return _bmi.toStringAsFixed(1);
  }

  String getResult() {
    if (_bmi >= 25) {
      return 'Overweight';
    } else if (_bmi > 18.5) {
      return 'Normal';
    } else {
      return 'Underweight';
    }
  }

  String getInterpretation() {
    if (_bmi >= 25) {
      return 'You have a higer than normal body weight. Try to exercise more.';
    } else if (_bmi > 18.5) {
      return 'You have a nomal body weight. Good job!';
    } else {
      return 'You have a lower than normal body weight. You can eat a bit more.';
    }
  }
}
```


### 結果画面にデータを渡す

ResultsPageに値渡し

```
class ResultsPage extends StatelessWidget {

  ResultsPage({@required this.bmiResult, @required this.resultText, @resultText this.interpretation});

  final String bmiResult;
  final String resultText;
  final String interpretation;
```

```
CalculatorBrain calc = CalculatorBrain(height: height, weight: weight);
              Navigator.push(context, MaterialPageRoute(builder: (context) {
                return ResultsPage(
                  bmiResult: calc.calculateBMI(),
                  resultText: calc.getResult(),
                  interpretation: calc.getInterpretation(),
                );
              }));

```

### できたもの

<img width="200" alt="スクリーンショット 2020-01-03 15 03 01" src="https://user-images.githubusercontent.com/11751495/71709413-46430680-2e3a-11ea-9741-28262b505d33.png">
<img width="200" alt="スクリーンショット 2020-01-03 15 03 14" src="https://user-images.githubusercontent.com/11751495/71709414-46db9d00-2e3a-11ea-9aeb-8f118ac35706.png">
<img width="200" alt="スクリーンショット 2020-01-03 15 02 48" src="https://user-images.githubusercontent.com/11751495/71709416-46db9d00-2e3a-11ea-9746-5cd4f10ba6ba.png">


![Jan-03-2020 15-09-50](https://user-images.githubusercontent.com/11751495/71709543-206a3180-2e3b-11ea-804e-6ae0cf9dc2ec.gif)


### Repositories

https://github.com/mcz9mm/bmi-calculator-flutter
