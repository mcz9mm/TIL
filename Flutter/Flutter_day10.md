### やったこと

- カードUIの作成→コンポーネント化
- コンストラクタの引数にRequireを持たせる
- ConstとFinal


### カードUIの作成→コンポーネント化

<img width="438" alt="スクリーンショット 2019-12-31 15 34 21" src="https://user-images.githubusercontent.com/11751495/71612329-0df5bb00-2be3-11ea-8932-84ed7284855b.png">

```
class InputPage extends StatefulWidget {
  @override
  _InputPageState createState() => _InputPageState();
}

class _InputPageState extends State<InputPage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('BMI CALCULATOR'),
      ),
      body: Column(
        crossAxisAlignment: CrossAxisAlignment.stretch,
        mainAxisAlignment: MainAxisAlignment.spaceEvenly,
        children: <Widget>[
          Expanded(
            child: Row(
              crossAxisAlignment: CrossAxisAlignment.stretch,
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: <Widget>[
                Expanded(
                  child: Container(
                    margin: EdgeInsets.all(15.0),
                    decoration: BoxDecoration(
                      color: Color(0xFF1D1E33),
                      borderRadius: BorderRadius.circular(10.0),
                    ),
                  ),
                ),
                Expanded(
                  child: Container(
                    margin: EdgeInsets.all(15.0),
                    decoration: BoxDecoration(
                      color: Color(0xFF1D1E33),
                      borderRadius: BorderRadius.circular(10.0),
                    ),
                  ),
                ),
              ],
            )
          ),
          Expanded(
              child: Container(
                margin: EdgeInsets.all(15.0),
                decoration: BoxDecoration(
                  color: Color(0xFF1D1E33),
                  borderRadius: BorderRadius.circular(10.0),
                ),
              ),
          ),
          Expanded(
              child: Row(
                crossAxisAlignment: CrossAxisAlignment.stretch,
                mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                children: <Widget>[
                  Expanded(
                    child: Container(
                      margin: EdgeInsets.all(15.0),
                      decoration: BoxDecoration(
                        color: Color(0xFF1D1E33),
                        borderRadius: BorderRadius.circular(10.0),
                      ),
                    ),
                  ),
                  Expanded(
                    child: Container(
                      margin: EdgeInsets.all(15.0),
                      decoration: BoxDecoration(
                        color: Color(0xFF1D1E33),
                        borderRadius: BorderRadius.circular(10.0),
                      ),
                    ),
                  ),
                ],
              )
          ),
        ],
      ),
    );
  }
}
```

#### Extract Widgetで繰り返し部分をリファクタ

1. Flutter Outlineでリファクタしたいウィジェットを選択
2. 右クリックで「Extract Widget」を選択
<img width="455" alt="スクリーンショット 2019-12-31 15 39 13" src="https://user-images.githubusercontent.com/11751495/71612436-b73cb100-2be3-11ea-9176-a9dbafc8b093.png">

Containerを別クラスにして自動生成してくれる
```
class ReusableCard extends StatelessWidget {
  const ReusableCard({
    Key key,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Container(
      margin: EdgeInsets.all(15.0),
      decoration: BoxDecoration(
        color: Color(0xFF1D1E33),
        borderRadius: BorderRadius.circular(10.0),
      ),
    );
  }
}
```

↓リファクタ後

```
body: Column(
        crossAxisAlignment: CrossAxisAlignment.stretch,
        mainAxisAlignment: MainAxisAlignment.spaceEvenly,
        children: <Widget>[
          Expanded(
            child: Row(
              crossAxisAlignment: CrossAxisAlignment.stretch,
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: <Widget>[
                Expanded(
                  child: ReusableCard(),
                ),
                Expanded(
                  child: ReusableCard(),
                ),
              ],
            )
          ),
          Expanded(
              child: ReusableCard(),
          ),
          Expanded(
              child: Row(
                crossAxisAlignment: CrossAxisAlignment.stretch,
                mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                children: <Widget>[
                  Expanded(
                    child: ReusableCard(),
                  ),
                  Expanded(
                    child: ReusableCard(),
                  ),
                ],
              )
          ),
        ],
      ),
```


### コンストラクタの引数にRequireを持たせる

必須化したい引数に@requiredをつける

```
ReusableCard({@required this.colour});
```

### ConstとFinal

```
void main() {

  const myConst = 2;
  final myFinal = 3;
  
  // Error: myConst = 3;
  // Error: myFinal = 4;
}
```

定数。一見どちらも同じようだが、微妙に違いがある。

https://dart.dev/guides/language/language-tour#final-and-const

https://qiita.com/uehaj/items/7c07f019e05a743d1022#const%E3%81%A8final%E3%81%AE%E9%81%95%E3%81%84

> If you never intend to change a variable, use final or const, either instead of var or in addition to a type. 
> A final variable can be set only once; a const variable is a compile-time constant. (Const variables are implicitly final.) 
> A final top-level or class variable is initialized the first time it’s used.

Constはコンパイル実行時に定数として設定される。
つまり、アプリ実行中に変更されるような箇所でConstは利用できない。
```
void main() {

  const myConst = 2 * 2 + 1;
  // Error const myConst = Datetime.now();
  const myFinal = Datetime.now();
}
```

### Repositories
https://github.com/mcz9mm/bmi-calculator-flutter
