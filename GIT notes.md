
[toc]


## Basic git

Change the current command line chat to another directory, use 3 commands:

- pwd
- ls
- cd

pwd means **print working directory**, it shows the abouslute directory of current file path.

ls means list **directory contents**, it lists all content of current file path.

cd stands for **change directory**, use it to jump to any file path you assign, if not, it would bring you to the home folder, the **~** do the same.

|           COMMAND           |                           FUNCTION                           |
| :-------------------------: | :----------------------------------------------------------: |
|            cd ..            |                         Upper lever                          |
|            cd -             |                  Back to last path of file                   |
|       rm [file name]        |                         Delete file                          |
|       cat [file name]       |                          Check file                          |
|            mkdiv            |                    Create new file folder                    |
| git add [file1] [file2] ... | Add changes of choosed file(s) in the working directory to the staging area |
|       git checkout .        |            Discharge changes in working directory            |
|       git log --stat        |        Show git history, and files that been changed         |
|        `git status`         |         check the current status of this repository          |

git branch (branchname)

git checkout (branchname)

> Relative links and image paths in README files

You can define relative links and image paths in your rendered files to help readers navigate to other files in your repository.

A relative link is a link that is relative to the current file. For example, if you have a README file in root of your repository, and you have another file in _docs/CONTRIBUTING.md_, the relative link to _CONTRIBUTING.md_ in your README might look like this:

```
[Contribution guidelines for this project](docs/CONTRIBUTING.md)
```

GitHub will automatically transform your relative link or image path based on whatever branch you're currently on, so that the link or path always works. The path of the link will be relative to the current file. Links starting with `/` will be relative to the repository root. You can use all relative link operands, such as `./` and `../`.

Relative links are easier for users who clone your repository. Absolute links may not work in clones of your repository - we recommend using relative links to refer to other files within your repository.


Use `git log -1` to view the last commit.

how to amend the time of commit:

```git
git commit --amend --date="YYYY-MM-DD HH:MM:SS"
```

> Commit assign details

git commit --date="Jan 26 14:19:54 2023 +0800" -am "SSH details."


## You can't merge with local modifications. 

Git protects you from losing potentially important changes.

You have three options:

- Commit the change using
  
    ```git
    git commit -m "My message"
    ```
    
- Stash it.
  
    Stashing acts as a stack, where you can push changes, and you pop them in reverse order.
    
    To stash, type
    
    ```git
    git stash
    ```
    
    Do the merge, and then pull the stash:
    
    ```git
    git stash pop
    ```
    
-   Discard the local changes
    
    using `git reset --hard`  
    or `git checkout -t -f remote/branch`
    
    Or: Discard local changes for a specific file
    
    using `git checkout filename`


## To ignore certain files in Git,

you can create a file called `.gitignore` in the root directory of your Git repository and list the files or patterns that you want Git to ignore.

If you want to ignore a file that is already checked in, you must untrack the file before you add a rule to ignore it. From your terminal, untrack the file.

```shell
$ git rm --cached FILENAME
```

Here's how you can create a `.gitignore` file and add files or patterns to ignore using the terminal in macOS:

1. Open Terminal on your macOS machine.
2. Navigate to the root directory of your Git repository by using the `cd` command. For example, if your Git repository is located at `/Users/YourUserName/Documents/MyProject`, you can navigate to it by running the following command:

```shell
bashCopy code
cd /Users/YourUserName/Documents/MyProject
```

1. Create a new file called `.gitignore` by running the following command:

```bash
touch .gitignore
```

1. Open the `.gitignore` file in your text editor of choice. For example, you can open it in the nano text editor by running the following command:

```bash
nano .gitignore
```

1. Add the names of the files or patterns that you want to ignore to the `.gitignore` file, each on a separate line. For example, to ignore a file called `secret.txt` and all `.log` files, you can add the following lines to the `.gitignore` file:

```
secret.txt
*.log
```

1. Save the changes to the `.gitignore` file and exit the text editor.
2. Add the `.gitignore` file to your Git repository by running the following command:

```
git add .gitignore
```

1. Commit the changes to your Git repository by running the following command:

```
sqlCopy code
git commit -m "Add .gitignore file"
```

Git will now ignore the files or patterns that you listed in the `.gitignore` file.



## Generate SSH key

1. Check if ssh folder has been generated

   ls -al ~/.ssh 

2. If not

   git config –global user.name ‘xxxxx’ 
   git config –global user.email ‘xxx@xx.xxx’

3. Generate key

   ssh-keygen -t rsa -C ‘email’

4. Return



## Could not read from remote repository. 

Encountered this:

> Could not read from remote repository. 

![[couldnot_read_from.png]]
This error informs us we have an authentication issue on SSH.

SSH stands for 

> Secure Shell Protocol.

```bash
ssh-keygen -t ed25519 -C "youremail@some.com"
```

this command generate private key and public key in your pc
then use code below to copy your public key
```bash
pbcopy < ~/.ssh/id_ed25519.pub
```
Go to GitHub-setting-SSH
Add new Key
> If we encounter an SSH authentication issue, our first port of call is to add your key to the SSH keychain:

```javascript
ssh-add ~/.ssh/id_rsa
```

This will add our id_rsa key to the keychain.

![[add_id_rsa.png]]
Now, test the SSH connection:

1. 打开终端。

2. 输入以下内容：

   ```shell
   $ ssh -T git@github.com
   # Attempts to ssh to GitHub
   ```

   您可能会看到类似如下的警告：
```shell
The authenticity of host 'github.com (IP ADDRESS)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)?
```

验证所看到消息中的指纹是否与 [GitHub 的公钥指纹](https://docs.github.com/zh/github/authenticating-to-github/githubs-ssh-key-fingerprints)匹配。 如果是，则键入 `yes`：

   > Hi USERNAME! You've successfully authenticated, but GitHub does not
   > provide shell access.
   
   注意：远程命令应退出，并显示代码 1。

4. 验证生成的消息包含您的用户名。 如果收到“权限被拒绝”消息，请参阅“[错误：权限被拒绝（公钥）](https://docs.github.com/zh/articles/error-permission-denied-publickey)”。

Now, try again to clone proj. to local file folder:

