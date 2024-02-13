# Lab Report 3
By: Sara Standlee
## Part 1 - Bugs
* A failure-inducing input for the buggy program (as a JUnit test): \
  ```
  import static org.junit.Assert.*;
  import org.junit.*;

  public class ArrayTests {
    @Test
    public void testReversedMultipleElements() {
      int[] input1 = {1,2,3,5};
      assertArrayEquals(new int[]{5,3,2,1}, ArrayExamples.reversed(input1));
    }
  }
  ```
  JUnit message:
  ```
  arrays first differed at element [0]; expected:[5] but was:[0]
  at ArrayTests.testReversedMultipleElements(ArrayTests.java:22)
  ```

  
* An input that doesn't induce a failure (as a JUnit test):
  ```
  public class ArrayTests {
    @Test
    public void testReversed() {
      int[] input1 = { };
      assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
    }
  }
  ```
  This test passes.

  
* The symptom, as the output of running the tests
```
saras@Sara MINGW64 ~/Documents/CSE12/lab3 (main)
$ javac -cp ".;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar" *.java

saras@Sara MINGW64 ~/Documents/CSE12/lab3 (main)
$ java -cp ".;lib/junit-4.13.2.jar;lib/hamcrest-core-1.3.jar" org.junit.runner.JUnitCore ArrayTests
JUnit version 4.13.2
..E
Time: 0.005
There was 1 failure:
1) testReversedMultipleElements(ArrayTests)
arrays first differed at element [0]; expected:<5> but was:<0>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReversedMultipleElements(ArrayTests.java:22)
        ... 32 trimmed
Caused by: java.lang.AssertionError: expected:<5> but was:<0>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 38 more

FAILURES!!!
Tests run: 2,  Failures: 1
```


* The bug, as the before-and-after code change required to fix it \
  The code before:
  ```
  public class ArrayExamples {
    static int[] reversed(int[] arr) {
      int[] newArray = new int[arr.length];
      for(int i = 0; i < arr.length; i += 1) {
        arr[i] = newArray[arr.length - i - 1];
      }
      return arr;
    }
  }
  ```
  The code after:
  ```
  public class ArrayExamples {
    static int[] reversed(int[] arr) {
      int[] newArray = new int[arr.length];
      for(int i = 0; i < arr.length; i += 1) {
        newArray[i] = arr[arr.length - i - 1];
      }
      return newArray;
    }
  }
  ```
  JUnit Tests now pass:
  ```
  saras@Sara MINGW64 ~/Documents/CSE12/lab3 (main)
  $ javac -cp ".;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar" *.java
  
  saras@Sara MINGW64 ~/Documents/CSE12/lab3 (main)
  $ java -cp ".;lib/junit-4.13.2.jar;lib/hamcrest-core-1.3.jar" org.junit.runner.JUnitCore ArrayTests
  JUnit version 4.13.2
  ..
  Time: 0.01
  
  OK (2 tests)
  ```
  \
Why this fixed the issue: \
Te main issue was the line `arr[i] = newArray[arr.length - i - 1];` in the 'before' code. This line needed to be replaced with the line `newArray[i] = arr[arr.length - i - 1];`. Before, the original array was being modified based on the new array (which is filled with the default zeroes). The new line `newArray[i] = arr[arr.length - i - 1];` fixes the issue because now the new array is being assigned values based on the original array, from back to front, which is what we wanted.  

  ## Part 2 - Researching Commands
