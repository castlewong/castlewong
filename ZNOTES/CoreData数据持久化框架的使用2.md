
> 今日职言：外表干净是尊重别人，内心干净是尊重自己，言行干净是尊重灵魂。

承接上一章的内容，我们继续完成使用`CoreData`框架搭建一个简单的`ToDo`待办事项`App`。

这一章节，我们完成一下`NewToDoView`新建事项页面。

![1.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/45f62a86503542bb864462f4586ffcf8~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

我们先新建一个新页面，命名为`NewToDoView`。

点击`Xcode`顶部导航栏，`File`文件，`New`新建，选择`File`创建文件，选择`iOS`中的`SwiftUI File`类型的文件，命名为`NewToDoView.swift`。

![2.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ebe40d4aa6cc458b99ca7281e4080394~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

## 页面UI设计

我们还是从上往下构建`UI`页面。

### TopNavBar顶部导航栏视图

![3.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a3b92c99eb9840e3be0a63c7ab4b9fde~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

首先是`TopNavBar`顶部导航栏，名称不能和之前创建的重复，它由一个`Text`标题一个`closeButton`关闭按钮组成。

```
// 顶部导航栏
struct TopNavBar: View {
    var body: some View {

        HStack {
            Text("新建事项")
                .font(.system(.title))
                .bold()

            Spacer()

            Button(action: {

            }) {
                Image(systemName: "xmark.circle.fill")
                    .foregroundColor(.gray)
                    .font(.title)
            }
        }
    }
}
复制代码
```

![4.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b709fcba6b504214ac323f04e97f1b86~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

### InputNameView输入框视图

然后是事项名称的输入框`TextField`。

`TextField`输入框需要有两个参数绑定，一个是内容绑定，即我们`TextField`输入框需要记录什么内容。第二个是`isEditing`输入状态绑定，帮助我们检测它是否正在输入，后面我们会用到输入的状态的检测。

我们在`NewToDoView`视图中，使用`@State`声明两个变量。

```
@State var name: String
@State var isEditing = false
复制代码
```

然后我们再构建`InputNameView`输入框视图的内容，再绑定参数。

```
//输入框
struct InputNameView: View {

    @Binding var name: String
    @Binding var isEditing: Bool

    var body: some View {

        TextField("请输入", text: $name, onEditingChanged: { (editingChanged) in

            self.isEditing = editingChanged

        })
            .padding()
            .background(Color(.systemGray6))
            .cornerRadius(8)
            .padding(.bottom)
    }
}
复制代码
```

最后在`NewToDoView`视图中展示`InputNameView`输入框视图的内容，这里用`VStack`垂直排布将`InputNameView`输入框视图和`TopNavBar`顶部导航栏排在一起。

```
VStack {
    TopNavBar()
    InputNameView(name: $name, isEditing: $isEditing)
}
复制代码
```

由于我们`NewToDoView`视图需要预览，因此要想在模拟器中看到效果，还需要在`NewToDoView_Previews`预览视图中添加参数。

运行一下，我们看下效果。

![5.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9fea1411fef74790a24dbe0495d18927~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

下面我们继续，接下来是事项的优先级选择，我们先完成`UI`的部分。

### PrioritySelectView优先级选择视图

我们命名一个`PrioritySelectView`优先级选择视图，这里当然也可以用代码整合的方式减少下代码量，我们将相同的修饰符抽离出来，然后再在`PrioritySelectView`优先级选择视图展示内容。

```
// 选择优先级
struct PrioritySelectView: View {
    var body: some View {

        HStack {
            PrioritySelectRow(name: "高", color: Color.red)
            PrioritySelectRow(name: "中", color: Color.orange)
            PrioritySelectRow(name: "低", color: Color.green)
        }
    }
}

// 选择优先级
struct PrioritySelectRow: View {

    var name: String
    var color:Color

    var body: some View {
    
        Text(name)
            .frame(width: 80)
            .font(.system(.headline))
            .padding(10)
            .background(color)
            .foregroundColor(.white)
            .cornerRadius(8)
    }
}
复制代码
```

我们把`PrioritySelectView`加到`NewToDoView`视图中看下效果。

```
VStack {
    TopNavBar()
    InputNameView(name: $name, isEditing: $isEditing)
    PrioritySelectView()
}
复制代码
```

![6.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f6517c94e5ef402481985a3b9e452092~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

### SaveButton保存按钮视图

接下来是`SaveButton`保存按钮的绘制，我们让按钮下面留点底边距。

我们也加进去`NewToDoView`视图看看效果。

```
// 保存按钮
struct SaveButton: View {
    var body: some View {

        Button(action: {

        }) {

            Text("保存")
                .font(.system(.headline))
                .frame(minWidth: 0, maxWidth: .infinity)
                .padding()
                .foregroundColor(.white)
                .background(Color.blue)
                .cornerRadius(8)
        }
        .padding([.top,.bottom])
    }
}
复制代码
```

![7.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c49536bc89b84983b189e51b87c1eaf7~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

### NewToDoView页面位置调整

然后，我们调整下位置，我们希望这个`NewToDoView`页面是从底部弹出来，然后内容也都在底部展示而不是居中，我们可以调整下整个`NewToDoView`页面的位置。

我们用`VStack`和`Spacer`将`NewToDoView`视图顶到底部，然后根据`InputNameView`输入框是否处于输入状态`isEditing`，来进行偏移，也就是当我们点击`InputNameView`输入框正在输入的时候，整个视图可以向上移动，这样我们的`keyboard`键盘输入就有位置正对应了，这是一个`小技巧`。

然后整个`NewToDoView`页面页面我们再置底一点，使用`.edgesIgnoringSafeArea`安全区域空出底部区域，这样好看很多。

```
VStack {

    Spacer()

    VStack {
        TopNavBar()
        InputNameView(name: $name, isEditing: $isEditing)
        PrioritySelectView()
        SaveButton()
    }
    .padding()
    .background(Color.white)
    .cornerRadius(10, antialiased: true)
    .offset(y: isEditing ? -320 : 0)

}.edgesIgnoringSafeArea(.bottom)
复制代码
```

![8.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a0bebcfe1b23426aab22013095b38516~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

## 交互逻辑设计

好了，我们完成了`NewToDoView`页面的绘制了，下面是逻辑部分。

### PrioritySelectView优先级选择逻辑

首先是我们的`PrioritySelectView`优先级的选择，我们希望点击选择哪个优先级，哪个优先级就`“亮起”`，这样我们好知道`选中`的是哪一个。

![9.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f3ea791d987a4a139277a1c39d2ace41~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

同样，我们需要储存`priority`优先级状态，`priority`优先级是存储在`NewToDoView`新增事项页面里的，这里用`@State`状态。

```
//NewToDoView视图中定义
@State var priority: Priority
复制代码
```

然后，我们完善下`PrioritySelectView`优先级的选择页面，根据选中状态展示背景颜色，如果没选中，我们就变成`.systemGray4`灰色。

```
// 选择优先级
struct PrioritySelectView: View {

    @Binding var priority: Priority

    var body: some View {

        HStack {

            PrioritySelectRow(name: "高", color: priority == .high ? Color.red : Color(.systemGray4))
                .onTapGesture { self.priority = .high }

            PrioritySelectRow(name: "中", color: priority == .normal ? Color.orange : Color(.systemGray4))
                .onTapGesture { self.priority = .normal }

            PrioritySelectRow(name: "低", color: priority == .low ? Color.green : Color(.systemGray4))
                .onTapGesture { self.priority = .low }
        }
    }
}
复制代码
```

我们完善下`NewToDoView`视图的绑定关系，顺便给个`示例数据`预览下模拟器结果。

```
struct NewToDoView: View {

    @State var name: String
    @State var isEditing = false
    @State var priority: Priority

    var body: some View {

        VStack {

            Spacer()

            VStack {
                TopNavBar()
                InputNameView(name: $name, isEditing: $isEditing)
                PrioritySelectView(priority: $priority)
                SaveButton()
            }
            .padding()
            .background(Color.white)
            .cornerRadius(10, antialiased: true)
            .offset(y: isEditing ? -320 : 0)

        }.edgesIgnoringSafeArea(.bottom)
    }
}

struct NewToDoView_Previews: PreviewProvider {
    static var previews: some View {
        NewToDoView(name: "", todoItems: .constant([]), priority: .normal)
    }
}
复制代码
```

![10.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0342459ca00943a38ca4a0a65003dd8e~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

### 页面弹出逻辑

让我们回到`ContentView`首页，我们将两个页面`联动`起来。

![11.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1c8261401ab44b5e828ffe1e4aa0cb20~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

页面弹出的交互逻辑是，当我们点击`ContentView`首页右上角的添加按钮时，打开`NewToDoView`新增事项页面。

明白了逻辑之后，我们现在`ContentView`首页写逻辑，先声明一个变量`showNewTask`，表示我们是否打开了`NewToDoView`新增事项页面，默认是`false`。

```
@State private var showNewTask = false
@State private var offset: CGFloat = .zero    //使用.animation防止报错，iOS15的特性
复制代码
```

如果`showNewTask`状态为`true`时，我们显示`NewToDoView`新增事项页面，我们可以把`NewToDoView`新增事项页面放在`ContentView`首页的`ZStack`包裹着。

```
//点击添加时打开弹窗
if showNewTask {
    NewToDoView(name: "", priority: .normal)
        .transition(.move(edge: .bottom))
        .animation(.interpolatingSpring(stiffness: 200.0, damping: 25.0, initialVelocity: 10.0),value: offset)
    }
复制代码
```

然后我们增加点击事件，当我们在`ContentView`首页点击添加按钮的时候，`showNewTask`状态变为为`true`。

```
// 顶部导航栏
struct TopBarMenu: View {

    @Binding var showNewTask: Bool

    var body: some View {

        HStack {

            Text("待办事项")
                .font(.system(size: 40, weight: .black))

            Spacer()

            Button(action: {

                //打开弹窗
                self.showNewTask = true

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

```
//ContentView视图

TopBarMenu(showNewTask: $showNewTask)
复制代码
```

![12.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8ba485182dfe45eb9929e9a304dea8db~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

好像基本完成了效果，但由于我们是使用`ZStack`包裹的方式，而不是用`ModelView`模态弹窗或者 `NavigationView`导航栏进入新的页面，所以我们还需要做一个`MaskView`蒙层遮住背景，让它看起来像是`弹窗`的效果。

### MaskView蒙层逻辑

```
//蒙层
struct MaskView : View {

    var bgColor: Color

    var body: some View {

        VStack {

            Spacer()

        }
        .frame(minWidth: 0, maxWidth: .infinity, minHeight: 0, maxHeight: .infinity)
        .background(bgColor)
        .edgesIgnoringSafeArea(.all)
    }
}
复制代码
```

然后把`MaskView`蒙层加到打开`NewToDoView`新增事项页面的逻辑里，同时，支持我们点击`MaskView`蒙层关闭弹窗。

```
//蒙层
MaskView(bgColor: .black)
    .opacity(0.5)
    .onTapGesture {
        self.showNewTask = false
    }
复制代码
```

![13.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0a54ae2ac1274940830f115d939f390f~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

好！我们实现了怎么弹出`NewToDoView`新增事项页面，我们回到`NewToDoView.swift`文件，我们实现如何点击关闭弹窗。

### 页面关闭逻辑

在`NewToDoView`新增事项页面关闭有`两种`，一种是`点击关闭按钮`关闭弹窗。

```
// 顶部导航栏
struct TopNavBar: View {

    @Binding var showNewTask: Bool

    var body: some View {

        HStack {
            Text("新建事项")
                .font(.system(.title))
                .bold()

            Spacer()

            Button(action: {

                //关闭弹窗
                self.showNewTask = false
            }) {

                Image(systemName: "xmark.circle.fill")
                    .foregroundColor(.gray)
                    .font(.title)
            }
        }
    }
}
复制代码
```

```
//NewToDoView视图
struct NewToDoView: View {

    @State var name: String
    @State var isEditing = false
    @State var priority: Priority
    @Binding var showNewTask: Bool

    var body: some View {

        VStack {

            Spacer()

            VStack {
                TopNavBar(showNewTask: $showNewTask)
                InputNameView(name: $name, isEditing: $isEditing)
                PrioritySelectView(priority: $priority)
                SaveButton()
            }
            .padding()
            .background(Color.white)
            .cornerRadius(10, antialiased: true)
            .offset(y: isEditing ? -320 : 0)

        }.edgesIgnoringSafeArea(.bottom)
    }
}
复制代码
```

![14.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7628a57bb09e4901b9c91d3f17f3ca12~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

我们发现系统`报错`了，这是因为我们使用`@Binding`绑定了是否展示页面`showNewTask`的布尔值，还需要在`ContentView首页`建立关联。

```
//ContentView视图

NewToDoView(name: "", priority: .normal, showNewTask: $showNewTask)
复制代码
```

![15.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9d35cbee7c8146a4ba6e2c222d27a46d~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

这样，我们就`完成`了第一种关闭弹窗的交互：`点击关闭按钮`关闭弹窗。

另一种关闭弹窗的交互是，我们新建一个事项，满足条件后（内容不为空），这是我们点击`saveButton`保存按钮，`关闭弹窗`。

我们再回到`NewToDoView.swift`文件。首先我们保存要校验下`InputNameView`输入框内容是否`为空`，`为空`的时候我们`不关闭`弹窗。当`InputNameView`输入框内容`不为空`的时候，我们才允许`关闭弹窗`。

```
// 保存按钮
struct SaveButton: View {

    @Binding var name:String
    @Binding var showNewTask: Bool

    var body: some View {

        Button(action: {

            //判断输入框是否为空
            if self.name.trimmingCharacters(in: .whitespaces) == "" {
                return
            }

            //关闭弹窗
            self.showNewTask = false

        }) {

            Text("保存")
                .font(.system(.headline))
                .frame(minWidth: 0, maxWidth: .infinity)
                .padding()
                .foregroundColor(.white)
                .background(Color.blue)
                .cornerRadius(8)
        }
        .padding([.top,.bottom])
    }
}
复制代码
```

```
//NewToDoView视图

SaveButton(name: $name, showNewTask: $showNewTask)
复制代码
```

我们回到`ContentView.swift`文件中，运行模拟器体验下。

我们完成了基础的关闭弹窗操作，可以点击关闭按钮关闭，也可以输入新建事项后，点击保存关闭弹窗。

![16.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/27fa3746eb324d7fa4150614f7f9c538~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

### 添加新事项逻辑

我们在`NewToDoView`添加完事项后，输入的`内容`和选择的`优先级`就会在`ContentView`首页`List`列表中创建一条数据，下面我们来完成添加新事项逻辑。

![17.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6b24af63859b4e5aac60272279e171fa~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

我们看回`NewToDoView.swift`文件，我们实现了有输入内容时，点击保存按钮关闭弹窗，但没有实现`addTask`新增数据，下面我们来实现它。

```
// 保存按钮
struct SaveButton: View {

    @Binding var name:String
    @Binding var showNewTask: Bool
    @Binding var todoItems: [ToDoItem]
    @Binding var priority:Priority

    var body: some View {

        Button(action: {

            //判断输入框是否为空
            if self.name.trimmingCharacters(in: .whitespaces) == "" {
                return
            }

            //添加一条新数据
            self.addTask(name: self.name, priority: self.priority)

            //关闭弹窗
            self.showNewTask = false

        }) {

            Text("保存")
                .font(.system(.headline))
                .frame(minWidth: 0, maxWidth: .infinity)
                .padding()
                .foregroundColor(.white)
                .background(Color.blue)
                .cornerRadius(8)
        }
        .padding([.top,.bottom])
    }

    //添加新事项方法
    private func addTask(name: String, priority: Priority, isCompleted: Bool = false) {

        let task = ToDoItem(name: name, priority: priority, isCompleted: isCompleted)
        todoItems.append(task)
    }
}
复制代码
```

我们定义一个`addTask`添加事项的`private`私有方法，添加的参数是`name`内容、`priority`优先级、`isCompleted`是否完成，默认为否`false`。然后实例化它，调用方法的时候在 `todoItems`数组中增加一条数据。然后，我们点击`SaveBotton`保存成功时调用`addTask`添加新事项方法。

```
//NewToDoView视图

struct NewToDoView: View {

    @State var name: String
    @State var isEditing = false
    @State var priority: Priority
    @Binding var showNewTask: Bool
    @Binding var todoItems: [ToDoItem]

    var body: some View {

        VStack {

            Spacer()

            VStack {
                TopNavBar(showNewTask: $showNewTask)
                InputNameView(name: $name, isEditing: $isEditing)
                PrioritySelectView(priority: $priority)
                SaveButton(name: $name, showNewTask: $showNewTask, todoItems: $todoItems, priority: $priority)
            }
            .padding()
            .background(Color.white)
            .cornerRadius(10, antialiased: true)
            .offset(y: isEditing ? -320 : 0)

        }.edgesIgnoringSafeArea(.bottom)
    }
}

struct NewToDoView_Previews: PreviewProvider {
    static var previews: some View {
        NewToDoView(name: "", priority: .normal, showNewTask: .constant(true), todoItems: .constant([]))
    }
}
复制代码
```

同时，我们在`NewToDoView`视图绑定关联关系，并在`NewToDoView_Previews`预览视图中也绑定好关系。

当然别忘了，还要在 `ContentView`首页视图绑定参数。

```
// ContentView视图

NewToDoView(name: "", priority: .normal, showNewTask: $showNewTask, todoItems: $todoItems)
复制代码
```

恭喜你，我们就完成了`ContentView`首页视图和`NewToDoView`新建事项视图的全部交互逻辑！

## 未完待续

但还没有全部完成，我们只是完成了一个简单的`ToDo`待办事项的`App`，还没有实现`CoreData`数据持久化。

由于篇幅过长，`上篇`我们完成了`ContentView`首页视图的制作，`中篇`我们完成`NewToDoView`新建事项视图的制作，当然还有他们之间的`交互`。

`CoreData`数据持久化框架的使用将再分出`下篇`，我们看看如何使用`CoreData`数据持久化框架，真正实现一个可以`保存数据`的`App`。

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
    @State private var showNewTask = false
    @State private var offset: CGFloat = .zero    //使用.animation防止报错，iOS15的特性

    //去掉List背景颜色
    init() {
        UITableView.appearance().backgroundColor = .clear
        UITableViewCell.appearance().backgroundColor = .clear
    }

    var body: some View {

        ZStack {
        
            VStack {
                TopBarMenu(showNewTask: $showNewTask)
                ToDoListView(todoItems: $todoItems)
            }

            //判断事项数量为0时展示缺省图
            if todoItems.count == 0 {
                NoDataView()
            }

            //点击添加时打开弹窗
            if showNewTask {

                //蒙层
                MaskView(bgColor: .black)
                    .opacity(0.5)
                    .onTapGesture {
                        self.showNewTask = false
                    }

                NewToDoView(name: "", priority: .normal, showNewTask: $showNewTask, todoItems: $todoItems)
                    .transition(.move(edge: .bottom))
                    .animation(.interpolatingSpring(stiffness: 200.0, damping: 25.0, initialVelocity: 10.0),value: offset)
                }
        }
    }
}

//蒙层
struct MaskView : View {

    var bgColor: Color

    var body: some View {

        VStack {

            Spacer()

        }
        .frame(minWidth: 0, maxWidth: .infinity, minHeight: 0, maxHeight: .infinity)
        .background(bgColor)
        .edgesIgnoringSafeArea(.all)
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}

// 顶部导航栏
struct TopBarMenu: View {

    @Binding var showNewTask: Bool

    var body: some View {

        HStack {
            Text("待办事项")
                .font(.system(size: 40, weight: .black))

            Spacer()

            Button(action: {

                //打开弹窗
                self.showNewTask = true
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

```
//  NewToDoView.swift

import SwiftUI

struct NewToDoView: View {

    @State var name: String
    @State var isEditing = false
    @State var priority: Priority
    @Binding var showNewTask: Bool
    @Binding var todoItems: [ToDoItem]

    var body: some View {

        VStack {

            Spacer()

            VStack {
                TopNavBar(showNewTask: $showNewTask)
                InputNameView(name: $name, isEditing: $isEditing)
                PrioritySelectView(priority: $priority)
                SaveButton(name: $name, showNewTask: $showNewTask, todoItems: $todoItems, priority: $priority)
            }
            .padding()
            .background(Color.white)
            .cornerRadius(10, antialiased: true)
            .offset(y: isEditing ? -320 : 0)
        }.edgesIgnoringSafeArea(.bottom)
    }
}

struct NewToDoView_Previews: PreviewProvider {
    static var previews: some View {
        NewToDoView(name: "", priority: .normal, showNewTask: .constant(true), todoItems: .constant([]))
    }
}

// 顶部导航栏
struct TopNavBar: View {

    @Binding var showNewTask: Bool

    var body: some View {

        HStack {
            Text("新建事项")
                .font(.system(.title))
                .bold()

            Spacer()

            Button(action: {

                //关闭弹窗
                self.showNewTask = false

            }) {
                Image(systemName: "xmark.circle.fill")
                    .foregroundColor(.gray)
                    .font(.title)
            }
        }
    }
}

//输入框
struct InputNameView: View {

    @Binding var name: String
    @Binding var isEditing: Bool

    var body: some View {
    
        TextField("请输入", text: $name, onEditingChanged: { (editingChanged) in

            self.isEditing = editingChanged

        })
            .padding()
            .background(Color(.systemGray6))
            .cornerRadius(8)
            .padding(.bottom)
    }
}

// 选择优先级
struct PrioritySelectView: View {

    @Binding var priority: Priority

    var body: some View {

        HStack {
            PrioritySelectRow(name: "高", color: priority == .high ? Color.red : Color(.systemGray4))
                .onTapGesture { self.priority = .high }

            PrioritySelectRow(name: "中", color: priority == .normal ? Color.orange : Color(.systemGray4))
                .onTapGesture { self.priority = .normal }
                
            PrioritySelectRow(name: "低", color: priority == .low ? Color.green : Color(.systemGray4))
                .onTapGesture { self.priority = .low }
        }
    }
}

// 选择优先级
struct PrioritySelectRow: View {

    var name: String
    var color:Color

    var body: some View {

        Text(name)
            .frame(width: 80)
            .font(.system(.headline))
            .padding(10)
            .background(color)
            .foregroundColor(.white)
            .cornerRadius(8)
    }
}

// 保存按钮
struct SaveButton: View {

    @Binding var name:String
    @Binding var showNewTask: Bool
    @Binding var todoItems: [ToDoItem]
    @Binding var priority:Priority

    var body: some View {

        Button(action: {

            //判断输入框是否为空
            if self.name.trimmingCharacters(in: .whitespaces) == "" {
                return
            }

            //添加一条新数据
            self.addTask(name: self.name, priority: self.priority)

            //关闭弹窗
            self.showNewTask = false

        }) {

            Text("保存")
                .font(.system(.headline))
                .frame(minWidth: 0, maxWidth: .infinity)
                .padding()
                .foregroundColor(.white)
                .background(Color.blue)
                .cornerRadius(8)
        }
        .padding([.top,.bottom])
    }

    //添加新事项方法
    private func addTask(name: String, priority: Priority, isCompleted: Bool = false) {

        let task = ToDoItem(name: name, priority: priority, isCompleted: isCompleted)
        todoItems.append(task)
    }
}
复制代码
```

快来动手试试吧！

**如果本专栏对你有帮助，不妨点赞、评论、关注～**