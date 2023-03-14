
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

Copy code

`emacs <filename>`

This will open the file in the emacs editor. The key bindings for editing in emacs can be quite different than in other editors, so consult a reference guide or tutorial for more information. When you're done editing, press "Ctrl + X, Ctrl + S" to save the changes and "Ctrl + X, Ctrl + C" to exit emacs.

Note that these are just a few examples of the text editors you can use in Bash, and there are many more options available.

[dd](https://github.com/castlewong/castlewong)