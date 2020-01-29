# TabBar

To create tabs layout, use a `DefaultTabController` is the most easy way:

```dart
DefaultTabController(
            length: 3,
            child: Scaffold(
                body: Column(
              children: <Widget>[
                  color: Colors.indigoAccent,
                  child: TabBar(
                      labelColor: Colors.white,
                      indicatorColor: Colors.red,
                      tabs: [
                        Tab(
                          text: 'sliver list',
                        ),
                        Tab(text: 'grid'),
                        Tab(text: 'lazily')
                      ]),
                ),
                Expanded(
                  child: TabBarView(
                    children: <Widget>[
                      Tab3List(),
                      Tab3List(),
                      Tab3List(),
                    ],
                  ),
                )
              ],
            ))
            )
```

## keep tab page state

When switch between the tabs, the active tab page will be re-rendered.
If we want to keep the state of tab page, we can extract the page to a new
class and implements `AutomaticKeepAliveClientMixin` mixin:

```dart
class _Tab3State<Tab3List> extends State with AutomaticKeepAliveClientMixin {
  @override
  // TODO: implement wantKeepAlive
  bool get wantKeepAlive => true;

  @override
  Widget build(BuildContext context) {
    super.build(context);
    // TODO: implement build
    return CustomScrollView(
      slivers: <Widget>[
        SliverList(
          delegate: SliverChildBuilderDelegate(
              (context, index) => createListTile(index.toString())),
        )
      ],
    );
  }
}
```
