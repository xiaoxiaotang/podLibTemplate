pod-template
============

## important notice 重要提示
It's based on official template https://github.com/CocoaPods/pod-template.git however, delete the choice for macOS,swift, test framework options, just keep the custom class prefix function, it will only ask you which prefix you want to use, and will create an iOS pod lib project with demo, no test frameworks.

基于官方模板https://github.com/CocoaPods/pod-template.git 改造，删除了选择mac os平台和Swift的选项，以及测试框架的选项，只保留了自定义类前缀的功能，会默认创建一个OC语言的iOS的pod库，带demo工程，无测试框架。

## usage 使用方法

制作私有pod库的过程总结

在此次podspec制作过程中，遇到了一些问题，现总结一下，以备下次查看：

1）运行 pod lib create LDLAAccount --template-url=https://github.com/xiaoxiaotang/podLibTemplate.git （官方用法/official usage） 可以快速创建一个包含Example工程的项目，其中自动生成了Podfile文件

以及LDLAAccount.podspec、ReadMe.md、License文件

2）将需要制作成pod的项目文件放入到Pod/Classes下，资源文件放到Pod/Asserts下

3）修改podspec文件中的 s.sourcefiles和bundle等相关，以及添加其依赖库

4）进入Example项目根目录下，pod install/update，运行Example工程，建立一个pod使用测试

5）Example运行没有错误后，再远程Gitlab建立一个LDLAAccount仓库，cd 到Example的上级目录（及podspec文件所在目录）

在命令行执行：git add .   

git commit -m “”

git remote add origin 远程仓库地址

git push origin master 

6) 由于podspec文件中获取Git版本控制的项目还需要tag号，所以需要给远程仓库打上一个tag，

执行命令：git tag -m “commit msg” “0.1.0”

git push —tags

7) 编辑podspec文件

修改podspec中的homepage 和 sources 和 版本号，summary 和 description

8）回到Example目录下，pod update ，运行项目，没有问题执行下一步

9）cd 到podspec所在目录，执行 pod spec lint LDLAAccount.podspec  --allow-warnings  --sources=远程仓库podspec git地址.git,https://github.com/CocoaPods/Specs.git  --verbose  --use-libraries

如果提示pass validate ，进行下一步

10）pod repo list 查看本地的Spec repo文件

11）pod repo push saict-scprivatepodspec LDLAAccount.podspec --allow-warnings  --sources=远程仓库podspec git地址.git,https://github.com/CocoaPods/Specs.git  --verbose  --use-libraries

pod repo push 230-privatepodspecs HttpRequestLibs.podspec --allow-warnings --sources=git@134.175.230.26:iOS_Compoent/PrivatePodSpecs.git,https://github.com/CocoaPods/Specs.git  --verbose  --use-libraries

将自定义的podspec加入到SepcRepo下，并push到远端

12）cd 到Example所在目录，修改.gitignore文件，加入Pods/，用以忽略依赖的第三方库文件

13）完善ReadMe.md，添加相应说明，再将工程重新push到远程仓库即可





Pod库的更新维护：

1）在Pod/Classes中加入所要加的文件

2）修改podspec文件，包括新的版本号

3）在Example的工程目录下，pod update，执行项目，成功后执行下一步

4）完善ReadMe文件，将整个文件push到远程仓库，并打上一个新的tag值

5）cd 到 podspec所在路径，如上执行pod spec lint LDLAAccount.podspec  --allow-warnings  --sources=远程仓库podspec git地址.git,https://github.com/CocoaPods/Specs.git  --verbose  --use-libraries 进行验证

6）添加这个新的podspec文件，执行命令：
pod repo push saict-scprivatepodspec LDLAAccount.podspec --allow-warnings  --sources=远程仓库podspec git地址.git,https://github.com/CocoaPods/Specs.git  --verbose  --use-libraries

pod repo push 230-privatepodspecs HttpRequestLibs.podspec --allow-warnings --sources=git@134.175.230.26:iOS_Compoent/PrivatePodSpecs.git,https://github.com/CocoaPods/Specs.git  --verbose  --use-libraries



到此，完成了pod的更新工作
