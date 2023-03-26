
> **is damaged and can’t be opened. you should move it to the trash**

sudo xattr -r -d com.apple.quarantine /Applications/Charles.app

> **If battery charging is paused or on hold on your Mac**

With macOS Big Sur or later, your Mac learns from your charging habits to improve the lifespan of your battery.

In macOS Big Sur or later, Optimized Battery Charging is designed to improve the lifespan of your battery and reduce the time your Mac spends fully charged. When the feature is enabled, your Mac will delay charging past 80% in certain situations. Your Mac learns your charging routine and aims to ensure that your Mac is fully charged when unplugged.

use offical website to download VS Code, the speed is so slow, find a way to workaround:
在 VS Code 官网下载 macOS 版 VS Code 好慢, 找到方法加速了:
更改国内镜像地址前缀：http://vscode.cdn.azure.cn
把下载地址stable 之前的替换成上述国内镜像, 即为：http://vscode.cdn.azure.cn/stable/622cb03f7e070a9670c94bae1a45d78d7181fbd4/VSCode-darwin.zip

command tab - switch apps used recently

`command 3` view as columns
`ctrl command 0` group by kind

#macOS-SC ⌃+⌘+0 use groups
#macOS-SC ![[group_by.png]]
#bash #macOS-SC 
cd - back to the previous dir
cd ~ home dir
cd .. back to the parent dir
⬆️ last order
hide or unhide a file in macOS
```bash
chflags nohidden/hidden foldername
```
#macOS-SC 
Now, I kinda get the beauty of purn-keyboard operation on macOS:

You can edit a text file in Bash using one of several command-line text editors, such as nano, vi, or emacs. Here are basic steps for each editor:

1.  nano:

Copy code

`nano <filename>`

This will open the file in the nano editor. You can make changes to the text file using the keyboard. When you're done editing, press "Ctrl + O" to save the changes and "Ctrl + X" to exit nano.

2.  vi:

Copy code

`vi <filename>`

This will open the file in the vi editor. 
Press `i` to enter insert mode, make your changes to the text file using the keyboard. 
When you're done editing, press **Esc** to exit insert mode. 
To save changes, type `:w` and hit enter. 
To exit vi, type `:q` and hit enter. 
Or just input `:wq` to save and exit.
If there are unsaved changes, you can type `:q!` and hit enter to exit without saving.
The bottom line shows status of the present, and you can input some command to operate the file you're editting.
This is the beauty of pure-keyboarding opreating, I want to learn master vim now.

3.  emacs:

`emacs <filename>`

This will open the file in the emacs editor. The key bindings for editing in emacs can be quite different than in other editors, so consult a reference guide or tutorial for more information. When you're done editing, press "Ctrl + X, Ctrl + S" to save the changes and "Ctrl + X, Ctrl + C" to exit emacs.

Note that these are just a few examples of the text editors you can use in Bash, and there are many more options available.

**Check md5 on macOS**
1. In Terminal, type
```bash
md5 <filename>
```
2. open the md5 file using textedit.app, compare the MD5 sum of the file with the one displayed in the terminal. 
3. If they are exactly the same, the file was downloaded successfully.