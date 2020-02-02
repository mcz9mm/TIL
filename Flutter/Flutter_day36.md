### やったこと
- Widgetをキャッシュして不要なrebuildを防ぐ
- レイアウト修正


### Widgetをキャッシュして不要なrebuildを防ぐ

チャート等を表示する画面でButtonのSetStateを押した際に余計なWidgetまで更新されていた。

Widget自体をプロパティにして、初回build時のみ`chartView`を生成するようにした。
```
Widget chartView;

Widget showCircleChartView() {
  if (chartView == null) {
    chartView = CircleChartView(
      models: Provider.of<MoneyData>(context, listen: false).moneys,
      goalValue: Provider.of<MoneyData>(context, listen: false).goalValue,
      size: 104.0,
    );
    return chartView;
  
    } else {
      return chartView;
    }
  }
}
```

#### 修正前

![Feb-02-2020 17-45-36](https://user-images.githubusercontent.com/11751495/73606726-d10d5180-45f0-11ea-84e3-8e1bd64f596f.gif)

#### 修正後

![Feb-02-2020 18-01-44](https://user-images.githubusercontent.com/11751495/73606815-84764600-45f1-11ea-91b3-f3078fd47277.gif)

### レイアウト修正

Flutter Inspectorを使おう

全体のレイアウトやWidgetの中身のプロパティ等を手軽にデバッグできる

<img width="500" alt="スクリーンショット 2020-02-02 19 25 58" src="https://user-images.githubusercontent.com/11751495/73606849-2302a700-45f2-11ea-97a0-0e62a739fa4f.png">
<img width="500" alt="スクリーンショット 2020-02-02 19 27 31" src="https://user-images.githubusercontent.com/11751495/73606855-36ae0d80-45f2-11ea-98e3-859e3fa07eee.png">


できあがり！
<img width="462" alt="スクリーンショット 2020-02-02 19 13 34" src="https://user-images.githubusercontent.com/11751495/73606824-b4bde480-45f1-11ea-8115-0b08fcf79e13.png">


