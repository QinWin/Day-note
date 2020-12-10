Android 学习
===========================================================

### 名词释义

限定符是资源目录名称中加入的短字符串，用于定义这些资源适用的设备配置。
屏幕尺寸（屏幕的物理尺寸）和屏幕密度（屏幕上像素的物理密度，称为 DPI）


### JetPack 认识

ConstraintLayout
库：androidx.constraintlayout:constraintlayout:2.0.0
酷炫实现：
https://github.com/android/views-widgets-samples/tree/master/ConstraintLayoutExamples

ViewModel
如果您希望在生成绑定类时忽略某个布局文件，请将 tools:viewBindingIgnore="true" 属性添加到相应布局文件的根视图中
Null 安全：由于视图绑定会创建对视图的直接引用，因此不存在因视图 ID 无效而引发 Null 指针异常的风险。
此外，如果视图仅出现在布局的某些配置中，则绑定类中包含其引用的字段会使用 @Nullable 标记。
类型安全：每个绑定类中的字段均具有与它们在 XML 文件中引用的视图相匹配的类型。这意味着不存在发生类转换异常的风险。

### 网络
官方示例：https://github.com/android/connectivity-samples/tree/master/NetworkConnect
Android 3.0（API 级别 11）及更高版本需要您在主界面线程以外的线程上执行网络操作，否则将抛出 NetworkOnMainThreadException。

### Android版本功能

从 Android 5.0（API 级别 21）开始，如果使用隐式 Intent 调用 bindService()，则系统会抛出异常。

### Kotlin

fun main() {
    println("Hello world!")
}

