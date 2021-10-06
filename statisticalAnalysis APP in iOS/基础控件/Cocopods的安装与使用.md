# Cocopods的安装与使用

## Cocopods介绍

CocoaPods是管理iOS项目所依赖的第三方开源库的工具，其项目源码在Github上管理。若项目开发不使用Cocopods，我们引入第三方开源库要做的步骤可能有：

- 把开源库的源代码复制到项目中
- 添加一些依赖框架和动态库(可能还需要引入其他的第三方开源库)
- 设置-ObjC，-fno，-objc，-arc 等参数
- 管理他们的更新

CocoaPods 是管理第三方插件的合集，其出现帮助节省了配置和更新第三方开源库的时间。 CocoaPods 将所有依赖的库都放在一个名为 Pods 的项目下，然后让主项目依赖 Pods 项目。然后， 我们编码工作都从主项目转移到 Pods 项目。Pods 项目最终会编译为一个 libPod-项目名.a 静态库， 主项目依赖于这个静态库。对于资源文件，CocoaPods 提供了一个名为 Pods-resources.sh 的 bash 脚本，该脚本在每次项目编译的时候都会执行，将第三方库的各种资源文件复制到目标目录中。

CocoaPods 通过一个名为 Pods.xcconfig 的文件来在编译时设置所有的依赖和参数。

CocoaPods 是用 Ruby 写的，并由若干个 Ruby 包 (gems) 构成的。在解析整合过程中，最重 要的几个 gems 分别是:CocoaPods/CocoaPods, CocoaPods/Core, 和 CocoaPods/Xcodeproj。



## Cocopods安装

在使用 Cocopods 之前，我们需要在`Terminal`进行安装：

1. 安装需要用到 Ruby，虽然 Mac 自带了 Ruby，但版本需要更新：

   ```bash
   sudo gem update −−system
   ```

2. 输入密码后安装 Cocopods：

   ```bash
   sudo gem install cocoapods
   ```

3. 如果安装过程过慢导致失败，可以更换国内下载源，安装完成后，在 `Terminal` 中：

   - cd 到目标工程文件路径下
   - pod init 会看到 Podfile 文件
   - vim Podfile 即可向其中插入想引用的第三方库