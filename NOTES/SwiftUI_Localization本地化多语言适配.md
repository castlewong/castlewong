
zhonguncle的博客-CSDN博客_swiftui 多语言

事先说明一下，开发环境使用的是英文（en），所以开发的语言是英语（后面会提到哦）。**如果不是从头添加本地化文件，而是添加，请看最后列出的的问题和解决方案。**

**如图所示是我们需要本地化的内容。就是这个文本`test`。**  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210601095459945.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzOTE5NDUw,size_16,color_FFFFFF,t_70)

**第一步，在Info里添加上简体中文（zh-Hans）和日语（ja）。其实这个步骤可以省略，直接下一个步骤开始也可以，第三步的之后会自动添加的。**。这样告诉[Xcode](https://so.csdn.net/so/search?q=Xcode&spm=1001.2101.3001.7020)我们支持哪些语言。日语在这里是为了展示多种语言场景，毕竟有时候我们不止需要翻译一种语言。  
![添加的步骤](https://img-blog.csdnimg.cn/20210601094854205.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzOTE5NDUw,size_16,color_FFFFFF,t_70)

![添加之后的样子](https://img-blog.csdnimg.cn/20210601094927494.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzOTE5NDUw,size_16,color_FFFFFF,t_70)

**第二步，新建三个Group/文件夹，`en.lproj`、`zh-Hans.lproj`和`ja.lproj`表示简体中文、英语和日语本地化文件夹。** 这里需要添加“开发语言（Development Language）”——英语，不然界面上会一直显示时间顺序上最早建立的本地化文件里的文本，不会显示英语本身。  
![新建组](https://img-blog.csdnimg.cn/2021060110030259.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzOTE5NDUw,size_16,color_FFFFFF,t_70)  
![例如这样的简体中文本地化文件组](https://img-blog.csdnimg.cn/20210601100311711.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzOTE5NDUw,size_16,color_FFFFFF,t_70)  
![新建结束应该的样子](https://img-blog.csdnimg.cn/20210601100424252.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzOTE5NDUw,size_16,color_FFFFFF,t_70)

**第三步，在三个Group下面都新建一个名为`Localizable.strings`的字符串文件**。右击->“New File…”或者command键+N键新建就可以啦。  
![新建选择这个哦](https://img-blog.csdnimg.cn/20210601100554230.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzOTE5NDUw,size_16,color_FFFFFF,t_70)  
![新建完的样子](https://img-blog.csdnimg.cn/20210601100752777.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzOTE5NDUw,size_16,color_FFFFFF,t_70)  
**第四步，在每个文件里输入以下内容（注意最后有个分号）：**

```
//英文的字符串本地化文件里输入
"test" = "test";
```

```
//简体中文的字符串本地化文件里输入
"test" = "测试";
```

```
//日文的字符串本地化文件里输入
"test" = "テスト";
```

**接下来回到最开始的界面，来看看我们的工作结果。把预览的代码改成如下样式：**

```
struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
            .environment(\.locale, .init(identifier: "en"))
    }
}
```

**这里的`"en"`就表示当前使用的系统语言。将其改成`"zh-Hans"`来看看吧**：

![代码和预览的样子](https://img-blog.csdnimg.cn/20210601101544851.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzOTE5NDUw,size_16,color_FFFFFF,t_70)

成功啦，改成`"ja"`再看看：  
![日文本地化显示](https://img-blog.csdnimg.cn/2021060110164922.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzOTE5NDUw,size_16,color_FFFFFF,t_70)  
日文也没问题。

这里有一个问题需要注意，如果按照这个步骤来，比如说想**添加一个新的**本地化文件，发现按照这个步骤来第一步就不行，添加的时候就卡住了。这时候只要直接从第二步开始就好了。。。









