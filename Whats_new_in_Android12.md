# What’s new in Android
#googleio

[動作の変更点: Android 12 をターゲットとするアプリ  |  Android 12 デベロッパー プレビュー](https://developer.android.com/about/versions/12/behavior-changes-12)
[動作の変更点: すべてのアプリ  |  Android 12 デベロッパー プレビュー  |  Android Developers](https://developer.android.com/about/versions/12/behavior-changes-all)

## annotationを非推奨に

<img width="500" alt="スクリーンショット 2021-05-19 14 39 16" src="https://user-images.githubusercontent.com/11751495/118768139-9ef13300-b8b9-11eb-8555-c647957195b8.png">


## Colorシステムの変更　パレットの拡張

ロック画面、ホーム画面、通知で馴染むように変更した
壁紙からColorのムードを取得できるようになった

<img width="500" alt="スクリーンショット 2021-05-19 14 41 14" src="https://user-images.githubusercontent.com/11751495/118768195-afa1a900-b8b9-11eb-95f2-f38c3f3f275f.png">
<img width="500" alt="スクリーンショット 2021-05-19 14 42 02" src="https://user-images.githubusercontent.com/11751495/118768207-b3353000-b8b9-11eb-85ab-866b2b481f34.png">


自動でできるが手動で設定する場合は0から1000のパターンを選べるようにしている

<img width="500" alt="スクリーンショット 2021-05-19 14 43 03" src="https://user-images.githubusercontent.com/11751495/118768271-c3e5a600-b8b9-11eb-98fa-f727d0e5ae6c.png">

## Widgetの更新
Androidユーザーの84%がホーム画面に少なくとも１つウィジェットを配置している。約3分の2がホーム画面に2つ以上のウィジェットを配置している。
ビジュアルデザインの観点からあまり使われなくなってる。システムUIを変更して選択を簡単にした。デベロッパーが実装する場合でもウィジェットレイアウトをホーム画面に馴染ませてUIを構築することができる。

詳しくは”Refreshing widgets”のセッションを見てね。

## Launch animation
[Splash screens  |  Android 12 デベロッパー プレビュー  |  Android Developers](https://developer.android.com/about/versions/12/features/splash-screen)
アプリのコールドスタートの問題。起動時にアニメーションを行う際、最新のデータやスクリーンショットがない場合、読み込みが終わるまで空のグラデーションが表示されてしまう。
スプラッシュ画面を用意し、アプリのアイコンがズームするアニメーションを全てのアプリに対応させた。アプリの読み込み中は主にバックグラウンドで実行される。

<img width="500" alt="スクリーンショット 2021-05-19 14 54 55" src="https://user-images.githubusercontent.com/11751495/118768519-11faa980-b8ba-11eb-9f95-081abfd6a730.png">

気に入らない場合はカスタマイズできる。
ズームの値や持続時間、カラーなどアニメーション自体のプロパティを変更できる。

## Notifications
### 1.全てのテンプレートを再設計→新しいUIに対応したものになっている

もちろんカスタマイズもできる。が作業時間かかるかも。

<img width="500" alt="スクリーンショット 2021-05-19 14 59 24" src="https://user-images.githubusercontent.com/11751495/118768579-2474e300-b8ba-11eb-8ef7-ea754ca0f86a.png">


### 2.トランポリン
通知をタップしたあとアプリが起動するけど数秒間何も起こらないのを改善した。

![May-19-2021 15-01-01](https://user-images.githubusercontent.com/11751495/118768621-3191d200-b8ba-11eb-8e3f-baa483b1f934.gif)

## Toast
トーストにアイコンを表示できるようになった。
どのアプリの通知かわかるようになったけど、その分表示できる文章が減ったので１行または２行の短いテキストにすること。
レート制限の追加。重なってループ表示されることを防いだ。（上限を設定した）

## Picture in Pictureの改善
[Picture in Picture (PiP) improvements  |  Android 12 デベロッパー プレビュー](https://developer.android.com/about/versions/12/features/pip-improvements)

## コンテンツをぼかす機能の復活
どんなViewでも使うことができる。リアルタイムで。
他の場所でもできる。ウィンドウコンテンツや、その外側にあるものもぼかすことができる。

<img width="500" alt="スクリーンショット 2021-05-19 15 06 34" src="https://user-images.githubusercontent.com/11751495/118768730-4ec6a080-b8ba-11eb-8101-f599f04c128f.png">
<img width="500" alt="スクリーンショット 2021-05-19 15 08 22" src="https://user-images.githubusercontent.com/11751495/118768735-4ff7cd80-b8ba-11eb-8989-4119da552f4c.png">

## Ripple効果のアップデート
スパークル効果がある。
デフォルトで有効になるので特に追加は必要ない。

<img width="500" alt="スクリーンショット 2021-05-19 15 10 18" src="https://user-images.githubusercontent.com/11751495/118768811-67cf5180-b8ba-11eb-91cb-c149451e8887.png">

## スクロール時のグロー効果
[Overscroll effect  |  Android 12 デベロッパー プレビュー  |  Android Developers](https://developer.android.com/about/versions/12/overscroll)

これもデフォルトで追加

## リッチコンテンツの挿入
[コンテンツ受信用の Unified API  |  Android 12 デベロッパー プレビュー  |  Android Developers](https://developer.android.com/about/versions/12/features/unified-content-api)

<img width="500" alt="スクリーンショット 2021-05-19 15 39 07" src="https://user-images.githubusercontent.com/11751495/118768866-77e73100-b8ba-11eb-9713-e226d2f5fd8b.png">

## Image

AVIFという画像フォーマットのサポートが追加

エンコードした際に画質が落ちないのが特徴
可逆圧縮もサポート

<img width="500" alt="スクリーンショット 2021-05-19 15 14 16" src="https://user-images.githubusercontent.com/11751495/118768915-83d2f300-b8ba-11eb-8077-e00f11cb1b00.png">


## Movie
[互換性のあるメディアのコード変換  |  Android 12 デベロッパー プレビュー  |  Android Developers](https://developer.android.com/about/versions/12/features/compatible-media-transcoding)
アプリ毎にサポートできる・できないをマニフェストに記載できる
また、ContentResolverを利用してメディアの取得を行うと確認できる。


## Audio
Audio-coupled Haptic Playbackという機能が追加

<img width="500" alt="スクリーンショット 2021-05-19 15 19 43" src="https://user-images.githubusercontent.com/11751495/118768984-9b11e080-b8ba-11eb-91b2-6750c89c204c.png">

曲を読み込んでこのAPIを設定すると、読み込んだ曲に基づいた振動パターンが生成される。
全てのデバイスでサポートされていないのでisAvailableでチェックしてから使うこと。

## Performance
[Performance class  |  Android 12 デベロッパー プレビュー  |  Android Developers](https://developer.android.com/about/versions/12/features/performance-class)


## Privacy

### Bluetooth
[New Bluetooth permissions in Android 12  |  Android 12 デベロッパー プレビュー](https://developer.android.com/about/versions/12/features/bluetooth-permissions)
アプリを使っていない時はデータにアクセスできないようにしている。
Bluetoothの利用権限が位置情報に含まれていたのを分離して単独で権限の許諾を求められるようになった。

### Location
位置情報の許諾方法も変更された。
許可するが正確な情報を得ることができないようにする。のが追加。

<img width="500" alt="スクリーンショット 2021-05-19 15 23 34" src="https://user-images.githubusercontent.com/11751495/118769040-aa912980-b8ba-11eb-9099-0a416f1b1675.png">

### Clipboard Access

クリップボードの情報を取得できるが通知が来るようになった。
クリップボードにアクセスする際はキーボードかフォアグラウンドなアプリだけ。


<img width="500" alt="スクリーンショット 2021-05-19 15 27 11" src="https://user-images.githubusercontent.com/11751495/118769043-abc25680-b8ba-11eb-8e72-3444964b88bc.png">


## Wear
アプリからUI操作する方法が更新
