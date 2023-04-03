
Backlog means sth. should be done but haven't be done.

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

### Use alias in macOS Terminal

Step-by-step instructions for creating an alias in the macOS Terminal:

1. Open your terminal application: You can do this by clicking on the Terminal icon in your Applications folder, or by searching for "Terminal" in Spotlight (the magnifying glass icon in the top-right corner of your screen).

2. Open your shell configuration file: The shell configuration file is a text file that contains settings and customizations for your terminal session. In macOS, the default shell is usually Bash, so we'll use that as an example. To open your `~/.bash_profile` file in nano (a simple text editor), type the following command and press Enter:

   ```shell
   nano ~/.bash_profile
   ```

   If you don't have a `.bash_profile` file yet, nano will create one for you when you save.

3. Create the alias: In the nano editor, add a new line at the bottom of the file with the following format:

   ```shell
   alias [alias_name]="[command_or_path]"
   ```

   Replace `[alias_name]` with whatever name you want to use for your alias, and replace `[command_or_path]` with the command or path that you want to run when you type the alias. 

   For example, if you want to create an alias called "docs" that points to your Documents folder, you would type:

   ```shell
   alias docs="cd /Users/yourusername/Documents"
   ```

   Make sure to replace `yourusername` with your actual username.

4. Save and exit: Press `Ctrl+O` to save the file, then press `Ctrl+X` to exit nano.

5. Reload the shell configuration: To make the alias available in your current terminal session, you need to reload the shell configuration file. You can do this by typing the following command and pressing Enter:

   ```shell
   source ~/.bash_profile
   ```

That's it! You should now be able to use your new alias by typing `cd [alias_name]` in the terminal. For example, you can navigate to your Documents folder by typing `cd docs`.

## zsh: This is the way. 1

Share some efficient skills you can use with zsh in macOS:

1. **Tab completion**: Zsh has a powerful tab completion feature that can save you a lot of time. For example, if you type `cd /u/l/b` and press the `Tab` key, zsh will automatically complete the path to `/usr/local/bin`.

2. **Aliases**: You can create aliases for frequently used commands to save time. For example, you can create an alias for `ls -la` by adding the following line to your `~/.zshrc` file: `alias ll='ls -la'`. Then, you can simply type `ll` instead of `ls -la`.

3. **History search**: Zsh allows you to search your command history using the `Ctrl+R` shortcut. Simply press `Ctrl+R` and start typing a command you previously used. Zsh will search your history and display matching commands.

4. **Auto-suggestions**: Zsh can suggest commands based on your command history and current input. To enable this feature, add the following line to your `~/.zshrc` file: `plugins=(zsh-autosuggestions)`. Then, start a new terminal session and try typing a command. Zsh will suggest commands based on your history and current input.

5. **Custom prompts**: You can customize your zsh prompt to display useful information, such as the current directory, git branch, and more. To customize your prompt, add the following line to your `~/.zshrc` file: `PROMPT='%n@%m:%~$(git_prompt_info) %# '`. This will display your username, hostname, current directory, and git branch (if applicable) in your prompt.

