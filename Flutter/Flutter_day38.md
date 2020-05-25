
復活

## やったこと
- SilverAppBar
- BackdropFilter


##  SilverAppBar
[SliverList & SliverGrid (Flutter Widget of the Week) - YouTube](https://youtu.be/ORiTTaVY6mM)

### Sample

![May-26-2020 08-16-40](https://user-images.githubusercontent.com/11751495/82847819-3a5ffa00-9f2b-11ea-89e7-dc4ea8ef14ee.gif)

### Code

```

class ProfileNewPageState extends State<ProfileNewPage> {

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: CustomScrollView(
        slivers: <Widget>[
          SliverAppBar(
            expandedHeight: 200.0,
            floating: false,
            pinned: true,
            flexibleSpace: FlexibleSpaceBar(
              centerTitle: true,
              title: Text(
                "SliverAppBar",
                style: TextStyle(
                  color: Colors.white,
                  fontSize: 16.0,
                ),
              ),
              background: Image.network(
                      “https://images.pexels.com/photos/1020315/pexels-photo-1020315.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260”,
                      fit: BoxFit.cover,
                    ),
            ),
          ),
          SliverGrid(
              gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
                crossAxisCount: 5,
              ),
              delegate: SliverChildBuilderDelegate(
                    (BuildContext context, int index) {
                  return Center(
                    child: Text(
                      'Item $index',
                    ),
                  );
                },
                childCount: 20,
              )
          ),
          SliverToBoxAdapter(
            child: Container(
              height: 100,
              color: Colors.redAccent,
              child: Center(
                child: Text(
                  'SliverToBoxAdapter',
                  style: TextStyle(
                      fontSize: 20,
                      fontWeight: FontWeight.bold
                  ),
                ),
              ),
            ),
          ),
          SliverList(
            delegate: SliverChildBuilderDelegate(
                  (context, index) => ListTile(
                title: Text(
                  "List Item $index",
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

### Doc
[SliverList class - widgets library - Dart API](https://api.flutter.dev/flutter/widgets/SliverList-class.html)
[SliverAppBar | Flutter Doc JP](https://flutter.ctrnost.com/basic/navigation/sliverappbar/)
[SliverGrid class - widgets library - Dart API](https://api.flutter.dev/flutter/widgets/SliverGrid-class.html)
[SliverToBoxAdapter class - widgets library - Dart API](https://api.flutter.dev/flutter/widgets/SliverToBoxAdapter-class.html)

## BackdropFilter
[BackdropFilter (Flutter Widget of the Week) - YouTube](https://youtu.be/dYRs7Q1vfYI)

### Sample


![May-26-2020 08-25-10](https://user-images.githubusercontent.com/11751495/82847860-71cea680-9f2b-11ea-8de6-3da82a168d45.gif)

### Code

```
background: Stack(
  children: <Widget>[
    Positioned.fill(
      child: Image.network(
        “https://images.pexels.com/photos/1020315/pexels-photo-1020315.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260”,
        fit: BoxFit.cover,
      ),
    ),
    Positioned.fill(
      child: BackdropFilter(
          filter: ImageFilter.blur(
              sigmaX: 5.0,
              sigmaY: 5.0
          ),
          child: Container(
            color: Colors.black.withOpacity(0.0),
          )
      ),
    )
  ],
),
```

### Code (& Slider)

```
class ProfileNewPageState extends State<ProfileNewPage> {

  double sigma = 0.0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: CustomScrollView(
        slivers: <Widget>[
          SliverAppBar(
            expandedHeight: 200.0,
            floating: false,
            pinned: true,
            flexibleSpace: FlexibleSpaceBar(
              centerTitle: true,
              title: Text(
                "SliverAppBar",
                style: TextStyle(
                  color: Colors.white,
                  fontSize: 16.0,
                ),
              ),
              background: Stack(
                children: <Widget>[
                  Positioned.fill(
                    child: Image.network(
                      "https://images.pexels.com/photos/1020315/pexels-photo-1020315.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260",
                      fit: BoxFit.cover,
                    ),
                  ),
                  Positioned.fill(
                    child: BackdropFilter(
                        filter: ImageFilter.blur(
                            sigmaX: sigma,
                            sigmaY: sigma
                        ),
                        child: Container(
                          color: Colors.black.withOpacity(0.0),
                        )
                    ),
                  )
                ],
              ),
            ),
          ),
          SliverGrid(
              gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
                crossAxisCount: 5,
              ),
              delegate: SliverChildBuilderDelegate(
                    (BuildContext context, int index) {
                  return Center(
                    child: Text(
                      'Item $index',
                    ),
                  );
                },
                childCount: 20,
              )
          ),
          SliverToBoxAdapter(
            child: Container(
              height: 100,
              child: Center(
                child: Slider(
                  min: 0,
                  max: 10,
                  value: sigma,
                  divisions: 100,
                  onChanged: (value) {
                    setState(() {
                      sigma = value;
                    });
                  },
                )
              ),
            ),
          ),
          SliverList(
            delegate: SliverChildBuilderDelegate(
                  (context, index) => ListTile(
                title: Text(
                  "List Item $index",
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


### Doc
[BackdropFilter class - widgets library - Dart API](https://api.flutter.dev/flutter/widgets/BackdropFilter-class.html)
