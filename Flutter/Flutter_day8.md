### やったこと

- セクション11: Boss Level Challenge 2 - Destini


### 背景に画像を当てる

Containerのdecorationプロパティに設定するとできるらしい

https://stackoverflow.com/questions/44179889/flutter-sdk-set-background-image

Stackを使うやり方もあったが今回の課題的に修正が多いので多分こっちであっていそう。

[Stackを使う方法](https://inducesmile.com/google-flutter/how-to-add-a-background-image-to-a-page-in-flutter/)

```
body: Container(
        //TODO: Step 1 - Add background.png to this Container as a background image.
        decoration: BoxDecoration(
          image: DecorationImage(
            image: AssetImage('images/background.png'),
            fit: BoxFit.fill
          )
        ),
```

### Widgetの表示・非表示を動的に切り替える

Visibilityを使う

```
// buttonShouldBeVisible() はboolを返すメソッド
child: Visibility(
  visible: storyBrain.buttonShouldBeVisible(),
  child: FlatButton(
    onPressed: () {
      //Choice 2 made by user.
      setState(() {
        storyBrain.nextStory(2);
      });
    },
    color: Colors.blue,
    child: Text(
      storyBrain.getChoice2(),
      style: TextStyle(
        fontSize: 20.0,
      ),
    ),
  ),
),
```

### できたもの
![Dec-28-2019 18-12-39](https://user-images.githubusercontent.com/11751495/71541524-b581ac00-299d-11ea-9791-7f9b7661958b.gif)


### Repositories

https://github.com/mcz9mm/destini-challenge-starting
