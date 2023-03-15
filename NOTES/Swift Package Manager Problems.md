
Set proxy for using SPM in China 国内使用 SPM
Xcode使用的是自带的git，设置全局或控制台的代理都无法使`SPM`走代理模式
使用Proxifier来设置代理规则，让 Xcode fetch 的时候走代理：
Use Proxifier to get things right:
1. add new proxy Proxies-add-IP 和 端口Port，使用 Clash 的话是 127.0.0.1:7890， SOCK5，注意最后一步save 时，千万不能选 default！
2. add new rules Rules-Application 处填写`"Xcode.app"; "Xcode"; com.apple.dt.Xcode; com.apple.dt.Xcode.sourcecontrol.Git` 注意每个分号后面有空格
3. action 处选择刚刚加的 IP 和 port
4. All set，现在 xcode 里 add packages 选择 GitHub 来源，resolve 和fetch就不会那么卡了，这个问题之前烦死我了。
Reference:
https://www.bolee.fun/xcode-spm-with-proxy.html
https://juejin.cn/post/6975355916531023880

### [Add a package dependency](https://developer.apple.com/documentation/xcode/adding-package-dependencies-to-your-app#Add-a-package-dependency)

To add a package dependency to your Xcode project, select File > Swift Packages > Add Package Dependency and enter its repository URL. You can also navigate to your target’s General pane, and in the “Frameworks, Libraries, and Embedded Content” section, click the + button, select Add Other, and choose Add Package Dependency.