やったこと
- List
- クラスの作成
	- コンストラクタ	
- Private化
- アクションの継承
- ポリモーフィズム
- RFlutter Alertの導入
- セクション10: Quizzler -Modularising & Organising Flutter Code

### List
``` 
List<Icon> scoreKeeper = [
  Icon(
    Icons.check,
    color: Colors.green,
  ),
  Icon(
    Icons.close,
    color: Colors.red,
  ),
  Icon(
    Icons.close,
    color: Colors.red,
  ),
];

// Add
scoreKeeper.add(
  Icon(
    Icons.check,
    color: Colors.green,
  ),
);


// ===========
List<String> = ['a', 'b', 'c']
```

### クラスの作成

#### コンストラクタ

``` dart
class Question {

  String questionText;
  bool questionAnswer;

  Question({String q, bool a}) {
    questionText = q;
    questionAnswer = a;
  }
	//これでも可能
	//Question({this.questionText, this.questionAnswer})
}
```

別クラスで利用したい
```
import 'question.dart';

Question q1 = Question(q: 'You can lead a cow down stairs but not up stairs.',a: false);

List<Question> questionBank = [
  Question(q: 'You can lead a cow down stairs but not up stairs.', a: false),
  Question(q: 'Approximately one quarter of human bones are in the feet.', a: true),
  Question(q: 'A slug\'s blood is green.', a: true),
];

```

### Private化
_ アンダーバーをつけるだけ
```
List<Question> _questionBank = [
  Question('You can lead a cow down stairs but not up stairs.', false),
  Question('Approximately one quarter of human bones are in the feet.', true),
  Question('A slug\'s blood is green.', true),
  Question('Buzz Aldrin\'s mother\'s maiden name was \"Moon\".', true),
  Question('It is illegal to pee in the Ocean in Portugal.', true),
];

```

### アクションの継承

```
void main() {
	// Car myNormalCar = Car();
	// print(myNormalCar.numberOfSeat);
	// myNormalCar.drive();

	ElectricCar myTesla = ElectricCar();
	myTesla.drive();
	myTesla.recharge();
}

class Car {
	int numberOfSeat = 5;
	
	void drive() {
		print('wheels turn.');
	}
}

class ElectricCar extends Car {
	int batteryLevel = 100;
	
	void recharge() {
		batteryLevel = 100;
	}
}

```

### ポリモーフィズム

``` 
void main() {
  LevitatingCar myMagLev = LevitatingCar();
  myMagLev.drive();
}

class Car {
	int numberOfSeat = 5;
	
	void drive() {
		print('wheels turn.');
	}
}

class LevitatingCar extends Car {
  
  @override
  void drive() {
		print('glide forwards');
	}
  
}
```

#### super

``` dart
void main() {

  SelfDrivingCar myWaymo = SelfDrivingCar(‘1 Hacker Way’);
  myWaymo.drive();
// wheels turn.
// steering towards 1 Hacker Way
  
}

class Car {
	int numberOfSeat = 5;
	
	void drive() {
		print(‘wheels turn.’);
	}
}

class SelfDrivingCar extends Car {
  
  String destination;
  
  SelfDrivingCar(String userSetDestination) {
    destination = userSetDestination;
  }
  
  @override
  void drive() {
    super.drive();
    
    print('steering towards $destination');
  }
  
}
```


### RFlutter Alertの導入
[rflutter_alert | Flutter Package](https://pub.dev/packages/rflutter_alert)

``` 
Alert(
          context: context,
          title: ‘Finished!’,
          desc: ‘You\’ve reached the end of the quiz.’,
        ).show();
```
### セクション10: Quizzler -Modularising & Organising Flutter Code
![Dec-27-2019 19-22-32](https://user-images.githubusercontent.com/11751495/71513767-23b36980-28df-11ea-82bf-1afab3cb3029.gif)

[GitHub - mcz9mm/quizzler-flutter: Learn to Code While Building Apps - The Complete Flutter Development Bootcamp](https://github.com/mcz9mm/quizzler-flutter)

[GitHub - mcz9mm/quizzler-flutter-challenge-starting: Starter code for the Quizzler Challenge from the Complete Flutter Development Bootcamp](https://github.com/mcz9mm/quizzler-flutter-challenge-starting)

