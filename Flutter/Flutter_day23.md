### やったこと
- Cloud Firestoreへのデータの保存
- Streamsを使用してFirebaseからのデータを監視する
- StreamBuilderを使用してストリームをウィジェットに変換する

### Cloud Firestoreへのデータの保存

#### DataBaseの作成
テストモードで作成
![スクリーンショット 2020-01-12 13 11 23](https://user-images.githubusercontent.com/11751495/72214080-1c769780-353e-11ea-9a19-026b31e88ec3.png)

Collectionは下記のように設定
![スクリーンショット 2020-01-12 13 18 49](https://user-images.githubusercontent.com/11751495/72214081-28faf000-353e-11ea-816a-121af57a38a3.png)
![スクリーンショット 2020-01-12 13 21 20](https://user-images.githubusercontent.com/11751495/72214095-737c6c80-353e-11ea-922f-b5472d580b31.png)

#### メッセージの送信

```
import 'package:cloud_firestore/cloud_firestore.dart';
final _firestore = Firestore.instance;

//

onPressed: () {
  // messageText + loggedInUser.email
  // messagesは先ほど作成したCollectionと一致させる
  _firestore.collection('messages').add({
    // <String: dynamic> 
    'text': messageText,
    'sender': loggedInUser.email,
  });
},
```

データが書き込まれていることを確認

![スクリーンショット 2020-01-12 13 28 12](https://user-images.githubusercontent.com/11751495/72214120-63b15800-353f-11ea-957d-395e7b10d899.png)


### Streamsを使用してFirebaseからのデータを監視する

#### データ取得
```
void getMessages() async {

  final messages = await _firestore.collection('messages').getDocuments();
  for (var message in messages.documents) {
    print(message.data);
  }
}
```

messagesで取得できたdocumentsはこれのこと↓↓
![スクリーンショット_2020-01-12_13_37_36](https://user-images.githubusercontent.com/11751495/72214208-d838c680-3540-11ea-8c01-0120bde7eaac.png)

<img width="419" alt="スクリーンショット 2020-01-12 13 37 06" src="https://user-images.githubusercontent.com/11751495/72214198-a32c7400-3540-11ea-894e-17cb40425c89.png">

#### Streamを利用して更新を監視する
getMessagesでのやり方だと毎秒メソッドをコールし続ける必要がある。

DBにデータが書き込まれた際に通知できるようにするにはStreamを利用する。

```
void messagesStream() async {
  //snapshotsでsubscribeする
  await for ( var snapshot in _firestore.collection('messages').snapshots()) {
    for (var message in snapshot.documents) {
      print(message.data);
    }
  }
}
```

![Jan-12-2020 14-08-48](https://user-images.githubusercontent.com/11751495/72214431-1d5ef780-3545-11ea-8ac3-28d07680e272.gif)

### StreamBuilderを使用してストリームをウィジェットに変換する

https://api.flutter.dev/flutter/widgets/StreamBuilder-class.html

Streamに新しい値が入るたびにsetStateが呼び出される

```
StreamBuilder<QuerySnapshot>(
  stream: _firestore.collection('messages').snapshots(),
  builder: (context, snapshot) {
    if (!snapshot.hasData) {
      return Center(
        child: CircularProgressIndicator(
          backgroundColor: Colors.lightBlueAccent,
        ),
      );
    }
    final messages = snapshot.data.documents;
    List<Text> messagesWidgets = [];
    for (var message in messages) {
      final messageText = message.data['text'];
      final messageSender = message.data['sender'];
      final messageWidget = Text('$messageText from $messageSender');
      messagesWidgets.add(messageWidget);
    }
    return Column(
      children: messagesWidgets,
    );
  },
),
```

