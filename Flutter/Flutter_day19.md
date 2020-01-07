### やったこと

Boss Level Challenge 3
- レベル1 銅メダル
- レベル2 銀メダル
- レベル3 金メダル

### API
https://apiv2.bitcoinaverage.com/#ticker-data-per-symbol

### レベル1 銅メダル
ビットコインの価格（米ドル）を表示する

前の気象情報のアプリと同様にデータ通信用クラスを生成、
```
import 'package:http/http.dart' as http;
import 'dart:convert';

class NetworkHelper {

  NetworkHelper(this.url);

  final String url;

  Future getData() async {
    http.Response response = await http.get(url);
    if (response.statusCode == 200) {
      String data = response.body;
      return jsonDecode(data);

    } else {
      print(response.statusCode);
    }
  }
}
```

CoinDataクラスにこのようなメソッドを作成。すでにレベル2,3を意識して、currencyを受け取れるようにしている。
```
Future<dynamic> getLastUSDPrice(String currency) async {

    NetworkHelper networkHelper = NetworkHelper('$bitcoinURL$currency');
    var bitcoinData = await networkHelper.getData();
    return bitcoinData;
  }
```

UI更新も前回を思い出しながら実装
```
void updateUI(dynamic bitcoinData) {

    setState(() {

      if (bitcoinData != null) {
        double lastPrice = bitcoinData['last'];
        currencyPrice = lastPrice.toInt().toString();
      } else {
        currencyPrice = 'Error';
      }
    });
  }
```

呼び出し直後にまずはコールする
```
@override
  void initState() {
    super.initState();

    getLastPrice();
  }


void getLastPrice() async {

    var data = await coinData.getLastUSDPrice(selectedCurrency);
    if (data != null) {
      updateUI(data);
    }
  }
```

<img width="300" alt="スクリーンショット 2020-01-07 9 16 15" src="https://user-images.githubusercontent.com/11751495/71858408-82be7d00-312e-11ea-87fd-8dbd29c12d92.png">


### レベル2 銀メダル
ユーザーが選択した通貨で1ビットコイン（BTC）の最新価格を表示する。

DropdownButtonとCupertinoPickerの`onChanged`、`onSelectedItemChanged`
```
onSelectedItemChanged: (selectedIndex) {
        print(selectedIndex);
        selectedCurrency = currenciesList[selectedIndex];
        getLastPrice();
      },
```

```
onChanged: (value) {
        print(value);
        setState(() {
          selectedCurrency = value;
          getLastPrice();
        });
      },
```

![Jan-07-2020 09-16-58](https://user-images.githubusercontent.com/11751495/71858405-7cc89c00-312e-11ea-9a2f-6023082cd14a.gif)


### レベル3 金メダル
- BTC-ビットコイン
- ETH-イーサリアム
- LTC-ライトコイン

選択した通貨で3つすべての仮想通貨価格を表示できるようにする

３つそれぞれAPIをたたき、通貨をkey, valueの形で保持しておくようにし、それを返すメソッドに修正
```
Future<Map<String, String>> getLastPrice(String currency) async {

    Map<String, String> cryptoPrices = {};
    for (String crypto in cryptoList) {
      NetworkHelper networkHelper = NetworkHelper('$bitcoinURL$crypto$currency');
      var bitcoinData = await networkHelper.getData();
      double price = bitcoinData['last'];
      cryptoPrices[crypto] = price.toStringAsFixed(0);
    }

    return cryptoPrices;
  }
```

Card Widgetもリファクタ対象だったのでExtractWidgetを行った
```
child: CryptoCard(
  crypto: 'LTC',
  price: isWaiting ? '?' : coinValues['LTC'],
  selectedCurrency: selectedCurrency,
),


///
class CryptoCard extends StatelessWidget {

  CryptoCard({
    this.crypto,
    this.price,
    this.selectedCurrency,
  });

  final String price;
  final String crypto;
  final String selectedCurrency;

  @override
  Widget build(BuildContext context) {
    return Card(
      color: Colors.lightBlueAccent,
      elevation: 5.0,
      shape: RoundedRectangleBorder(
        borderRadius: BorderRadius.circular(10.0),
      ),
      child: Padding(
        padding: EdgeInsets.symmetric(vertical: 15.0, horizontal: 28.0),
        child: Text(
          '1 $crypto = $price $selectedCurrency',
          textAlign: TextAlign.center,
          style: TextStyle(
            fontSize: 20.0,
            color: Colors.white,
          ),
        ),
      ),
    );
  }
}
```

![Jan-07-2020 10-03-17](https://user-images.githubusercontent.com/11751495/71860106-f82d4c00-3134-11ea-93c7-e3ad33cb94d4.gif)


### Repositories
https://github.com/mcz9mm/bitcoin-ticker-flutter
