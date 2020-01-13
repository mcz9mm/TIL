### やったこと
ToDoリストの作成

- デザインを見ながら実装


### デザインを見ながら実装

課題として実装するのは↓のデザイン
![スクリーンショット 2020-01-14 7 52 44](https://user-images.githubusercontent.com/11751495/72298946-dbe45e80-36a2-11ea-9126-c6c7cb5223d4.png)

ヘッダー部分
```
class TasksScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.lightBlueAccent,
      body: Container(
        padding: EdgeInsets.only(top: 60.0, left: 30.0, right: 30.0, bottom: 30.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: <Widget>[
            CircleAvatar(
              child: Icon(
                Icons.list,
                size: 30.0,
                color: Colors.lightBlueAccent,
              ),
              backgroundColor: Colors.white,
              radius: 30.0,
            ),
            SizedBox(
              height: 10.0,
            ),
            Text(
              'Todoey',
              style: TextStyle(
                color: Colors.white,
                fontSize: 50.0,
                fontWeight: FontWeight.w700,
              ),
            ),
            Text(
              '12 tasks',
              style: TextStyle(
                color: Colors.white,
                fontSize: 18.0
              ),
            )
          ],
        ),
      ),
    );
  }
}
```

<img width="300" alt="スクリーンショット 2020-01-14 8 04 37" src="https://user-images.githubusercontent.com/11751495/72299549-85781f80-36a4-11ea-94d1-892b0752844f.png">


#### BottomのWhiteViewのレイアウト

Columnでさらに全体をWrapしてExpandedで表現する

上部だけ角丸にするやり方↓
```
borderRadius: BorderRadius.only(
  topLeft: Radius.circular(20.0),
  topRight: Radius.circular(20.0),
)
```

```
body: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: <Widget>[
          Container(
            padding: EdgeInsets.only(top: 60.0, left: 30.0, right: 30.0, bottom: 30.0),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: <Widget>[
                CircleAvatar(
                  child: Icon(
                    Icons.list,
                    size: 30.0,
                    color: Colors.lightBlueAccent,
                  ),
                  backgroundColor: Colors.white,
                  radius: 30.0,
                ),
                SizedBox(
                  height: 10.0,
                ),
                Text(
                  'Todoey',
                  style: TextStyle(
                    color: Colors.white,
                    fontSize: 50.0,
                    fontWeight: FontWeight.w700,
                  ),
                ),
                Text(
                  '12 tasks',
                  style: TextStyle(
                      color: Colors.white,
                      fontSize: 18.0
                  ),
                ),
              ],
            ),
          ),
          Expanded(
            child: Container(
              decoration: BoxDecoration(
                  color: Colors.white,
                  borderRadius: BorderRadius.only(
                    topLeft: Radius.circular(20.0),
                    topRight: Radius.circular(20.0),
                  )
              ),
            ),
          ),
        ],
      ),
```

<img width="300" alt="スクリーンショット 2020-01-14 8 23 44" src="https://user-images.githubusercontent.com/11751495/72300457-32539c00-36a7-11ea-9478-ba77dfa926b0.png">


#### FloatingButtonの追加

```
return Scaffold(
  backgroundColor: Colors.lightBlueAccent,
  floatingActionButton: FloatingActionButton(
    backgroundColor: Colors.lightBlueAccent,
    child: Icon(Icons.add),
  ),
```
<img width="300" alt="スクリーンショット 2020-01-14 8 29 14" src="https://user-images.githubusercontent.com/11751495/72300724-f53bd980-36a7-11ea-9bd7-75d879ef2251.png">


#### ListViewの追加

WidgetをExtract

```
import 'package:flutter/material.dart';
import 'package:todoey_flutter/widgets/task_tile.dart';

class TasksList extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return ListView(
      children: <Widget>[
        TaskTile(),
        TaskTile(),
      ],
    );
  }
}
```

Listの中身の部分
```
import 'package:flutter/material.dart';

class TaskTile extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return ListTile(
      title: Text('This is a task.'),
      trailing: Checkbox(
        value: false,
      ),
    );
  }
}
```

List呼び出し部分

```
Expanded(
  child: Container(
    padding: EdgeInsets.symmetric(horizontal: 20.0),
    decoration: BoxDecoration(
      color: Colors.white,
      borderRadius: BorderRadius.only(
        topLeft: Radius.circular(20.0),
        topRight: Radius.circular(20.0),
      ),
    ),
    child: TasksList(),
  ),
),
```

<img width="300" alt="スクリーンショット 2020-01-14 8 48 42" src="https://user-images.githubusercontent.com/11751495/72301615-b0fe0880-36aa-11ea-9b7e-59a55e3fb50a.png">


### Repositories 
https://github.com/mcz9mm/todoey_flutter
