# Android  测试教程(16):monkeyrunner 简介

如果你需要实现自动测试，Android 的 monkeyrunner 工具可以帮助你实现自动测试，它提供了一组 API 可以用来控制 Android 设备或模拟器，使用 monkeyrunner，你可以编写 Python 程序来安装 Android 应用或是测试包，运行应用或测试，发送按键消息，并可以截屏，然后保存在计算机中。monkeyrunner 主要目的是用来在应用程序或框架层次来测试应用程序或运行单元测试包，但你也可以用作其它目的。

monkeyrunner 工具包不同于 UI/Application Exerciser Monkey（也称为 Money)，money 通过 adb shell 来运行，可以模拟“猴子”随机按键或是发送系统消息给指定的应用来实现 Stress 测试。

monkeyrunner API 主要通过下面三个包：

- MonkeyRunner： 主要提供了 monkeyrunner 应用的辅助方法以及，用来链接设备或是模拟器的方法，并提供 UI 支持等。
- MonkeyDevice： 代表一个设备或是模拟器，提供安装，卸载应用的方法，启动一个 Activity，发送按键或是 Touch 事件等。
- MonkeyImage： 代表一个截屏图像，可以截取不同格式的图像，比较两个 MonkeyImage 图像，保存图像等。

下面为一个 Python 写的 monkeyrunner 应用， 因为涉及到 Python 语言，这里不详细说明了

```

    # Imports the monkeyrunner modules used by this program
    from com.android.monkeyrunner import MonkeyRunner, MonkeyDevice
    
    # Connects to the current device, returning a MonkeyDevice object
    device = MonkeyRunner.waitForConnection()
    
    # Installs the Android package. Notice that this method returns a boolean,
    # so you can test to see if the installation worked.
    device.installPackage('myproject/bin/MyApplication.apk')
    
    # sets a variable with the package's internal name
    package = 'com.example.android.myapplication'
    
    # sets a variable with the name of an Activity in the package
    activity = 'com.example.android.myapplication.MainActivity'
    
    # sets the name of the component to start
    runComponent = package + '/' + activity
    
    # Runs the component
    device.startActivity(component=runComponent)
    
    # Presses the Menu button
    device.press('KEYCODE_MENU','DOWN_AND_UP')
    
    # Takes a screenshot
    result = device.takeSnapshot()
    
    # Writes the screenshot to a file
    result.writeToFile('myproject/shot1.png','png')

```

详细的 API 说明请参考 [Android 文档](http://developer.android.com/guide/developing/tools/monkeyrunner_concepts.html) ，如果你需要实现自动测试，编写测试代码，可以使用 Python 通过 monkeyrunner API 来实现。

Tags: [Android](http://www.imobilebbs.com/wordpress/archives/tag/android) [测试](http://www.imobilebbs.com/wordpress/archives/tag/%e6%b5%8b%e8%af%95)
