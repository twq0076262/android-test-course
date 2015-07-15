# Android 测试教程(13):TestCase 示例

Android 测试框架是基于 JUnit 的，因此对一些和平台关系不大的类，可以直接使用 JUnit 中的 TestCase 来测试。

MorseCodeConverterTest 用来测试 MorseCodeConverter 类，MorseCodeConverter 的实现和 Android 平台联系不大，因此可以直接使用 TestCase 作为基类。

TestCase 由 Assert 类派生而来，Assert 提供了大量的 Assert方法，用来比较期望值和实际值。

本例代码如下：

```

    public class MorseCodeConverterTest extends TestCase {
    
     @SmallTest
     public void testCharacterS() throws Exception {
    
     long[] expectedBeeps = {
     MorseCodeConverter.DOT,
     MorseCodeConverter.DOT,
     MorseCodeConverter.DOT,
     MorseCodeConverter.DOT,
     MorseCodeConverter.DOT};
     long[] beeps = MorseCodeConverter.pattern('s');
    
     assertArraysEqual(expectedBeeps, beeps);
     }
    
     private void assertArraysEqual(long[] expected, long[] actual) {
     assertEquals("Unexpected array length.",
     expected.length, actual.length);
     for (int i = 0; i < expected.length; i++) {
     long expectedLong = expected[i];
     long actualLong = actual[i];
     assertEquals("Unexpected long at index: " + i,
     expectedLong, actualLong);
     }
     }
    }
    

```

为一个基本的 JUnit Testcase 测试，使用 assertEquals 来测试期望值和实际值。

Tags: [Android](http://www.imobilebbs.com/wordpress/archives/tag/android) [测试](http://www.imobilebbs.com/wordpress/archives/tag/%e6%b5%8b%e8%af%95)