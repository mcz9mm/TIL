### やったこと
- SQLiteを使ってデータの永続化
- データの保存
- 読み取り


### SQLiteを使ってデータの永続化

https://flutter.dev/docs/cookbook/persistence/sqlite#3-open-the-database


基本的にはこちら→[日本語版](https://flutter.ctrnost.com/logic/sqlite/)を参考に実装した

※今回扱うModel用に書き直しているだけなので詳細等は上記リンクを参考にしてください。

pubspec.yml
```
dependencies:
  flutter:
    sdk: flutter
  sqflite:
  path:
```

import
```
import 'dart:async';
import 'package:path/path.dart';
import 'package:sqflite/sqflite.dart';
```

#### DBの設定、扱うModelの定義

```
class MoneyModel {

  final int id;
  final String name;
  final int value;
  final String date;

  MoneyModel({this.id, this.name, this.value, this.date});

  Map<String, dynamic> toMap() {
    return {
      'id': id,
      'name': name,
      'value': value,
      'date': date,
    };
  }
}
```

```
Future<Database> initDatabase() async {
  return openDatabase(
  join(await getDatabasesPath(), 'money_database.db'),
    onCreate: (db, version) {
      return db.execute("CREATE TABLE money(id INTEGER PRIMARY KEY, name TEXT, value INTEGER, date TEXT)",);
    },
    version: 1,
  );
}
```

```
Future<Database> getDatabase() async {
  return openDatabase(
    join(await getDatabasesPath(), 'money_database.db'),
  );
}
```

### データの保存 Insert

```
Future<void> insertMoney(MoneyModel model) async {
  final Database db = await getDatabase();
  await db.insert(
    'money',
    model.toMap(),
    conflictAlgorithm: ConflictAlgorithm.replace,
  );
}
```


### 保存したデータの取得

```
Future<List<MoneyModel>> getMoneys() async {
  final Database db = await getDatabase();
  final List<Map<String, dynamic>> maps = await db.query('money');
  return List.generate(maps.length, (i) {
    return MoneyModel(
      id: maps[i]['id'],
      name: maps[i]['name'],
      value: maps[i]['value'], 
      date: maps[i]['date'],
    );
  });
}
```

呼び出しはこんな感じ
```
void setDatabase() async {
  var models = await MoneyDatabase().getMoneys();
  _moneys = models;
  notifyListeners();
}
```


DeleteとUpdateは次回やります。

