### やったこと
- ListView
- Flexibleを利用する
- チャットUIに寄せてデザインする
- 投稿順に表示させる
- Cloud Firestore Authorisation and Security Rules

### ListView

#### チャットアプリ風デザインを実装する

https://api.flutter.dev/flutter/widgets/ListView-class.html

```
class MessageBubble extends StatelessWidget {

  MessageBubble({this.sender, this.text});
  final String sender;
  final String text;

  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: EdgeInsets.all(10.0),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.end,
        children: <Widget>[
          Text(
            sender,
            style: TextStyle(
              fontSize: 12.0,
              color: Colors.black54
            ),
          ),
          Material(
            elevation: 5.0,
            borderRadius: BorderRadius.circular(30.0),
            color: Colors.lightBlueAccent,
            child: Padding(
              padding: EdgeInsets.symmetric(vertical: 10.0, horizontal: 20.0),
              child: Text(
                '$text',
                style: TextStyle(
                  color: Colors.white,
                  fontSize: 15.0,
                ),
              ),
            ),
          ),
        ],
      ),
    );
  }
}
```

#### ListView作成部分

```
List<MessageBubble> messagesBubbles = [];
for (var message in messages) {
  final messageText = message.data['text'];
  final messageSender = message.data['sender'];
  final messageBubble = MessageBubble(
    sender: messageSender,
    text: messageText,
  );
  messagesBubbles.add(messageBubble);
}

final messageBubble = MessageBubble(
  sender: messageSender,
  text: messageText,
);

return Expanded(
  child: ListView(
    padding: EdgeInsets.symmetric(horizontal: 10.0, vertical: 20.0),
    children: messagesBubbles,
  ),
);
```

<img width="300" alt="スクリーンショット 2020-01-13 13 20 22" src="https://user-images.githubusercontent.com/11751495/72232901-768f5f80-3607-11ea-8af8-074d87747f43.png">


### Flexibleを利用する
https://api.flutter.dev/flutter/widgets/Flexible-class.html

AndroidはiPhoneよりアスペクト比が高いのでキーボードが表示される際に、
ロゴの画像が上にシフトした際に途切れてしまう。（レイアウトエラーが表示される）

<img width="600" alt="スクリーンショット 2020-01-13 13 30 25" src="https://user-images.githubusercontent.com/11751495/72233191-18637c00-3609-11ea-8679-53fa6328ddd5.png">

Flexibleでwrapしてあげる
```
Flexible(
  child: Hero(
    tag: 'logo',
    child: Container(
      height: 200.0,
      child: Image.asset('images/logo.png'),
    ),
  ),
),
```

<img width="600" alt="スクリーンショット 2020-01-13 13 30 05" src="https://user-images.githubusercontent.com/11751495/72233154-e8b47400-3608-11ea-83d4-50c6aee7b78b.png">

### チャットUIに寄せてデザインする

isMeはloggedInUserのemailでsenderと比較できる
```
class MessageBubble extends StatelessWidget {

  MessageBubble({this.sender, this.text, this.isMe});
  final String sender;
  final String text;
  final bool isMe;

  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: EdgeInsets.all(10.0),
      child: Column(
        crossAxisAlignment: isMe ? CrossAxisAlignment.end : CrossAxisAlignment.start,
        children: <Widget>[
          Text(
            sender,
            style: TextStyle(
              fontSize: 12.0,
              color: Colors.black54
            ),
          ),
          Material(
            elevation: 5.0,
            borderRadius: isMe ? BorderRadius.only(
                topLeft: Radius.circular(30.0),
                bottomLeft: Radius.circular(30.0),
                bottomRight: Radius.circular(30.0)
            ) : BorderRadius.only(
                topRight: Radius.circular(30.0),
                bottomLeft: Radius.circular(30.0),
                bottomRight: Radius.circular(30.0)
            ) ,
            color: isMe ? Colors.lightBlueAccent : Colors.white,
            child: Padding(
              padding: EdgeInsets.symmetric(vertical: 10.0, horizontal: 20.0),
              child: Text(
                '$text',
                style: TextStyle(
                  color: isMe ? Colors.white : Colors.black54,
                  fontSize: 15.0,
                ),
              ),
            ),
          ),
        ],
      ),
    );
  }
}
```

<img width="300" alt="スクリーンショット 2020-01-13 14 13 06" src="https://user-images.githubusercontent.com/11751495/72234184-26b49680-360f-11ea-9087-7642070fdf00.png">


### 投稿順に表示させる

```
final messages = snapshot.data.documents.reversed;

child: ListView(
  reverse: true,
```

![Jan-13-2020 14-41-32](https://user-images.githubusercontent.com/11751495/72234993-16061f80-3613-11ea-89e6-abfa51632df6.gif)

### Cloud Firestore Authorisation and Security Rules

https://firebase.google.com/docs/rules/get-started?authuser=0

ユーザー認証済みであれば読み取り、書き込み権限を付与する
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth.uid != null;
    }
  }
}
```

![スクリーンショット 2020-01-13 14 50 46](https://user-images.githubusercontent.com/11751495/72235195-1652ea80-3614-11ea-8cec-9ea838ec158d.png)

