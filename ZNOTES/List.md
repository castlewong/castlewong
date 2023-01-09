
```
struct ContentView: View {
    var body: some View {

        // 简单的列表
        List {
            ForEach(1 ... 4, id: \.self) { index in
                Text("第 \(index)页")
            }
        }
    }
}

```

在使用ForEach遍历创建视图时，需要用id来标识内容，当里面的内容发现变化时，ForEach就可以自动更新UI。

简单来读一下代码内容：

我们传递给ForEach一个范围的值，用来循环遍历生成列表。

而它的id（标识符）被设置为值本身self，也就是前面设置的1、2、3、4。

然后用index参数存储循环的值。

我们在这里遍历了4次，每一次展示一个Text，Text里面的文字是“第”+{index}+“页”，index的参数值从1～4；

这样，我们就得到了一个列表。

当然，还有更简单的遍历方法。

```
struct ContentView: View {
    var body: some View {

        // 简单的列表
        List {
            ForEach(1 ... 4, id: \.self) {
                Text("第 \($0)页")
            }
        }
    }
}
```

在这里，我们省略索引参数index，而使用简化的$0，它引用闭包的第一个参数，直接将数据集合传递给List。

作者：文如秋雨  
链接：https://juejin.cn/post/7085515068586065950  
来源：稀土掘金  
