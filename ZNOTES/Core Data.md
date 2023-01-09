Core Date is not a database
It's just a framework for devs to manage and interact with data on a persistent store

> ~.xcdatamodeld

the managed object model is defined in a file with the extension
this is the managed object model generated for your project and 
this is where you define the entities for interacting with the persistent store

> Persistence.swift

this file contains the code for loading the managed object model and 
saving the data to the persistent store

一个是`SwiftUICoreData.xcdatamodeld`文件，它是管理整个项目生成的对象模型的，是定义`实体与持久存储交互`的文件。

另一个是`Persistence.swift`文件，它是`数据保存到 persistent store 持久存储区`的文件。

To save and manage data on the local database
1. create an entity in the managed object odel(i.e. .xcdatamodeld)
2. define a managed object, which inherits from NSManagedObject, to associate with the entity
3. In the views that need to save and updata the data, get the managed object context from the enviromnment using @Enviroment like this👇🏻 : create the managed object and use the save method of the context to add the object to the database.
```
@Environment(\.managedObjectContext) var context
```
4. For data retrieval, Apple introduced a property wrapper called @FetchRequest for you to fetch data from the persistent store.
to save enum into the db we have to store its raw value which is an integer
in Core Data every entity should be paired with a model class

perform fetch update insert delete

[[CoreData数据持久化框架的使用1]]
[[CoreData数据持久化框架的使用2]]
[[CoreData数据持久化框架的使用3]]
[[CoreData in Multiplatform App  Apple Developer Forums]]
