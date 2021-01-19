## 自定义底部导航，支持角标

>原插件好长时间不在更新维护，自己fork了份并修复了一些问题

##
![bottomtabbar](/screenshot.png){width="400px"}

# BottomTabBar
    和官方BottomNavigationBar类似，只是加入了一些小特性，特别是角标

### items : ```List<BottomTabBarItem>```
    BottomTabBar 底部导航栏中，其中每个BottomTabBarItem都有一个图标和标题。

###  onTap  : ```ValueChanged<int>```
    BottomTabBar 点击事件，返回当前索引index

###  currentIndex  : ```int```
    BottomTabBar 当前选中索引

### type  : ```BottomTabBarType ```
    BottomTabBar 显示模式，可选值BottomTabBarType.fixed、BottomTabBarType.shifting

### fixedColor  : ```Color ```
    仅当type为BottomTabBarType.fixed时有效,作用于选中颜色
    当值为null 则默认主题primary颜色[ThemeData.primaryColor]，
    
### iconSize : ```double```
    icon尺寸大小

### [新增] isAnimation : ```bool```
    点击tabbar是否显示动画，默认true

### [new]  isInkResponse : ```bool```
    点击tabbar是否显示反馈，默认true

# BottomTabBarItem 
    BottomTabBarItem主要选项

### [新增]  badgeNo : ```String```
    角标显示的文本

### [新增]  badgeColor : ```Color```
    角标背景颜色, 默认 fixedColor

### [新增]  badge : ```Widget```
    自定义角标


## 如何使用?

在pubspec.yaml导入依赖

```
dependencies:
  flutter:
    sdk: flutter
  bottom_tab_bar:
    git: https://github.com/error-code/flutter_bottom_tab_bar.git

```

使用示例:

```
import 'package:bottom_tab_bar/bottom_tab_bar.dart';

class HomeState extends State<Home> with SingleTickerProviderStateMixin {
  TabController _tabController;
  int _selectedIndex = 1;
  String badgeNo1;
  var titles = ['home', 'video', 'find', 'smallvideo', 'my'];
  var icons = [
    Icons.home,
    Icons.play_arrow,
    Icons.child_friendly,
    Icons.fiber_new,
    Icons.mic_none
  ];
  @override
  void initState() {
    super.initState();
    _tabController =
        new TabController(vsync: this, initialIndex: 1, length: titles.length);
    badgeNo1 = '12';
  }

  void _onItemSelected(int index) {
    setState(() {
      _selectedIndex = index;
      badgeNo1 = '';
    });
  }

  final _widgetOptions = [
    Text('Index 0: Home'),
    Text('Index 1: Video'),
    Text('Index 2: find someone'),
    Text('Index 3: small Video'),
    Text('Index 4: My'),
  ];
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Bottom Tab Bar'),
        actions: <Widget>[new Icon(Icons.photo_camera)],
      ),
      bottomNavigationBar: BottomTabBar(
        items: <BottomTabBarItem>[
          BottomTabBarItem(
              icon: Icon(icons[0]), title: Text(titles[0]), badgeNo: badgeNo1),
          BottomTabBarItem(icon: Icon(icons[1]), title: Text(titles[1])),
          BottomTabBarItem(icon: Icon(icons[2]), title: Text(titles[2])),
          BottomTabBarItem(
              icon: Icon(icons[3]),
              activeIcon: Icon(icons[3]),
              title: Text(titles[3])),
          BottomTabBarItem(icon: Icon(icons[4]), title: Text(titles[4])),
        ],
        fixedColor: Colors.blue,
        currentIndex: _selectedIndex,
        onTap: _onItemSelected,
        type: BottomTabBarType.fixed,
        isAnimation: false,
        isInkResponse: false,
        badgeColor: Colors.green,
      ),
      body: Center(
        child: _widgetOptions.elementAt(_selectedIndex),
      ),
    );
  }
}

```

