
===============================================================================
1, FragmentScenario：Fragment 的测试框架；
   FragmentFactory：统一的 Fragment 实例化组件；
   FragmentContainerView：Fragment 专属视图容器；
   OnBackPressedDispatcher：在 Fragment 或其他组件中处理返回按钮事件。

2, 状态转移才是生命周期的本质（Activity 同理）


3，Context
Context是一个抽象类，具体的实现类有Application、Activity、Service与ContextImpl。为方便区分，通常也称
为ApplicationConext、ActivityContext与ServiceContext

Context 个数 = 2 x（Service 个数 + Activity 个数 + Application 个数） + 其他 ContextImpl 个数

   Activity

   Service

   BroadCastReceiver

   ContentProvider

   Application

4, Style  Theme

样式的本质是一组可复用的 View 属性集合，而主题是 一组可引用的命名资源集合。