
已损坏
废纸篓

打开终端执行以下命令：

xattr -cr /YOUR_PATH/NoFWL.app

同样的问题不要一直问，这个在 README.md 里已经写过了。请阅读一下好吗？



Xcode shortcuts for SwiftUI

option command [
move up

jump to definition-**ctrl command click**

//    MARK: option command ⬅️ 作为 fold 的快捷键也太方便了吧 好舒服 世界是由懒人推动的 

//    MARK:  可以在代码缩略图中看到 所以有用

折叠代码块：command+option+ → 或 ←  

command shift [ 移动到左边的tab

c o left curly brace

向上👆🏻移动当前行一行

opt command 0  toggle Inspector Bar on the right
command 0 **Hide navigator**

## 关于Xcode快捷键

Mac键盘图标与对应快捷按键

⌘——Command ()

⌃ ——Control

⌥——Option (alt)

⇧——Shift

⇪——Caps Lock

## 2.常见的快捷键组合

command + R——运行

command + B——编译

command + .——停止

command + 1~8——分别对应工程导航从左到右


fold code pack/折叠代码块：command+option+ → 或 ←

移动到左边的tab: command shift [

## 3.炫酷的快捷键组合

command + L——快速跳转到类的指定行

![](https://upload-images.jianshu.io/upload_images/4124076-77a26edd7edfb5ea.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

command + shift +0——查看Apple文档

![](https://upload-images.jianshu.io/upload_images/4124076-e96ae0919146e0e6.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

command + option + ← / command + option + →——收放方法体

![](https://upload-images.jianshu.io/upload_images/4124076-77ae18840333a246.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

整体位移代码

选中的代码 + command + \[ ——向左位移  

选中的代码 + command + \]—— 向右位移

选中的代码 + command + option + \[——向上位移

选中的代码 + command + option + \]——向下位移

command + K——清除控制台打印信息  



## storyboard 快捷键

com + option + =——更新选中View的frame

com + =——当前试图的frame 根据子视图更新size（如果有图片根据图片的原始大小）

按住option键+ 移动鼠标到View之间，会显示View之间的距离

在Xcode 6中有许多快捷键的设定可以使得你的编程工作更为高效，对于在代码文件中快速导航、定位Bug以及新增应用...

- [![](https://upload-images.jianshu.io/upload_images/766340-6d7ee846658322bc.png?imageMogr2/auto-orient/strip|imageView2/1/w/300/h/240/format/webp)](https://www.jianshu.com/p/6700d6056d1b)

- 参考:http://www.cnblogs.com/langtianya/p/3888157.html一、关于运行...

  [![](https://upload-images.jianshu.io/upload_images/1955259-c9b66d6ae53ea0ee.png?imageMogr2/auto-orient/strip|imageView2/1/w/300/h/240/format/webp)](https://www.jianshu.com/p/bc45d180bf83)

- 文章来源:一. 快捷键设置 MAC 中得特殊键 MAC 中得特殊符号 :-- Command () : ⌘ ;-...

  [![](https://upload-images.jianshu.io/upload_images/3084347-2031044a6de9a3c9?imageMogr2/auto-orient/strip|imageView2/1/w/300/h/240/format/webp)](https://www.jianshu.com/p/2f6248d5842c)

- 刚开始用Xcode是不是发现以前熟悉的开发环境的快捷键都不能用了？怎么快捷运行，停止，编辑等等、都不一样了。快速的...

  [![](https://upload-images.jianshu.io/upload_images/5828704-e87d105f3d44d06a.png?imageMogr2/auto-orient/strip|imageView2/1/w/300/h/240/format/webp)](https://www.jianshu.com/p/2bd9f1bc2990)

- 一、关于运行调试 1、运行，停止，都在工具栏的Product里。 Command + R 运行。 Command ...

  [![](https://upload-images.jianshu.io/upload_images/2461075-75d5fc0500f54328.png?imageMogr2/auto-orient/strip|imageView2/1/w/300/h/240/format/webp)](https://www.jianshu.com/p/9e5648ad20ec)

## xcode快捷键

1、一次性修改一个scope里的变量名：

点击该变量，出现下划虚线，然后command+control+E激活所有相同变量，然后进行修改。

2、删除一个词：option+delete

    删除一句话：command+delete

3、快捷搜索：

先点亮想要搜索的词，然后command+E将该次放入剪贴板，然后command+G来向下遍历该词，shift+command+G向上遍历。

4、新建tab：command+T

    tab间切换：command+shift+\[ 或 \]

    前后两行交换：command+option+\[ 或 \]

    不同窗口间切换：command+\`

5、快捷open：command+shift+O

然后option+shift+return切换出window布局选择界面

command+option+return：切换至双窗口

command+return：切换回单窗口

6、前进和后退：command+control+ → 或 ←

7、折叠代码块：command+option+ → 或 ←

8、debug：

下一行：F6

进入方法：F7

跳出方法：F8

全速执行：command+control+Y

clear debug console：command+K

9、查看帮助：

option+鼠标左键单击  或者

command+control+shift+/  （即command+control+?）


> **let** replacements = [
>
> ​    ("2", "2️⃣")
>
> ​    ("1", "1️⃣")
>
> ​    **for** (searchString, replacement) **in** replacements {
>
> ​      dateformatter.string(from: Date()) = dateformatter.string(from: Date()).replacingOccurrences(of: searchString, with: replacement)
>
> ​    }

Leaning tips and tricks about the tool will help you down the road. Today, I will show you 4 Xcode shortcuts that I find helpful when dealing with SwiftUI.

Leaning tips and tricks about the tool will help you down the road. Today, I will show you 4 Xcode shortcuts that I find helpful when dealing with SwiftUI.

-   [Refresh Canvas](https://sarunw.com/posts/xcode-shortcuts-for-swiftui/#refresh-canvas)
-   [Re-Indent](https://sarunw.com/posts/xcode-shortcuts-for-swiftui/#re-indent)
-   [Move line up / Move line down](https://sarunw.com/posts/xcode-shortcuts-for-swiftui/#move-line-up-%2F-move-line-down)
-   [Show/Hide SwiftUI Preview](https://sarunw.com/posts/xcode-shortcuts-for-swiftui/#show%2Fhide-swiftui-preview)

## [Refresh Canvas](https://sarunw.com/posts/xcode-shortcuts-for-swiftui/#refresh-canvas)

SwiftUI Preview is an excellent tool for creating and updating a view, but if you type code too fast, Xcode might stop updating the preview, and you will see the dialog to resume the live preview.

![Xcode can stop live updating, but you can resume by tap the resume button.](https://d33wubrfki0l68.cloudfront.net/417c4f592a0989638724f8ce803bfe589ededcef/d3151/images/swiftui-shortcut-updating-paused.png)

Xcode can stop live updating, but you can resume by tap the resume button.

Reach to that **Resume** button all day might be annoying. But there is a shortcut for that.

To resume automatic preview update, you use this shortcut.

**Command option p**

> ⌘ - command + ⌥ - option + p or  
> **Editor menu > Canvas > Refresh Canvas**

This will refresh your preview and start the automatic update again.

![Press command + option + p keys to trigger refresh canvas.](https://d33wubrfki0l68.cloudfront.net/56b9747367b5fc7d594e688fa29cafcafff46a34/9b6e1/images/swiftui-shortcut-update-preview.gif)

Press command + option + p keys to trigger refresh canvas.

## [Re-Indent](https://sarunw.com/posts/xcode-shortcuts-for-swiftui/#re-indent)

By nature, SwiftUI is likely to contain many indentations. Each view and each modifier mean another level of indentation. Writing a complex view might leave unaligned indents in your code. You can format that with the re-indent command.

To do that, you use the following shortcut.

> ⌃ – control + i or  
> **Editor menu > Structure > Re-Indent**

Re-indent only applies to the line your cursor is focusing, so you might need to select all the code (⌘ - command + a) before using re-indent command.

![control + i to re-indent your code.](https://d33wubrfki0l68.cloudfront.net/996bfaa0ada6c0e7dee3770c609543ff7cddb8e1/b2c2e/images/swiftui-shortcut-re-indent.gif)

control + i to re-indent your code.

## [Move line up / Move line down](https://sarunw.com/posts/xcode-shortcuts-for-swiftui/#move-line-up-%2F-move-line-down)

In UIKit, I rarely use this shortcut. But in SwiftUI, moving lines of code up and down can help you in two areas.

-   [Rearrange view modifiers](https://sarunw.com/posts/xcode-shortcuts-for-swiftui/#rearrange-view-modifiers).
-   [Rearrange views](https://sarunw.com/posts/xcode-shortcuts-for-swiftui/#rearrange-views).

### Rearrange view modifiers[](https://sarunw.com/posts/xcode-shortcuts-for-swiftui/#rearrange-view-modifiers)

The order of view modifier is very important in SwiftUI. Changing the order means changing in behaviors and appearance.

The following code will add a padding around the text view, then add background color to both the text view and padding.

```
Text("SwiftUI")    .padding()    .background(Color.yellow)
```

While the following will only add a background color to the text view.

```
Text("SwiftUI")    .background(Color.yellow)    .padding()
```

![Add padding before background color (Left) and add background color before a padding (Right).](https://d33wubrfki0l68.cloudfront.net/68893e401e75b777450dc0c7cfd31d72f50f91da/00ad4/images/swiftui-shortcut-modifier-order.png)

Add padding before background color (Left) and add background color before a padding (Right).

When working with SwiftUI, you will find yourself copying and pasting the view modifier around to get the result you want. Xcode has two commands to move code up and down, which might save you time copying and pasting if you use multiple modifiers.

To move line of code up:

> ⌘ - command + ⌥ - option + \[ or  
> **Editor menu > Structure > Move Line Up**

To move line of code down:

> ⌘ - command + ⌥ - option + \] or  
> **Editor menu > Structure > Move Line Down**

These commands will move a focusing line of code up and down.

command + option + \[ or \] to move a line of code up and down.

### Rearrange views[](https://sarunw.com/posts/xcode-shortcuts-for-swiftui/#rearrange-views)

View modifier is not the only thing we move. The view itself is another thing that we regularly move around when working in SwiftUI. It is very easy to compose views in SwiftUI. Most of the time, you will rearrange your view using VStack or HStack, and that's mean changing view position means moving your view's code up and down in a stack view.

We can also move a chunk of codes by **highlighting all the code** you want and then using the **Move line up / Move line down** command.

To move multiple lines of code up, you highlight the code and then use the following shortcut.

> ⌘ - command + ⌥ - option + \[ or  
> **Editor menu > Structure > Move Line Up**

To move multiple lines of code down:

> ⌘ - command + ⌥ - option + \] or  
> **Editor menu > Structure > Move Line Down**

Highlight the code and press command + option + \[ or \] to move multiple lines of code up and down.

 [![](https://d33wubrfki0l68.cloudfront.net/b1eee8a0d991d298e71cb3e0b9542ef89d355c18/eb3dc/images/sponsor/logobanner_360x240px-04.png)

CI/CD for iOS and macOS developers. Fast builds on M1 machines and predictable pricing. Automatic code signing and publishing with really good documentation.

Start building now](https://codemagic.io/ios-continuous-integration/?utm_source=sarun_website&utm_medium=sarun&utm_campaign=ios_sponsorship)

[Sponsor sarunw.com and reach thousands of iOS developers.](https://sarunw.com/sponsor)

## Show/Hide SwiftUI Preview[](https://sarunw.com/posts/xcode-shortcuts-for-swiftui/#show%2Fhide-swiftui-preview)

SwiftUI Preview is good, but it takes too much space. Apart from working with a view, you usually want it close.

To toggle SwiftUI Preview, you use this shortcut:

> ⌘ - command + ⌥ - option + ⏎ Return or  
> **Editor menu > Canvas**

Show/Hide SwiftUI Preview with command + option + return shortcut.

Feel free to follow me on [Twitter](https://twitter.com/sarunw) and ask your questions related to this post. Thanks for reading and see you next time.

If you enjoy my writing, please check out my Patreon [https://www.patreon.com/sarunw](https://www.patreon.com/sarunw) and become my supporter. Sharing the article is also greatly appreciated.