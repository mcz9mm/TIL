### やったこと
- TextFieldをパスワード入力できるようにする
- キーボードの入力タイプを変更する
- FirebaseAuthを使用してFirebaseにユーザーを登録する
- FirebaseAuthでユーザーを認証する
- modal progress hudの導入

###  TextFieldをパスワード入力できるようにする

```
TextField(
  obscureText: true,
```

![Jan-12-2020 11-51-50](https://user-images.githubusercontent.com/11751495/72213422-f945eb00-3531-11ea-8349-d8d23187a640.gif)


### キーボードの入力タイプを変更する

```
TextField(
  keyboardType: TextInputType.emailAddress,
```

<img width="398" alt="スクリーンショット 2020-01-12 11 58 16" src="https://user-images.githubusercontent.com/11751495/72213468-d49e4300-3532-11ea-9eca-f66c887dc4e0.png">


### FirebaseAuthを使用してFirebaseにユーザーを登録する

Firebase Authenticationの設定でメールパスワードログイン設定を有効化する
![スクリーンショット_2020-01-12_12_11_04](https://user-images.githubusercontent.com/11751495/72213588-ba656480-3534-11ea-88fe-06c1dece6595.png)

#### 登録処理

```
final _auth = FirebaseAuth.instance;

// 登録部分
onPress: () async {
  try {
    // passwordは6文字以上であること
    final newUser = await _auth.createUserWithEmailAndPassword(email: email, password: password);
    if (newUser != null) {
      Navigator.pushNamed(context, ChatScreen.id);
    }
  } catch (e) {
    print(e);
  }
},
```

![スクリーンショット 2020-01-12 12 17 00](https://user-images.githubusercontent.com/11751495/72213631-71fa7680-3535-11ea-8a99-b2983561afdb.png)

#### getUser

```
final _auth = FirebaseAuth.instance;
FirebaseUser loggedInUser;

void getCurrentUser() async {
  try {
    final user = await _auth.currentUser();
    if (user != null) {
      loggedInUser = user;
      print(loggedInUser.email);
    }
  } catch (e) {
    print(e);
  }
}
```

### FirebaseAuthでユーザーを認証する


```
final _auth = FirebaseAuth.instance;

// 認証部分
onPress: () async {
  try {
    final user = await _auth.signInWithEmailAndPassword(
    email: email, password: password);
    if (user != null) {
      Navigator.pushNamed(context, ChatScreen.id)
    }
  } catch (e) {
    print(e);
  }
},
```


### modal progress hudの導入
https://pub.dev/packages/modal_progress_hud

```
bool showSpinner = false;

// Paddingをラップする
return Scaffold(
  backgroundColor: Colors.white,
  body: ModalProgressHUD(
    inAsyncCall: showSpinner,
      child: Padding(
      
// 要リファクタではあるが、更新部分はsetStateで行う
onPress: () async {
  setState(() {
    showSpinner = true;
  });
  try {
    final newUser = await _auth.createUserWithEmailAndPassword(email: email, password: password)
    if (newUser != null) {
      Navigator.pushNamed(context, ChatScreen.id);
    }
    setState(() {
      showSpinner = false;
    });
  } catch (e) {
    print(e);
  }
},
```

![Jan-12-2020 12-46-23](https://user-images.githubusercontent.com/11751495/72213909-68274200-353a-11ea-8195-5bd82fd07423.gif)



