



Dev notes



Encountered this:

> Could not readf rom remote repository. 

<img src="/Users/inside/Documents/castlewong/git_images/couldnot_read_from.png"  />

This error informs us we have an authentication issue.  

If we encounter an SSH authentication issue, our first port of call is to add your key to the SSH keychain:

```javascript
ssh-add ~/.ssh/id_rsa
```

This will add our id_rsa key to the keychain.

![](/Users/inside/Documents/castlewong/git_images/add_id_rsa.png)

Now, test the SSH connection:

1. 打开终端。

2. 输入以下内容：

   ```shell
   $ ssh -T git@github.com
   # Attempts to ssh to GitHub
   ```

   ![](/Users/inside/Documents/castlewong/git_images/identity_added.png)

   您可能会看到类似如下的警告：

   ```shell
   > The authenticity of host 'github.com (IP ADDRESS)' can't be established.
   > RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
   > Are you sure you want to continue connecting (yes/no)?
   ```

3. 验证所看到消息中的指纹是否与 [GitHub 的公钥指纹](https://docs.github.com/zh/github/authenticating-to-github/githubs-ssh-key-fingerprints)匹配。 如果是，则键入 `yes`：

   ```shell
   > Hi USERNAME! You've successfully authenticated, but GitHub does not
   > provide shell access.
   ```

   注意：远程命令应退出，并显示代码 1。

4. 验证生成的消息包含您的用户名。 如果收到“权限被拒绝”消息，请参阅“[错误：权限被拒绝（公钥）](https://docs.github.com/zh/articles/error-permission-denied-publickey)”。

Now, try again to clone proj. to local file folder:

![](/Users/inside/Documents/castlewong/git_images/clone_success.png)

