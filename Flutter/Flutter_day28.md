### やったこと
- Flutter App Architecture Patterns
  - MVCの復習
- Provider Package
- ProviderとChangeNotifierを利用した実装にする
- Flutterコースの終了

### Flutter App Architecture Patterns

#### MVC

- Model: Data&Logic
- View: User Interface
- Controller: Mediator

View 

↓

(Send input events)

↓

Controller 

↓

(Makes request)

↓

Model 

↓

(Sends data)

↓

Controller

↓

(Modifies)

↓

View


### Provider Package
Lifting State Upは複数画面での値の管理が複雑になる。

Google公式で推奨されているのが`Provider Package`である。

https://pub.dev/packages/provider

#### 何が解決できるのか

- View1(data)
- View2
- View3
- View4(data)

1→2→3→4で階層ができているとして、1のdataを4でも使いたい場合、2,3を経由して
データの値渡しをしなければならない。

Providerを利用するとStateをsubscribeできるのでView1でのdata更新を
View3で監視（Listen）することができる。


View1
```
//data == String
Provider<String>(
  create: (context) {
    return data;
  }
)
// or
Provider<String>(
  create: (context) => data,
)
```

View4(dataを利用する部分)
```
Text(Provider.of<String>(context));
```

#### Dataを通知用Classにする

```
class Data extends ChangeNotifer {
  String data = 'sample data here';
}

// View1
ChangeNotiferProvider<Data>(
  create: (context) => Data(),
  
// View4
Text(Provider.of<Data>(context).data);
```

#### TextField用にする


```
//View3
TextField(
  onChanged: (newText) {
    Provider.of<Data>(context).chnageString(newText);
  }
);

class Data extends ChangeNotifer {
  String data = 'sample data here';
  
  Void chnageString(String newString) {
    data = newString;
    // リスナー通知メソッド
    notifyListeners();
  }
}
```

#### 毎回通知させたくない場合

```
Text(Provider.of<Data>(context, listen: false).data);
```

### ProviderとChangeNotifierを利用した実装にする
TODOアプリに必要な機能

- Read
- Add
- Check
- Delete

#### READ

TaskData
```
import 'package:flutter/foundation.dart';
import 'package:todoey_flutter/models/tasks.dart';

class TaskData extends ChangeNotifier {

  List<Task> tasks = [
    Task(name: 'Buy milk'),
    Task(name: 'Buy eggs'),
    Task(name: 'Buy bread'),
  ];
}
```

main
```
Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => TaskData(),
      child: MaterialApp(
        home: TasksScreen(),
      ),
    );
  }
```

TasksList
```
class TasksList extends StatelessWidget {
 
  @override
  Widget build(BuildContext context) {
    return ListView.builder(itemBuilder: (context, index) {
      return TaskTile(
        taskTitle: Provider.of<TaskData>(context).tasks[index].name,
        isChecked: Provider.of<TaskData>(context).tasks[index].isDone,
        checkboxCallBack: (checkboxState) {
          //setState(() {
          //  Provider.of<TaskData>(context).tasks[index].toggleDone();
          //});
        },
      );
    },
      itemCount: Provider.of<TaskData>(context).tasks.length,
    );
  }
}
```

#### TasksListのProvider.of<TaskData>(context)を簡略化

```
Consumer<TaskData>(
  builder: (context, taskData,  child) {
    return ListView
  }
```

```
class TasksList extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return Consumer<TaskData>(
      builder: (context, taskData,  child) {
        return ListView.builder(itemBuilder: (context, index) {
          return TaskTile(
            taskTitle: taskData.tasks[index].name,
            isChecked: taskData.tasks[index].isDone,
            checkboxCallBack: (checkboxState) {
//          setState(() {
//            taskData.tasks[index].toggleDone();
//          });
            },
          );
        },
          itemCount: taskData.tasks.length,
        );
      },
    );
  }
}
```

#### getterを利用する

```
// getter
int get taskCount {
  return tasks.length;
}

// TasksList
itemCount: taskData.taskCount,
```

#### Add

TaskDataに追加用のメソッドを作成、通知リスナーを用意
```
void addTask(String newTaskTitle) {
  final task = Task(name: newTaskTitle);
  tasks.add(task);
  notifyListeners();
}
```

#### Taskを外部から変更させないようにする

UnmodifiableListViewは変更不可にするもの
```
List<Task> _tasks = [
  Task(name: 'Buy milk'),
  Task(name: 'Buy eggs'),
  Task(name: 'Buy bread'),
];

UnmodifiableListView<Task> get tasks {
  return UnmodifiableListView(_tasks);
}
```

```
Provider.of<TaskData>(context, listen: false).addTask(newTaskTitle);
```

#### Check

タスクの更新を行う

TaskDataに追加
```
void updateTask(Task task) {
  task.toggleDone();
  notifyListeners();
}
```

```
class TasksList extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return Consumer<TaskData>(
      builder: (context, taskData,  child) {
        return ListView.builder(itemBuilder: (context, index) {
          final task = taskData.tasks[index];
          return TaskTile(
            taskTitle: taskData.tasks[index].name,
            isChecked: taskData.tasks[index].isDone,
            checkboxCallBack: (checkboxState) {
              taskData.updateTask(task);
            },
          );
        },
          itemCount: taskData.taskCount,
        );
      },
    );
  }
}
```

#### Delete

ListTileでロングタップされた時に削除する

```
void deleteTask(Task task) {
  _tasks.remove(task);
  notifyListeners();
}
```

```
return ListTile(
  onLongPress: longPressCallBack,

//
longPressCallBack: () {
  taskData.deleteTask(task);
},
```

### できたもの
![Jan-18-2020 15-30-55](https://user-images.githubusercontent.com/11751495/72659722-8fcd4d00-3a07-11ea-947d-c777d2a48b62.gif)

### Flutterコースの終了
![UC-B0WIF0QP](https://user-images.githubusercontent.com/11751495/72659733-a83d6780-3a07-11ea-8de2-57624d8fd132.jpg)

### Repositories 
https://github.com/mcz9mm/todoey_flutter
