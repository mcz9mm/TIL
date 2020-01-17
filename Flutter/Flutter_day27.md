### やったこと
- Task Modelの作成
- ListView Builder
- Lifting State Upを使ってタスクの追加

### Task Modelの作成

TODOで扱うModelを作成する
```
class Task {

  final String name;
  bool isDone;

  Task({this.name, this.isDone = false});

  void toggleDone() {
    isDone = !isDone;
  }
}
```


### ListView Builder

https://api.flutter.dev/flutter/widgets/ListView-class.html

> The ListView.builder constructor takes an IndexedWidgetBuilder, 
> which builds the children on demand. 
> This constructor is appropriate for list views with a large (or infinite)
> number of children because the builder is called only for those 
> children that are actually visible.

https://api.flutter.dev/flutter/widgets/IndexedWidgetBuilder.html

```
return ListView.builder(itemBuilder: (context, index) {
      return TaskTile(
        taskTitle: tasks[index].name,
        isChecked: tasks[index].isDone,
        checkboxCallBack: (checkboxState) {
          setState(() {
            tasks[index].toggleDone();
          });
        },
      );
    },
      itemCount: tasks.length,
    );
```

#### TaskTileをStatelessに変更

```
class TaskTile extends StatelessWidget {

  final bool isChecked;
  final String taskTitle;
  final Function checkboxCallBack;

  TaskTile({this.isChecked, this.taskTitle, this.checkboxCallBack});

  @override
  Widget build(BuildContext context) {
    return ListTile(
      title: Text(
        taskTitle,
        style: TextStyle(
          decoration: isChecked ? TextDecoration.lineThrough : null,
        ),
      ),
      trailing: Checkbox(
        activeColor: Colors.lightBlueAccent,
        value: isChecked,
        onChanged: checkboxCallBack,
      ),
    );
  }
}
```

#### TaskListはStateful

```
class TasksList extends StatefulWidget {
  @override
  _TasksListState createState() => _TasksListState();
}

class _TasksListState extends State<TasksList> {

  List<Task> tasks = [
    Task(name: 'Buy milk'),
    Task(name: 'Buy eggs'),
    Task(name: 'Buy bread'),
  ];

  @override
  Widget build(BuildContext context) {
    return ListView.builder(itemBuilder: (context, index) {
      return TaskTile(
        taskTitle: tasks[index].name,
        isChecked: tasks[index].isDone,
        checkboxCallBack: (checkboxState) {
          setState(() {
            tasks[index].toggleDone();
          });
        },
      );
    },
      itemCount: tasks.length,
    );
  }
}
```


###  Lifting State Upを使ってタスクの追加
https://flutter.dev/docs/development/data-and-backend/state-mgmt/simple#lifting-state-up

```
class TasksList extends StatefulWidget {
  // 外部からListを受け取る
  final List<Task> tasks;
  TasksList({this.tasks});

  @override
  _TasksListState createState() => _TasksListState();
}

// widget.でアクセスできる
TaskTile(
  taskTitle: widget.tasks[index].name,
  isChecked: widget.tasks[index].isDone,
  checkboxCallBack: (checkboxState) {
    setState(() {
      tasks[index].toggleDone();
    });
  },
);
```


#### AddTaskScreenはコールバックを作成

```
class AddTaskScreen extends StatelessWidget {

  final Function addTaskCallBack;

  AddTaskScreen(this.addTaskCallBack);
```


newTaskTitleがコールバックで返されるのでそれをタスクに追加
```
floatingActionButton: FloatingActionButton(
  onPressed: () {
    showModalBottomSheet(
    context: context,
    builder: (context) => AddTaskScreen(
      (newTaskTitle) {
        setState(() {
          tasks.add(Task(name: newTaskTitle));
        });
        Navigator.pop(context);
      },
    ),
  );
},
backgroundColor: Colors.lightBlueAccent,
child: Icon(Icons.add),
),
```

![Jan-17-2020 09-45-44](https://user-images.githubusercontent.com/11751495/72574922-2a496580-390e-11ea-95de-c9acae19d5b8.gif)

#### 動画だとTasksScreenはStatelessだったけど、、、
newTaskTitleがコールバックで受け取った際にnullになったのでStatefulWidgetに変更して対応した。

```
class AddTaskScreen extends StatefulWidget {
```


### Repositories 
https://github.com/mcz9mm/todoey_flutter
