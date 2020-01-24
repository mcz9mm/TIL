### やったこと
- BottomNavigationBarの実装
- Pageの切替


### BottomNavigationBarの実装

https://api.flutter.dev/flutter/material/BottomNavigationBar-class.html

Scaffold ウィジェットに組み込んでいく

```
int _selectedIndex = 0;
  static const TextStyle optionStyle = TextStyle(fontSize: 30, fontWeight: FontWeight.bold);
  void _onItemTapped(int index) {
    setState(() {
      _selectedIndex = index;
    });
  }
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      //
      //
      //
      bottomNavigationBar: BottomNavigationBar(
        items: const <BottomNavigationBarItem>[
          BottomNavigationBarItem(
            icon: Icon(Icons.home),
            title: Text('Home'),
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.insert_chart),
            title: Text('Charts'),
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.call_made),
            title: Text('Goals'),
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.settings),
            title: Text('Settings'),
          ),
        ],
        currentIndex: _selectedIndex,
        selectedItemColor: kPrimaryColor,
        unselectedItemColor: kSecondaryColor,
        onTap: _onItemTapped,
      ),
    );
  }
```


### Pageの切替

```
final List<Widget> _widgetOptions = <Widget>[
    MoneysPage(),
    ChartsPage(), // Added
    GoalsPage(), // Added
    SettingsPage(), // Added
  ];
```

```
 return Scaffold(
      body: _widgetOptions.elementAt(_selectedIndex),
```

追加した各ページの中身はCenterにTextを配置しただけ
```
import 'package:flutter/material.dart';

class SettingsPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(child: Center(child: Text('SettingsPage'),),);
  }
}
```

![Jan-24-2020 09-41-36](https://user-images.githubusercontent.com/11751495/73036123-cf73b900-3e8d-11ea-8e42-e6d108a01a07.gif)

