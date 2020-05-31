# CompareVersionDiff
导出每个手机版本的里面apk、property、xml配置，然后对比2个不同的版本之间的差异，来确认是否有非预期的修改被带入

背景：
手机项目开发进入后期，相关的修改及对应的测试重点是针对修改点，在多个团队共性开发的情况下，每个模块的修改点ReleaseNote不一定都能准确提供，都过对比apk/property/xml，可以过滤一些非预期的修改

> 说明：此方法能拦截一部分比较明显的问题，缩小差异范围，为评估版本的修改影响和测试策略的制定提供帮助

### 使用说明
配置要求：
- 电脑上配置adb、java

执行[start_getdiff.bat](https://github.com/chadmXiang/CompareVersionDiff/tree/master/tool/start_getdiff.bat "With a Title"). 

### 实现说明
通过adb shell命令来获取并解析生成excel表格，然后对比excel表格差异
```
adb shell dumpsys package
adb shell getprop
adb shell settings list system
adb shell settings list global
adb shell settings list secure
```
#### 1.apk差异
一般情况下，apk有修改就是更新迭代版本号，通过这个来确认是否有改动；另外如果和上一个版本有apk增加或减少的，就需要重点确认，是否符合预期

#### 2.property差异
一般增加某个特性会用一个property开关来控制，通过对比这个来确认是否有新增加

#### 3.xml差异
通过对比system/global/secure里面的配置差异，来确认修改点

