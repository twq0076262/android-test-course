# Android 测试教程(6):测试 Activity

Activity 的测试非常依赖于 Android 的 Instrumation 框架，和 Android 其他组件不同的是，Activity 具有复杂的生命周期回调函数(如 onCreate, onStart 等) ，通常情况下除通过 Instrumation 接口外不能直接调用这些回调函数。

- 测试 Activity 的基本测试类为 InstrumentationTestCase,它提供了 Instrumentation 接口给 TestCase 的子类。 为了支持 Activity 测试，InstrumentationTestCase 提供了下面功能：
- 生命周期控制： 使用 Instrumentation，你可以启动，暂停，中止被测试的 Activity。
- Dependency Injection : Instrumentation 允许创建一些 Mock 对象如 Context，Application 来帮助测试 Activity，从而帮助你控制测试环境并和实际的应用的其他部分隔离开来。你也可以定制一些 Intent 以启动 Activity。
- 用户界面交互： 你可以使用 Instrumentation 向 UI 发送按键和触摸事件。

下面几个为主要的用于测试 Activity 由 TestCase 派生而来的测试类：

- ActivityInstrumentationTestCase2  通常用于多个 Activity 的功能测试，它使用正常的系统框架来运行 Activity（使用应用程序本身），并使用正常系统 Context (非 Mock）来测试 Activity 的功能。 允许你创建一些 Mock Intent 用来测试 Activity 的响应。要注意的是，这种 TestCase 不允许使用 Mock 的 Context 和 Application 对象测试，也就是说你必须使用和应用程序实际运行的环境来测试。
- ActivityUnitTestCase 通常用来测试单独 Activity。在启动被测试的 Activity 之前，你可以 Inject 一个假的 Context 或是 Application ，使用这个 Mock 的 Context 中一个隔离环境中运行被测试的 Activity。通常用于 Activity 的单元测试，而不和 Anroid 系统进行交互。
- SingleLaunchActivityTestCase  用于测试单个 Activity，和 ActivityUnitTestCase 不同的是，它只运行 setUp 和 tearDown 一次，而不是在运行 testCase 中每个 Test Method 前后运行 setup 和 tearDown ，它可以保证运行多个测试之间 fixture 不会被重置，从而可以用来测试一些有关联的方法。

本篇和后面几篇介绍 Activity，Service，Content Provider 测试的基本概念和相关类，之后则结合 ApiDemo->Tests 为例具体介绍这些类的用法。

Tags: [Android](http://www.imobilebbs.com/wordpress/archives/tag/android) [测试](http://www.imobilebbs.com/wordpress/archives/tag/%e6%b5%8b%e8%af%95)