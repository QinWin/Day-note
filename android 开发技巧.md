#activity

1.用户可能没有任何应用处理您发送到 startActivity() 的隐式 Intent。或者，由于配置文件限制或管理员执行的
设置，可能无法访问应用。如果发生这样的情况，调用失败，应用也会崩溃。要验证 Activity 是否会接收 Intent，
请对 Intent 对象调用 resolveActivity()。如果结果为非空，则至少有一个应用能够处理该 Intent，并且可以安
全调用 startActivity()。如果结果为空，不要使用该 Intent。如有可能，您应停用发出该 Intent 的功能。

强制创建选择器 Intent.createChooser()

另外使用PackageManager  queryIntentActivities() 也可以达到相同的效果

2.parcelable(CREATOR) serializable(serialVersionUID) 
在发送您希望另一个应用接收的 Intent 时，请勿使用 Parcelable 或 Serializable 数据。如果某个应用尝试访问
 Bundle 对象中的数据，但没有对打包或序列化类的访问权限，则系统将提出一个 RuntimeException。
 
我们建议您使用 Bundle 类为 Intent 对象设置操作系统已知的基元。Bundle 类针对使用 parcel 进行编组和解组进行了高度优化。

3.如果您希望选择器对话框中的图标与 Activity 的默认图标不同，请在 <intent-filter> 元素中添加 android:icon。

4.Android 应用链接
深层链接是指将用户直接转到应用中的特定内容的网址。在 Android 中，您可以通过添加 intent 过滤器以及从传入
的 intent 提取数据来设置深层链接，以便将用户吸引到正确的 Activity。

5.keystore   $ keytool -list -v -keystore my-release-key.keystore

6.最近使用的应用屏幕 == 概览屏幕 == 近期任务列表

FLAG_ACTIVITY_NEW_DOCUMENT
使用 FLAG_ACTIVITY_NEW_DOCUMENT 标记启动的 Activity 必须在清单中设置 android:launchMode="standard" 属性值（默认值）。

如果您在创建新文档时设置了 FLAG_ACTIVITY_MULTIPLE_TASK 标记，则系统始终会以目标 Activity 为根来创建新任务。
此设置支持同一文档在多个任务中打开。