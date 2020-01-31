### やったこと
- showModalBottomSheetの部分だけ表示・非表示のたびに何度もrebuildされる件
- bezier_chartの導入


### showModalBottomSheetの部分だけ表示・非表示のたびに何度もrebuildされる件

各Widgetのbuild時にdebugPrintを差し込んでパフォーマンス調査した。

こんな感じに
```
@override
  Widget build(BuildContext context) {
    debugPrint('MoneysPage build');
```

すると、、
```
flutter: AddMoneyPage build
flutter: MoneysPage build
flutter: CircleChart build
flutter: AddMoneyPage build
flutter: AddMoneyPage build
flutter: AddMoneyPage build
flutter: AddMoneyPage build
flutter: AddMoneyPage build
flutter: AddMoneyPage build
flutter: AddMoneyPage build
flutter: AddMoneyPage build
```

めっちゃ呼ばれてる、、、

showModalBottomSheetの部分だった。
```
floatingActionButton: FloatingActionButton(
        onPressed: () {
          showModalBottomSheet(
            context: context,
            builder: (context) => AddMoneyPage(),
          );
        },
```

調べてみるとベストアンサーにこんなことが、

https://teratail.com/questions/215572

> 動かしてみると、ボトムシートの開閉時にリビルドされています。
> コードをちらっと見てみると内部では AnimatedBuilder が使われており、
> _ModalBottomSheetLayoutがアニメーションが進むと位置が変更されるので、
> リビルドしているようです。そして、それを避けるオプションなどは用意されていないように見えます。

[コードはこちら](https://github.com/flutter/flutter/blob/v1.9.1%2Bhotfix.4/packages/flutter/lib/src/material/bottom_sheet.dart#L214-L241)

issueにも挙げられてたし、クローズされているのでこれは意図どおりらしい、
https://github.com/flutter/flutter/issues/27847


とにかくProvider使ってるし、パフォーマンスには今後も気を付けたい所存

### bezier_chart

https://pub.dev/packages/bezier_chart

#### いつも通りの導入から
```
dependencies:
  bezier_chart: ^1.0.16
```

```
$ flutter pub get
```

```
import 'package:bezier_chart/bezier_chart.dart';
```

#### 実装（とりあえず表示まで）

```
class LineChart extends StatelessWidget {
  final fromDate = DateTime.now().subtract(Duration(days: 7));
  final toDate = DateTime.now();

  final date1 = DateTime.now().subtract(Duration(days: 2));
  final date2 = DateTime.now().subtract(Duration(days: 3));
  final date3 = DateTime.now().subtract(Duration(days: 4));
  final date4 = DateTime.now().subtract(Duration(days: 5));
  final date5 = DateTime.now().subtract(Duration(days: 6));
  final date6 = DateTime.now().subtract(Duration(days: 7));

  @override
  Widget build(BuildContext context) {
    debugPrint('LineChart build');
    return Container(
      child: Center(
        child: Container(
          height: MediaQuery.of(context).size.height / 3,
          width: MediaQuery.of(context).size.width,
          child: BezierChart(
            fromDate: fromDate,
            bezierChartScale: BezierChartScale.WEEKLY,
            toDate: toDate,
            selectedDate: toDate,
            series: [
              BezierLine(
                label: "Duty",
                onMissingValue: (dateTime) {
                  if (dateTime.day.isEven) {
                    return 10.0;
                  }
                  return 5.0;
                },
                data: [
                  DataPoint<DateTime>(value: 10, xAxis: date1),
                  DataPoint<DateTime>(value: 50, xAxis: date2),
                  DataPoint<DateTime>(value: 20, xAxis: date3),
                  DataPoint<DateTime>(value: 30, xAxis: date4),
                  DataPoint<DateTime>(value: 20, xAxis: date5),
                  DataPoint<DateTime>(value: 10, xAxis: date6),
                ],
              ),
            ],
            config: BezierChartConfig(
              displayYAxis: true,
              verticalIndicatorStrokeWidth: 3.0,
              verticalIndicatorColor: Colors.white,
              showVerticalIndicator: true,
              verticalIndicatorFixedPosition: false,
              backgroundColor: kPrimaryColor,
              footerHeight: 30.0,
            ),
          ),
        ),
      ),
    );
  }
}
```

![Jan-31-2020 09-08-15](https://user-images.githubusercontent.com/11751495/73501482-69e17880-4409-11ea-9b26-791f8c1f4a03.gif)

実際まだサンプルデータで表示しただけ。

あと、x軸が長いと横スクロールしてしまうのでそれをさせないようにしたい。


