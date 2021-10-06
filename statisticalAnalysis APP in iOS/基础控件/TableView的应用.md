# TableView的应用

## 什么是 TableView?

`TableView` 直译为表格视图，如今我们手机上的各种 app 都存在着表格视图:当我们打开知乎时，首先看到的就是一个 `TableView`，首页上的每一个回答都是 `TableView` 中的一个 `cell`，只不它是一种自定义的表格视图；当我们在淘宝搜索栏中搜索某一关键词后，屏幕上出现的也是`TableView`，每一个商品都是`TableView`上的一个`cell`；当我们打开微信想找某 个对话框时，对话框也是 `TableView` 上的 `cell`。通过本章以及下一章的学习，你将学习如何做出联系人列表，以及如何构建基本的表格视图界面。当然，仅有`TableView` 是不够的，在下一章结束后，你将掌握更多的技能。



## 数据源代理

`UITableView` 继承自 `UIScrollView`，在进行 `ViewController` 编辑时，有如下两种方法对其进行代理：

- 第一种

  1. 将鼠标右键将 `UITableViewDataSource` 与 `ViewController` 相连进行代理

  2. ```swift
     class ViewController: UIViewController,UITableViewDataSource {}
     ```

- 第二种

  1. 拖拽 `UITableView` 至代码中

  2. 在 `viewDidLoad()` 中：

     ```swift
     super.viewDidLoad()
     self.tableView.dataSource = (self as UITableViewDataSource)
     ```

     

## TableView 的基本属性

完成代理后，代码部分需要设置 `UITableView` 的各项参数，与 `ScrollView `不同的是，`TableView` 存在两个必须继承的方法：

1. ```swift
   func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
     return 1
   }
   ```

2. ```swift
   func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
     code
   }
   ```

上述内容中，前者为每一个 section 有多少个 rows，后者为对每个 rows 进行属性设置，

下一章中我会对 rows 中的属性进行详细说明，本章仅探讨 `TableView` 的一些性质。除了这两个必须继承的方法外，`TableView` 还有一个十分重要的内容：设置 section 数量。若想显示不同分组，需要我们手动添加一个方法，否则只显示第一组内的单元格(注:分组显示需要在 storyboard 中设置Grouped)：

```swift
func numberOfSections(in tableView: UITableView) -> Int { 
  return 1
}
```

若不设置此方法，return 默认值为 1，`TableView` 中除了上述的三个方法外，还有如下的几个属性：

```swift
rowHeight//统一设置所有行高度
separatorColor//分割线颜色 
separatorStyle//分割线样式
tableHeaderView//可在分组单元格上方放置 
title tableFooterView//可以用来显示加载更多页面
```



## 国家分组 demo

接下来以一个国家分组 demo 练习表格视图的分组：

```swift
func numberOfSections(in tableView: UITableView) -> Int {
  //一共分几组，若没有此则默认为 1 section，不会显示出了第一个以外的 section
  return 3 
}

func tableView(_ tableView: UITableView, titleForHeaderInSection section: Int) -> String? {
  //组标题，即页眉
  if section == 0{ 
    return "亚洲"
  }else if section == 1{ 
    return "非洲"
  }else {
    return "欧洲"
  }
}

func tableView(_ tableView: UITableView, titleForFooterInSection section: Int) -> String? {
  //组注释，即页尾
  if section == 0{ 
    return "Asia"
  }else if section == 1{ 
    return "Africa"
  }else {
    return "Euro"
  } 
}

func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
  if section == 0{ 
    //亚洲
    return 3
  }else if section == 1{
    //非洲
    return 2 
  }else {
    //欧洲
    return 1 
  }
}

func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
  let cell = UITableViewCell.init(style: UITableViewCell.CellStyle.default, reuseIdentifier: nil)
  if indexPath.section == 0 { //亚洲
    if indexPath.row == 0 { 
      cell.textLabel?.text = "中国"
    }else if indexPath.row == 1{
      cell.textLabel?.text = "日本"
    }else if indexPath.row == 2{ 
      cell.textLabel?.text = "韩国"
    }
    
  }else if indexPath.section == 1 {
    //非洲
    if indexPath.row == 0{ 
      cell.textLabel?.text = "南非"
    }else {
      cell.textLabel?.text = "坦桑尼亚"
    }
  
  }else {
    cell.textLabel?.text = "英国"
  }
  return cell 
}
```

值得注意的是，如果我们在工程文件中大量套用if else函数会导致性能大大下降，该部分仅为演示时使用，在下一章中我们会集中探讨如何通过数组来定义 `cell`。

