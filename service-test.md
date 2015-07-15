# Android 测试教程(8):测试 Service

Android 测试框架也提供对 Service 测试的支持，基本类为 ServiceTestCase,因为 Service 类通常假定和它是和 Client 是分开使用的，因此你可以无需使用 Instrumentation 来测试 Service。

当你设计一个 Service 时，你应该考虑测试用例中如何检查 Service 的当前状态，比如你在 onCreate ,onStartCommand 中启动一个 Service，一般没有一个全局变量来表示 Service 是否成功，你可能需要自己定义一个全局变量用于测试用例中。

ServiceTestCase 中提供 getService() 可以取得当前被测试的 Service对象。

ServiceTestCase 为 AndroidTestCase 的子类，因此可以测试和 Permission 相关的功能，并提供 Mock 的Application 和 Context 对象为测试 Service提供了一个隔离的测试环境。

后面提供具体例子。

Tags: [Android](http://www.imobilebbs.com/wordpress/archives/tag/android) [测试](http://www.imobilebbs.com/wordpress/archives/tag/%e6%b5%8b%e8%af%95)