# Android 测试教程(4):测试相关 API

Android 的测试框架相关的 API 主要定义在三个包中：

- android.test  用于编写 Android 测试用例
- android.test.mock  定义了方便测试用的测试“桩”类
- android.test.suitebuilder  运行测试用例的 Test Runner 类

Android 测试 API 是基于 JUnit 扩展而来，并添加了与 Android 平台相关的测试 API。

**JUnit**

你可以直接使用 JUnit 中相关 API 编写一些和平台无关的测试用例（基于 TestCase）, Android  测试 API 中提供了一个 TestCase 的子类 AndroidTestCase ，可以用来编写一些 Android 相关的对象的测试用例，AndroidTestCase 支持一些和平台相关的 setup,teardown 以及 setup 方法。

你也可以直接使用 JUnit 的 Assert 方法 显示测试结果，这些 Assert 方法可以通过比较预期的值和实际的值，如果不同可以排除异常。Android 测试 API 扩展了一些 Assert 方法用于支持和 Android 平台相关的比较。

要注意的是，Android 测试 API 支持 JUnit 3 代码风格，而不支持 JUnit 4 代码风格，也只能使用 InstrumentationTestRunner 来运行测试用例。

**Instrumentation**

Android 的 Instrumentation 提供了一些“钩子”方法连接到 Android 操作系统中，可以独立控制 Android 组件（Activity，Service 等）的生命周期，并可以控制 Android 如何调用一个应用。

在通常情况下（普通的 Android 应用），Android 的 activity，Service 等的生命周期是由 Android 操作系统来控制的。 比如一个 Activity 的生命周期开始于 onCreate (由某个 Intent 激活），然后是 onResume. 可以参见 [Android 简明开发教程五：Activities](http://www.imobilebbs.com/wordpress/?p=853)。 应用程序本身无法直接控制这些生命周期状态的切换。但使用 Instrumatation API 时你可以直接调用这些方法。

Instrumentation API 也可以支持强制某个应用和另一个已经在运作的应用运行在同一个进程中，这在通常的情况下是不可能实现的。

使用 Instrumentation API 你可以直接调用 Activity 或是 Service 的生命周期回调函数，从而可以让你运行一步一步的运行 Activity 或是 Service 的生命周期函数。如下例显示了如何使用 Instrumentation API 来测试 Activity 保持和恢复 State。

```

    // Start the main activity of the
    // application under test
    mActivity = getActivity();
    
    // Get a handle to the Activity object's
    //main UI widget, a Spinner
    mSpinner
    = (Spinner)mActivity
     .findViewById(com.android.example.spinner.R.id.Spinner01);
    
    // Set the Spinner to a known position
    mActivity.setSpinnerPosition(TEST_STATE_DESTROY_POSITION);
    
    // Stop the activity - The onDestroy()
    //method should save the state of the Spinner
    mActivity.finish();
    
    // Re-start the Activity - the onResume()
    //method should restore the state of the Spinner
    mActivity = getActivity();
    
    // Get the Spinner's current position
    int currentPosition = mActivity.getSpinnerPosition();
    
    // Assert that the current position is the
    //same as the starting position
    assertEquals(TEST_STATE_DESTROY_POSITION, currentPosition);
    
```

其中关键的一个方法是 getActivity()，只有调用 getActivity() 后被测试的 activity 才会启动。此外 Instrumentation API 允许把测试项目和被测试的应用项目运行到同一个进程中，从而在测试代码中可以直接调用被测试应用的方法和访问其成员。

**Test case 相关类**

Android 提供了多个由 Testcase 或 Assert 派生而来的子类以支持 Android 平台相关的 setup,teardown 和其它辅助方法。

- AndroidTestCase 为一 Android 平台下通用的测试类，它支持所有 JUnit 的 Assert 方法和标准的 setUp 和 tearDown 方法，并可以用来测试 Android permission 。
- 组件相关的测试类如测试 activity, Content provider ,Service 相关的测试类，Android 没有提供单独的用来测试 BroadcastReceiver 的测试类，而是可以通过发送 Intent 对象来检测 Broadcast Receiver 的反应结果来测试 BroadcastReceiver。
- ApplicationTestCase 可以用来测试 Application 对象。
- InstrumentationTestCase 如果你要使用 Instrumentation API，那么你必须使用 InstrumentationTestCase 或其子类。

**Assertion classes**

Android 测试中可以使用 JUnit 中提供的 Assert 方法来显示测试结果。除此之外，Testing API 还提供了 MoreAsserts 和 ViewAsserts 类。其中 MoreAsserts 支持更多的比较方法包括 RegEx(正则）比较等。ViewAsserts 可以用来校验 UI View。

**Mock object classes**

android.test.mock 包中定义一些测试“桩”类，如 MockApplication，MockContentProvider ,MockContext，MockCursor, MockPackagManager 等用例帮助测试。

后面将具体介绍如何使用这些 API 来编写测试用例。

Tags: [Android](http://www.imobilebbs.com/wordpress/archives/tag/android) [测试](http://www.imobilebbs.com/wordpress/archives/tag/%e6%b5%8b%e8%af%95)