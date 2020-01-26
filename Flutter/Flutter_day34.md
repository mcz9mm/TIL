### やったこと
- お金を回す！！(Rotateアニメーション)
- StatusBarのColor周り
- flutter_circular_chartでチャート表示

### お金を回す！！(アニメーション)

```
class _MoneysPageState extends State<MoneysPage> with SingleTickerProviderStateMixin {

AnimationController _controller;

@override
  void initState() {
  super.initState();
  _controller = AnimationController(
      duration: const Duration(milliseconds: 10000),
      vsync: this,
    );
    _controller.forward();
    _controller.repeat();
}
```

disposeも忘れずに
```
@override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }
```

お金を回す
```
RotationTransition(
  turns: Tween(begin: 0.0, end: 1.0).animate(_controller),
  child: Icon(
    Icons.monetization_on,
    color: Colors.white,
    ),
 ),
```

![Jan-26-2020 21-19-45](https://user-images.githubusercontent.com/11751495/73135069-a61b7e80-4081-11ea-922b-453f1f2d4ece.gif)

### StatusBarのColor周り

```
Widget build(BuildContext context) {
  SystemChrome.setSystemUIOverlayStyle(SystemUiOverlayStyle.dark.copyWith(
    statusBarColor: Colors.white, // android
    statusBarBrightness: Brightness.light// iOS
  ));
return Scaffold(
  appBar: PreferredSize(child: AppBar(
    backgroundColor: Colors.red,
    elevation: 0.0,
  ),
```

<img width="300" alt="スクリーンショット 2020-01-26 15 56 54" src="https://user-images.githubusercontent.com/11751495/73135091-ea0e8380-4081-11ea-9f0c-5b96a4a81e14.png">


今回はAppBarの高さは必要なかった＋カラーも不要なので透明にした。
```
@override
  Widget build(BuildContext context) {
    SystemChrome.setSystemUIOverlayStyle(SystemUiOverlayStyle.dark.copyWith(
        statusBarColor: Colors.white, // android
        statusBarBrightness: Brightness.light// iOS
    ));
    return Scaffold(
      appBar: PreferredSize(child: AppBar(
        backgroundColor: Colors.white.withAlpha(0),
        elevation: 0.0,
      ),
        preferredSize: Size.fromHeight(0.0)
      ),
```

### flutter_circular_chartでチャート表示

https://pub.dev/packages/flutter_circular_chart#-readme-tab-

ドキュメント通りに実装した。
CircularSegmentEntryは値(100)がmaxになるので割合を出すために少し計算処理を加えた。
```
import 'package:flutter/material.dart';
import 'package:flutter_circular_chart/flutter_circular_chart.dart';
import 'package:saving_money/models/money_model.dart';

class CircleChartView extends StatelessWidget {

  CircleChartView({@required this.models, @required this.goalValue});

  final List<MoneyModel> models;
  final int goalValue;

  double percent() {
    if (models.isEmpty) {
      return 0.0;
    } else {
      return ((models.map((task) => task.value).toList().reduce((curr, next) => curr + next).toDouble()) / goalValue) * 100;
    }
  }

  final GlobalKey<AnimatedCircularChartState> _chartKey = GlobalKey<AnimatedCircularChartState>();

  @override
  Widget build(BuildContext context) {
    return Container(
      child: AnimatedCircularChart(
        key: _chartKey,
        size: Size(200,200),
        initialChartData: <CircularStackEntry>[
          CircularStackEntry(
            <CircularSegmentEntry>[
              CircularSegmentEntry(
                percent(),
                Colors.blue[400],
                rankKey: 'completed',
              ),
              CircularSegmentEntry(
                (100 - percent()).abs(),
                Colors.blueGrey[600],
                rankKey: 'remaining',
              ),
            ],
            rankKey: 'progress',
          ),
        ],
        chartType: CircularChartType.Radial,
        edgeStyle: SegmentEdgeStyle.round,
        percentageValues: true,
        holeLabel: '${percent().toStringAsFixed(1)}%',
        labelStyle: TextStyle(
          color: Colors.blueGrey[600],
          fontWeight: FontWeight.bold,
          fontSize: 24.0,
        ),
      ),
    );
  }
}
```

<img width="300" alt="スクリーンショット 2020-01-26 21 08 23" src="https://user-images.githubusercontent.com/11751495/73135198-cc8de980-4082-11ea-9277-0b00fab6773e.png">



