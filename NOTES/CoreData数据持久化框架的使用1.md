学会使用`CoreData`数据持久化框架搭建一个简单的`ToDo`待办事项`App`。

![12.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fb6aae64afb841518db7052cddc48513~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

之前的学习中构建过[[List]]列表和`SwipeCard`卡片，我们发现如果我们重新启动模拟器，它的数据会恢复原始数组的数据。这是因为每次打开`App`的时候，系统会根据数据源重新遍历数据，当用户关闭应用程序并重新启动时，所有数据都“`消失`”了。

本章我们学习一个新的框架，叫做`CoreData`，它一个管理数据对象的框架，可以将我们的数据保存起来，这样每当我们重新打开`App`的时候，`App`展示的就是我们上一次操作的数据。

值得注意的一点是，`CoreData`可不是数据库哦，它只是一个用于开发人员`管理和存储数据持久化`的交互框架，它的持久存储并`不局限于`数据库。

首先，创建一个新项目，命名为`SwiftUICoreData`，请注意，这里我们需要勾选使用`CoreData`。

![2.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/18c9b30e60fe4feb88d6535975d2bb69~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

## CoreData框架数据持久化实现原理

我们发现，和以往创建的`App`不同，这次多了几个文件。

一个是`SwiftUICoreData.xcdatamodeld`文件，它是管理整个项目生成的对象模型的，是定义`实体与持久存储交互`的文件。

另一个是`Persistence.swift`文件，它是`数据保存到持久存储区`的文件。

![3.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ff7c6468b2d94ac0ab25f8a9372520b9~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

`SwiftUI`通过将管理对象上下文`viewContext`注入到环境中，来实现在`任何视图`都可以`检索`上下文，并且能够`管理数据`。

我们再看一下`SwiftUICoreDataApp.swift`文件，可以看到它定义了一个常量`persistenceController`来保存`PersistenceController`的实例，并在`ContentView`主视图中将托管对象上下文`viewContext`注入到环境中。

![4.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f3c7d94863504bb19a0d74987433ebb6~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

上面我们看到已经在管理对象模型中创建实体了，并且定义一个继承自`NSManagedObject`的管理对象来与实体关联。

我们回到`ContentView.swift`文件，可以看到系统生成了一堆的`示例代码`，让我们解读一下。

首先使用了`@Environment`环境变量从环境中获取托管对象上下文`viewContext`：

```swift
@Environment(\.managedObjectContext) var context
```

然后创建管理对象，并使用`context`上下文的`save`方法将对象添加到`数据库`中：

```swift
//示例代码
let task = ToDoItem(context: context)

task.id = UUID()
task.name = name
task.priority = priority
task.isCompleted = isCompleted
复制代码
```

在`数据检索`方面，我们引入了一个名为`@FetchRequest`的属性包装器，用于从持久存储中获取数据。它可以指定要检索的实体对象以及数据的排序方式，然后，`CoreData`框架就可以将使用`@Environment`环境的托管对象上下文`context`来获取数据。

```
@FetchRequest(
    sortDescriptors: [NSSortDescriptor(keyPath: \Item.timestamp, ascending: true)],animation: .default)
    private var items: FetchedResults<Item>
复制代码
```

好了，以上就是`CoreData`框架数据持久化实现的原理，我们可以预览下系统提供的例子。

![5.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a3b61a2bb972456998a4e1f7acb7713e~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

下面，让我们进入正题。

## ToDoItem类准备

首先，我们需要定义一个模型类，我们可以创建一个新的文件，点击`Xcode`顶部导航栏，`File`文件，`New`新建，选择`File`创建文件，选择`iOS`中的`Swift File`类型的文件，命名为`ToDoItem.swift`。

然后我们构建需要`App`需要的参数。

我们先构建一个枚举类型`Priority`，来表示我们任务的优先级，分别是低、中、高、最高，用数值`Int`类型表示权重。

```
//任务紧急程度的枚举
enum Priority: Int {
    case low = 0
    case normal = 1
    case high = 2
}
复制代码
```

然后定义一个类`ToDoItem`遵循`ObservableObject`可被观察对象协议和`Identifiable`可被识别协议，在`ToDoItem`类里面有三个参数：`name`名称、`priority`优先级、`isCompleted`是否完成。并且在`ObservableObject`协议需要使用`@Published`定义，这样才能在参数改变的时候检测到`变化`。

至于遵循`Identifiable`协议就不用说了，我们定义`id`作为每一个任务项的`唯一标识符`，这样即便是相同名称、相同优先级的任务，系统也不会把它们作为同一个，这个我们之前的章节讲过。

```
//ToDoItem遵循ObservableObject协议
class ToDoItem: ObservableObject, Identifiable {
    var id = UUID()
    @Published var name: String = ""
    @Published var priority: Priority = .high
    @Published var isCompleted: Bool = false

    //实例化
    init(name: String, priority: Priority = .normal, isCompleted: Bool = false) {
        self.name = name
        self.priority = priority
        self.isCompleted = isCompleted
    }
}
复制代码
```

我们回到`ContentView.swift`文件，我们看看需要做哪些东西。

## TopBarMenu顶部导航栏

首先是`TopBarMenu`顶部导航栏，比较简单，在这里就不赘述了。

```
//顶部导航栏
struct TopBarMenu: View {
    var body: some View {

        HStack {
            Text("待办事项")
                .font(.system(size: 40, weight: .black))

            Spacer()

            Button(action: {

            }) {
                Image(systemName: "plus.circle.fill")
                    .font(.largeTitle).foregroundColor(.blue)
            }
        }
        .padding()
    }
}
复制代码
```

![6.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/18c677b1acb04ccb912fe4c5a099c7a6~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

中间的内容部分，我们可以看到有两种情况，一种是没有数据的时候，我们展示一张`Image`图片，另一种是有数据的时候，展示`List`数据列表。

## NoDataView缺省页

我们导入一张图片，命名叫做`image01`，然后构建第一种空数据的情况，业务上常常叫做缺省页的图。

```
//缺省图
struct NoDataView: View {
    var body: some View {
    
        Image("image01")
            .resizable()
            .scaledToFit()
    }
}
复制代码
```

![7.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5f3013d42bfc49e692eacdb33bb5f777~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

如果`List`列表有数据的时候，我们需要展示列表数据，接下来，我们完成下`List`的创建。

## ToDoListView列表页创建

之前的章节我们了解过`List`列表的创建方式，这里我们先构建单个任务项`ToDoListRow`视图的样式，然后使用`List`列表+`ForrEach`循环的方法构建整个列表`ToDoListView`。

```
// 列表
struct ToDoListView: View {

    @Binding var todoItems: [ToDoItem]

    var body: some View {
    
        List {
            ForEach(todoItems) { todoItem in
                ToDoListRow(todoItem: todoItem)
            }
        }
    }
}

// 列表内容
struct ToDoListRow: View {

    @ObservedObject var todoItem: ToDoItem

    var body: some View {
    
        Toggle(isOn: self.$todoItem.isCompleted) {
            HStack {

                Text(self.todoItem.name)
                    .strikethrough(self.todoItem.isCompleted, color: .black)
                    .bold()
                    .animation(.default)

                Spacer()

                Circle()
                    .frame(width: 20, height: 20)
            }
        }
    }
}
复制代码
```

![8.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0ac71bb8489340c890d4f0cf7ad3860e~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

我们在`ToDoListView`列表视图使用`@Binding`(图中有误)声明了一个`todoItems`状态，用来存储`ToDoItem`数组，当数据变化时就刷新页面。

```
//ContentView视图

VStack {
    TopBarMenu()
    ToDoListView(todoItems: $todoItems)
}
复制代码
```

然后我们在`ToDoListRow`视图使用`@ObservableObject`声明了一个`todoItem`，用来引用定义好的实例化方法。

对于`ToDoListRow`单个任务项的视图，里面也比较简答，我们用了一个`Toggle`开关作为复选框，再加上一个`Text`文字作为待办事项的内容标题，最后我们还用了一个`Circle`圆形的形状，作为`priority`标识。

`priority`标识我们可以定义一个私有的颜色方法，当我们从`Priority`枚举类型中获得不同状态时，返回不同的颜色，比如`优先级高`显示`红色`，`一般优先级`显示`橘色`，`低优先级`显示`绿色`。

```
// 根据优先级显示不同颜色
private func color(for priority: Priority) -> Color {

    switch priority {
        case .high:
            return .red
        case .normal:
            return .orange
        case .low:
            return .green
        }
    }
复制代码
```

定义好方法后，我们将`Circle`圆形赋予背景颜色，颜色值调用`priority`定义颜色方法。

```
.foregroundColor(self.color(for: self.todoItem.priority))
复制代码
```

然后对于`Toggle`开关，我们希望用的是`checkbox`复选框的样式，还记得之前的章节中我们用`ButtonStyle`修改`Button`按钮的样式么？

是的，`Toggle`开关也支持自定义样式的方式，我们可以用`ToggleStyle`开关样式把`Toggle`开关变成`checkbox`复选框。

```
// checkbox复选框样式
struct CheckboxStyle: ToggleStyle {
    func makeBody(configuration: Self.Configuration) -> some View {
        return HStack {
        
            Image(systemName: configuration.isOn ? "checkmark.circle.fill" : "circle")
                .resizable()
                .frame(width: 24, height: 24)
                .foregroundColor(configuration.isOn ? .purple : .gray)
                .font(.system(size: 20, weight: .bold, design: .default))
                .onTapGesture {
                    configuration.isOn.toggle()
                }
            configuration.label
        }
    }
}
复制代码
```

然后，我们给`Toggle`开关添加`.toggleStyle`开关样式修饰符就可以将自定义好的样式加到里面了。

```
.toggleStyle(CheckboxStyle())
复制代码
```

![9.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/194be32856be482c84a182a4d8bb2c37~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

以上，我们完成了空的列表`NoDataView`缺省页，还有有数据时的列表`ToDoListView`待办事项列表，当然现在`ToDoListView`待办事项列表还没有数据，别急，我们慢慢来。

## 页面展示逻辑判断

那么什么时候展示`NoDataView`缺省页视图，什么时候展示`ToDoListView`待办事项列表视图呢？

当然是`todoItems`没有数据的时候展示`NoDataView`缺省页视图，`todoItems`有数据的时候展示`ToDoListView`待办事项列表视图。

我们就可以把这个判断加到`ContentView`主视图里面。

```
if todoItems.count == 0 {
    NoDataView()
}
复制代码
```

最后，在`ContentView`主视图布局部分，我们将`TopBarMenu`顶部导航栏、`ToDoListView`待办事项列表用`VStack`垂直排布在一起，然后使用`ZStack`层叠视图将`NoDataView`缺省页视图包裹在一起看看效果。

```
//主视图
struct ContentView: View {

    @State var todoItems: [ToDoItem] = []

    var body: some View {

        ZStack {
            VStack {
                TopBarMenu()
                ToDoListView()
            }

            if todoItems.count == 0 {
                NoDataView()
            }
        }
    }
}
复制代码
```

![10.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5ee5c12b17e444bdb1d792b91ce19cf0~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

嗯？为啥`List`列表会有背景颜色？这是`iOS14`的新特性，如果我们需要去掉这个颜色，需要再做一下处理，在视图加载的时候，将`TableView`列表和`TableViewCell`列表项的背景颜色变成无填充颜`.clear`。

```
//去掉Listb背景颜色

init() {
    UITableView.appearance().backgroundColor = .clear
    UITableViewCell.appearance().backgroundColor = .clear
}
复制代码
```

这样，我们就完成了列表展示页的制作。

![11.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bee502c4527e437898f619f538a03109~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

由于章节篇幅太长，将分为上下两章来写，上半部分先完成主要页面的构建，下半部分我们再完成`NewToDoView`新增任务项页面和基于`CoreData`框架数据持久化的逻辑部分。

本章完整代码如下：

```
//ToDoItem.swift

import Foundation

enum Priority: Int {
    case low = 0
    case normal = 1
    case high = 2
}

class ToDoItem: ObservableObject, Identifiable {
    var id = UUID()
    @Published var name: String = ""
    @Published var priority: Priority = .high
    @Published var isCompleted: Bool = false

    init(name: String, priority: Priority = .normal, isCompleted: Bool = false) {
        self.name = name
        self.priority = priority
        self.isCompleted = isCompleted
    }
}
复制代码
```

```
//ContentView.swift

import CoreData

import SwiftUI

struct ContentView: View {

    @State var todoItems: [ToDoItem] = []

    //去掉Listb背景颜色
    init() {
        UITableView.appearance().backgroundColor = .clear
        UITableViewCell.appearance().backgroundColor = .clear
    }

    var body: some View {

        ZStack {
            VStack {
                TopBarMenu()
                ToDoListView(todoItems: $todoItems)
            }

            if todoItems.count == 0 {
                NoDataView()
            }
        }
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}

// 顶部导航栏
struct TopBarMenu: View {
    var body: some View {

        HStack {
            Text("待办事项")
                .font(.system(size: 40, weight: .black))

            Spacer()

            Button(action: {

            }) {
                Image(systemName: "plus.circle.fill")
                    .font(.largeTitle).foregroundColor(.blue)
            }
        }
        .padding()
    }
}

// 缺省图
struct NoDataView: View {
    var body: some View {
        Image("image01")
            .resizable()
            .scaledToFit()
    }
}

// 列表
struct ToDoListView: View {

    @Binding **var** showNewTask: Bool

    var body: some View {

        List {
            ForEach(todoItems) { todoItem in
                ToDoListRow(todoItem: todoItem)
            }
        }
    }
}

// 列表内容
struct ToDoListRow: View {

    @ObservedObject var todoItem: ToDoItem

    var body: some View {

        Toggle(isOn: self.$todoItem.isCompleted) {
            HStack {

                Text(self.todoItem.name)
                    .strikethrough(self.todoItem.isCompleted, color: .black)
                    .bold()
                    .animation(.default)
                    
                Spacer()
                
                Circle()
                    .frame(width: 20, height: 20)
                    .foregroundColor(self.color(for: self.todoItem.priority))
            }
        }.toggleStyle(CheckboxStyle())
    }

    // 根据优先级显示不同颜色
    private func color(for priority: Priority) -> Color {
        switch priority {
        case .high:
            return .red
        case .normal:
            return .orange
        case .low:
            return .green
        }
    }
}

// checkbox复选框样式
struct CheckboxStyle: ToggleStyle {

    func makeBody(configuration: Self.Configuration) -> some View {
        return HStack {

            Image(systemName: configuration.isOn ? "checkmark.circle.fill" : "circle")
                .resizable()
                .frame(width: 24, height: 24)
                .foregroundColor(configuration.isOn ? .purple : .gray)
                .font(.system(size: 20, weight: .bold, design: .default))
                .onTapGesture {
                    configuration.isOn.toggle()
                }
            configuration.label
        }
    }
}
复制代码
```

快来动手试试吧！

**如果本专栏对你有帮助，不妨点赞、评论、关注～**
