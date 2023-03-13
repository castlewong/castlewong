[Link](https://juejin.cn/post/7089246277442994207)

承接上一章的内容，我们继续完成使用`CoreData`框架搭建一个简单的`ToDo`待办事项`App`。

这一章节，我们正式进入使用`CoreData`框架实现`数据持久化`。

![1.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7b3ca5c3959244d49659a002701b9484~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

之前我们是通过创建项目的时候勾选使用`CoreData`框架，系统给我们创建了需要的`文件`和`模型`。那么这一章节，我们尝试使用`CoreData`框架达到`数据持久化`的目的。

## Persistence.swift文件

`Persistence.swift`文件是数据`保存`到持久存储区的文件，通过将管理对象上下文`注入`到环境中，来实现在任何视图都可以`检索`上下文，并且能够`管理数据`。

我们`删除`多余的示例数据代码。

```
import Foundation

import CoreData

struct PersistenceController {    

    static let shared = PersistenceController()

    let container: NSPersistentContainer

    init(inMemory: Bool = false) {

        container = NSPersistentContainer(name: "SwiftUICoreData")

        if inMemory { container.persistentStoreDescriptions.first!.url = URL(fileURLWithPath: "/dev/null")
        }

        container.loadPersistentStores(completionHandler: { storeDescription, error in
            if let error = error as NSError? {
                fatalError("Unresolved error \(error), \(error.userInfo)")
            }
        })
    }
}
复制代码
```

![2.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9142516b3c6c48f79fc90a57555dc2ed~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

## SwiftUICoreDataApp.swift文件

我们回到`SwiftUICoreDataApp.swift`文件，我们需要将托管对象上下文注入到环境中，这样我们就能够方便地在内容视图中访问上下文，并且管理数据库中的数据。

```
import SwiftUI

@main
struct SwiftUICoreDataApp: App {

    let persistenceController = PersistenceController.shared

    var body: some Scene {

        WindowGroup {

            ContentView()
                .environment(\.managedObjectContext, persistenceController.container.viewContext)
        }
    }
}
复制代码
```

![3.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d57bf3aabf3741e6be9219ebb56b2010~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

## SwiftUICoreData.xcdatamodeld模型

模型创建完成后，我们需要创建一个新的实体`ToDoItem`来存储我们需要用到的`参数`，我们将原来的实体`Item`重新命名为`ToDoItem`。

在`ToDoItem`实体中，我们需要定义好项目需要的`属性`。

```
id:UUID
name:String
priorityNum:Integer32
isCompleted:Boolean
复制代码
```

由于`priority`优先级属性是一个`Enum`枚举类型，为了将`Enum`枚举类型`保存`到数据库中，我们必须存储它的`原始值`，即`Int`整数，因此需要使用`Integer 32`类型，而且为了避免`命名冲突`，我们将属性命名为`priorityNum`。

这里再科普一个知识点。

由于`ToDoItem`实体我们重新定义了，那么要保证`Module`模块要选择`CurrrentProductModule`当前产品的模型，`Codegen`代码基因要选择`Manual/None`，不然我们在项目中引用模型的时候可能会`找不到`我们定义的`ToDoItem`实体，这非常重要！非常重要！非常重要！重要的事情说三遍。

![10.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/be82347338c64f17a8d68494def5ad2c~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

## CoreData模型类

在`CoreData`框架中，每个实体都与一个模型类`配对`，我们需要在`ToDoItem.swift`文件定义模型类。

这里`CoreData`的模型类继承自`NSManagedObject`协议，每个属性都使用`@NSManaged`进行注释，并且对应我们`ToDoItem`创建的属性`id、name、priorityNum、isCompleted`。

```
import Foundation

import CoreData

enum Priority: Int {
    case low = 0
    case normal = 1
    case high = 2
}

public class ToDoItem: NSManagedObject {
    @NSManaged public var id: UUID
    @NSManaged public var name: String
    @NSManaged public var priorityNum: Int32
    @NSManaged public var isCompleted: Bool
}

extension ToDoItem: Identifiable {

    var priority: Priority {

        get {
            return Priority(rawValue: Int(priorityNum)) ?? .normal
        }

        set {
            self.priorityNum = Int32(newValue.rawValue)
        }
    }
}
复制代码
```

![5.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fb820b2a49c0427b80a52839e7a275d7~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

## ContentView.swift文件

定义好`CoreData`模型类后，我们需要在`ContentView`主视图中使用它，我们使用`@FetchRequest`属性包装器从数据库`加载数据`，我们替换之前使用`@State`标记的`ToDoItem`数组数据来源。

```
@FetchRequest( entity: ToDoItem.entity(),
    sortDescriptors: [ NSSortDescriptor(keyPath: \ToDoItem.priorityNum, ascending: false) ])

var todoItems: FetchedResults<ToDoItem>
复制代码
```

我们在环境中注入了托管对象上下文，获取所需的数据。

由于我们的`List`列表数据来源于新定义的`todoItems`，我们把整个`ToDoListView`的`body`内容拆回到`ContentView`主视图，这样我们就可以`直接`遍历循环`todoItems`的内容。

```
List {
    ForEach(todoItems) { todoItem in
        ToDoListRow(todoItem: todoItem)
}
复制代码
```

![11.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/60aeca7f149140e9afdf7de66685a2b0~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

## NewToDoView.swift文件

紧接着，我们需要同步更新`NewToDoView.swift`的代码。要将一个新任务保存到数据库中，首先需要从环境中获取管理对象上下文。

```
@Environment(\.managedObjectContext) var context
复制代码
```

然后，我们在`NewToDoView`视图和`saveButton`保存按钮视图就不需要再`@Binding`绑定`ToDoItem`数组了。

```
@Binding var todoItems: [ToDoItem]
复制代码
```

然后，我们再更新下`addTask`添加新事项的方法。

```
//添加新事项方法
private func addTask(name: String, priority: Priority, isCompleted: Bool = false) {

    let task = ToDoItem(context: context)
    task.id = UUID()
    task.name = name
    task.priority = priority
    task.isCompleted = isCompleted

    do {
        try context.save()
    } catch {
        print(error)
    }
}
复制代码
```

![12.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/82223e19b87a4e81b9299c5491e3b6dc~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

我们要将`新事项`插入数据库中，需要使用托管上下文创建`ToDoItem`，然后调用上下文的`save`函数来提交更改。

因为我们删除了`todoItems`绑定，所以还需要调整`NewToDoView_Previews`预览视图。

```
NewToDoView(name: "", priority: .normal, showNewTask: .constant(true))
复制代码
```

由于我们`NewToDoView`新建事项视图`发现变化`，我们回到`ContentView`首页视图，重新修改下`绑定`关系。

```
NewToDoView(name: "", priority: .normal, showNewTask: $showNewTask)
复制代码
```

同样，我们在`ContentView`首页视图也需要从环境中获取管理对象上下文。

```
@Environment(\.managedObjectContext) var context
复制代码
```

## ToDoListRow视图

与添加新事项类似，我们需要获取用于记录更新的托管对象上下文。对于`Toggle`优先级选择视图，每当切换发生更改时，`todoItem`的`isCompleted`属性将被更新。我们可以附加`onReceive`修饰符，`onReceive`修饰符可以监听`isCompleted`属性和其他我们定义好的属性的更改，并通过调用上下文的`save`函数将它们保存到持久存储区。

```
//监听todoItem数组参数变化并保存
.onReceive(todoItem.objectWillChange, perform: { _ in
    if self.context.hasChanges {
        try? self.context.save()
    }
})
复制代码
```

![6.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0c8d5e54b9d144ba881132fbb54c128b~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

## deleteTask删除事项方法

上面我们既然完成了`addTask`新增事项方法，那么顺便完成`deleteTask`删除事项的交互。

```
//删除事项方法
private func deleteTask(indexSet: IndexSet) {
    for index in indexSet {

        let itemToDelete = todoItems[index]

        context.delete(itemToDelete)
    }
    
    DispatchQueue.main.async {
        do {
            try context.save()

        } catch {
            print(error)
        }
    }
}
复制代码
```

`deleteTask`删除事项方法接收一个存储要`删除的项`的索引集，我们只需要调用上下文的`delete`函数，并指定要删除的项，然后调用`save`函数来提交更新。

我们把这个方法加到`List`里，就可以实现`滑动删除`的操作。

```
List {
    ForEach(todoItems) { todoItem in
        ToDoListRow(todoItem: todoItem)
    }.onDelete(perform: deleteTask)
}
复制代码
```

![9.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/81b78ce1a6da49888606e158be5f3795~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

## preview预览效果

我们运行模拟器的时候发现报错了，这是因为我们没有在`contentview_preview`结构体中注入托管对象上下文。我们需要创建一个内存中的数据存储，并准备一些测试数据。

我们在`Persistence.swift`文件创建了一个`PersistenceController`实例，并将`inMemory`参数设置为`true`，然后我们添加`10`个示例待办事项，并将它们`保存`到数据存储中。

```
import CoreData

struct PersistenceController {

    static let shared = PersistenceController()

    let container: NSPersistentContainer

    static var preview: PersistenceController = {

        let result = PersistenceController(inMemory: true)
        let viewContext = result.container.viewContext

        for index in 0..<10 {
            let newItem = ToDoItem(context: viewContext)
            newItem.id = UUID()
            newItem.name = "待办事项\(index)"
            newItem.priority = .normal
            newItem.isCompleted = false

        }
        do {
            try viewContext.save()
        } catch {
            let nsError = error as NSError
            fatalError("Unresolved error \(nsError), \(nsError.userInfo)")
        }
        return result
    }()

    init(inMemory: Bool = false) {

        container = NSPersistentContainer(name: "SwiftUICoreData")

        if inMemory {
        
            container.persistentStoreDescriptions.first!.url = URL(fileURLWithPath: "/dev/null")
        }

        container.loadPersistentStores(completionHandler: { (storeDescription, error) in
            if let error = error as NSError? {
                fatalError("Unresolved error \(error), \(error.userInfo)")
            }
        })
    }
}
复制代码
```

之后我们如果只需要在`ContentView_Previews`预览视图的上下文注入到内容视图的环境中，就可以看到`示例`的数据啦～

```
struct ContentView_Previews: PreviewProvider {

    static var previews: some View { 
    
        ContentView().environment(\.managedObjectContext, PersistenceController.preview.container.viewContext)
    }
}
复制代码
```

![8.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/58b7938304a842098be2eb7d45c0af02~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image?)

快来动手试试吧！

**如果本专栏对你有帮助，不妨点赞、评论、关注～**