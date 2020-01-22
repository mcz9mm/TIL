### やったこと
- Datetimeの変換


### Datetimeの変換

こちらを参考にさせていいただきました。
https://medium.com/flutter-jp/datetime-17e618c8e26e

https://medium.com/flutter-jp/intl-beb5b9e8ee73

SQLiteへはDatetime型はサポートされていないのでStringで保存するしかない

#### Date→String

```
final date = DateTime.now().toUtc().toIso8601String();
```

#### parse用のメソッドを作成

```
String parseDateTitle(String fromDate) {
  final parseDate = DateTime.parse(fromDate).toLocal();
  return '${parseDate.year}/${parseDate.month}/${parseDate.day} ${parseDate.hour}:${parseDate.minute}';
}
```

### 進捗悪し
アプリの機能とか考えてたら迷走してあまり実装できず。。
