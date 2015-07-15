# Android 测试教程(7):测试 Content Provider

Content Provider 为不同的应用访问数据提供了统一的接口，本篇介绍 Android 测试包中用于测试 Content Provider 的相关知识。

Android 测试包中用于测试 Content Provider 的基本类为 ProviderTestCase2, 允许你在一个隔离环境下来测试 Content Provider。 并提供了一些 Mock 类如 IsolatedContext ,MockContentResover 来辅助测试。

和其它测试一样，对于 Content Provider 测试也是通过 InstrumentationTestRunner 来进行的。

编译测试代码的一般方法是通过派生 ProviderTestCase2 (为 AndroidTestCase  的子类），因此可以使用 JUnit 和 Android 平台相关的方法来测试 Content Provider。

可以参见后面的实例来了解如何测试 Content Provider。

Tags: [Android](http://www.imobilebbs.com/wordpress/archives/tag/android) [测试](http://www.imobilebbs.com/wordpress/archives/tag/%e6%b5%8b%e8%af%95)

 