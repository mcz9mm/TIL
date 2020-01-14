### やったこと
- BottomSheet Widget
- BottomSheetにコンテンツを加える 
- CheckBoxのStateを管理する


### BottomSheet Widget
https://api.flutter.dev/flutter/material/BottomSheet-class.html

####  まずは空のContainerを表示

```
Widget buildButtomSheet(BuildContext context) {
  return Container();
}

//
floatingActionButton: FloatingActionButton(
  onPressed: () {
    showModalBottomSheet(context: context, builder: buildButtomSheet);
  },
```

<img width="300" alt="スクリーンショット 2020-01-14 9 05 25" src="https://user-images.githubusercontent.com/11751495/72302328-02a79280-36ad-11ea-8346-086372343890.png">

１行で書くことも可能
```
showModalBottomSheet(context: context, builder: (BuildContext context) => Container());
```

#### 上部のみ角丸実装

少し実装がゴリ押し気味だが。。

```
import 'package:flutter/material.dart';

class AddTaskScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      color: Color(0xff757575),
      child: Container(
        decoration: BoxDecoration(
          color: Colors.white,
          borderRadius: BorderRadius.only(
            topRight: Radius.circular(20.0),
            topLeft: Radius.circular(20.0),
          )
        ),
      ),
    );
  }
}
```

<img width="300" alt="スクリーンショット 2020-01-14 9 15 11" src="https://user-images.githubusercontent.com/11751495/72302756-65e5f480-36ae-11ea-84ca-03209672fd70.png">

### BottomSheetにコンテンツを加える 

```
import 'package:flutter/material.dart';

class AddTaskScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      color: Color(0xff757575),
      child: Container(
        padding: EdgeInsets.all(20.0),
        decoration: BoxDecoration(
          color: Colors.white,
          borderRadius: BorderRadius.only(
            topRight: Radius.circular(20.0),
            topLeft: Radius.circular(20.0),
          )
        ),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: <Widget>[
            Text(
              'Add Task',
              textAlign: TextAlign.center,
              style: TextStyle(
                color: Colors.lightBlueAccent,
                fontSize: 30.0,
              ),
            ),
            TextField(
              autofocus: true,
              textAlign: TextAlign.center,
            ),
            SizedBox(height: 8.0,),
            FlatButton(
              child: Text(
                'Add',
                style: TextStyle(
                  color: Colors.white,
                ),
              ),
              color: Colors.lightBlueAccent,
              onPressed: () {

              },
            ),
          ],
        ),
      ),
    );
  }
}
```

<img width="300" alt="スクリーンショット 2020-01-14 9 24 26" src="https://user-images.githubusercontent.com/11751495/72303157-ab56f180-36af-11ea-97c3-124cc8be83d7.png">


### CheckBoxのStateを管理する

#### Checkbox単体で更新する場合
```
class TaskCheckbox extends StatefulWidget {
  @override
  _TaskCheckboxState createState() => _TaskCheckboxState();
}

class _TaskCheckboxState extends State<TaskCheckbox> {

  bool isChecked = false;

  @override
  Widget build(BuildContext context) {
    return Checkbox(
      activeColor: Colors.lightBlueAccent,
      value: isChecked,
      onChanged: (newValue) {
        setState(() {
          isChecked = newValue;
        });
      },
    );
  }
}
```

![Jan-15-2020 08-19-29](https://user-images.githubusercontent.com/11751495/72391173-cab55380-376f-11ea-84f1-d53fda2713b6.gif)


#### Checkboxが更新された際にTextにも何かしら更新をさせる場合

状態（checkboxState）とコールバックをコンストラクタに追加し、親で管理させる

```
class TaskCheckbox extends StatelessWidget {
  final bool checkboxState;
  final Function toggleCheckboxState;

  TaskCheckbox(this.checkboxState, this.toggleCheckboxState);

  @override
  Widget build(BuildContext context) {
    return Checkbox(
      activeColor: Colors.lightBlueAccent,
      value: checkboxState,
      onChanged: toggleCheckboxState,
    );
  }
}
```

TaskTileがCheckboxを管理。
```
class TaskTile extends StatefulWidget {
  @override
  _TaskTileState createState() => _TaskTileState();
}

class _TaskTileState extends State<TaskTile> {
  bool isChecked = true;

  void checkboxCallBack (bool checkboxState) {
    setState(() {
      isChecked = checkboxState;
    });
  }

  @override
  Widget build(BuildContext context) {
    return ListTile(
      title: Text(
        'This is a task.',
        style: TextStyle(
          decoration: isChecked ? TextDecoration.lineThrough : null,
        ),
      ),
      trailing: TaskCheckbox(isChecked, checkboxCallBack),
    );
  }
}
```

![Jan-15-2020 08-35-55](https://user-images.githubusercontent.com/11751495/72391932-11a44880-3772-11ea-88d4-32f4b3db97bc.gif)

#### コンストラクタに直接コールバックを書くことも可能

```
TaskCheckbox(isChecked, (bool checkboxState) {
  setState(() {
    isChecked = checkboxState;
  });
}),
```


### Repositories 
https://github.com/mcz9mm/todoey_flutter
