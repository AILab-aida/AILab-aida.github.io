---
title: flutter provider基础使用
categories: 移动端
tags:
  - iOS
  - Android
---

## main.dart

废话不多说 直接上代码 😃

```
import 'package:flutter/material.dart';
import 'package:flutter_demo/provider/main_provider.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(MaterialApp(
    title: 'demo',
    theme: ThemeData(
      primarySwatch: Colors.blue,
    ),
    //定义作用区间 只绘制顶层home
    home: MultiProvider(
      providers: [
        ChangeNotifierProvider(builder: (_) => MainProvider()),
      ],
      child: Home(),
    ),
  ));
}

class Home extends StatefulWidget {
  @override
  _HomeState createState() => new _HomeState();
}

class _HomeState extends State<Home> {
//  int curNum = 0;
  int curNum;

  @override
  void initState() {
    super.initState();
    //TODO
  }

  void add() {
    setState(() {
      curNum += 1;
    });
    //TODO
  }

  void minus() {
    setState(() {
      curNum -= 1;
    });
    //TODO
  }

  @override
  Widget build(BuildContext context) {
    //定义provider 实例化
    MainProvider provider = Provider.of<MainProvider>(context);
    curNum = provider.curNum;
    return new Scaffold(
      appBar: new AppBar(
        title: new Text('demo'),
      ),
      body: Column(
        children: <Widget>[
          Add(),
//           Add(
//             add: add,
//           ),
          Container(
            child: Text(
              '$curNum',
              style: TextStyle(fontSize: 30),
            ),
          ),
          Minus(),
          // Minus(
          //   minus: minus,
          // ),
        ],
      ),
    );
  }
}

class Minus extends StatelessWidget {
  const Minus({
    Key key,
    // this.minus,
  }) : super(key: key);
  // final int curNum;
  // final VoidCallback minus;
  @override
  Widget build(BuildContext context) {
    MainProvider provider = Provider.of<MainProvider>(context);
    return Container(
      child: Container(
        child: FlatButton(
          child: Text(
            '-',
            style: TextStyle(fontSize: 30),
          ),
          onPressed: () {
            provider.minus();
          },
        ),
      ),
    );
  }
}

class Add extends StatelessWidget {
  const Add({
    Key key,
    // this.add,
  }) : super(key: key);
  // final int curNum;
  // final VoidCallback add;
  @override
  Widget build(BuildContext context) {
    MainProvider provider = Provider.of<MainProvider>(context);
    return Container(
      child: Container(
        child: FlatButton(
          child: Text(
            '+',
            style: TextStyle(fontSize: 30),
          ),
          onPressed: () {
            provider.add();
          },
        ),
      ),
    );
  }
}
```

## main_provider.dart

废话不多说 直接上代码 😃

```
import 'package:flutter/material.dart';

//定义作用区间 状态管理与界面抽离 祖先 父 子 孙子 统一操作数据
class MainProvider extends ChangeNotifier {
  int curNum = 0;
  add() {
    curNum += 1;
    notifyListeners();
  }

  minus() {
    curNum -= 1;
    notifyListeners();
  }
}

```
