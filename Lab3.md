# Lab Report 3
By: Sara Standlee
## Part 1 - Bugs
* A failure-inducing input for the buggy program (as a JUnit test):
  Below is the code for a JUnit test which causes a failure in the buggy program. The input is {1,2,3,5}, and we expect {5,3,2,1}. However, instead, we recieve {0,0,0,0}.
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
  Below is the code for a JUnit test which does not induce a failure. The input is an empty array { }, and the expected output is also an empty array { }. This test case passes: The buggy code works for this test case. 
  ```
  public class ArrayTests {
    @Test
    public void testReversed() {
      int[] input1 = { };
      assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
    }
  }
  ```

  
* The symptom, as the output of running the tests
  Below shows the output of running the tests. The failure of the test case with a non-empty array as an innput is the symptom.   
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
  The code after (note the line in the for-loop is changed, this is the code change required to fix the buggy code):
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
The main issue was the line `arr[i] = newArray[arr.length - i - 1];` in the 'before' code. This line needed to be replaced with the line `newArray[i] = arr[arr.length - i - 1];`. Before, the original array was being modified based on the new array (which is filled with the default zeroes). The new line `newArray[i] = arr[arr.length - i - 1];` fixes the issue because now the new array is being assigned values based on the original array, from back to front, which is what we wanted.  

  ## Part 2 - Researching Commands
* Consider the command `find`:
* Four interesting command line options / alternate ways to use the command:

  
  - `-name pattern`:
    - This command line option is commonly used in the form `find /path/to/search -name "filename.txt"` and is used to find files by name starting from the specified directory. It also can be used simply in the form `find -name "filename.txt"`. In this case, the `find` command will start searching for files named "filename.txt" from the current directory and its subdirectories. 
    - Example 1 of using `-name pattern`: \
      This example demonstrates using the `-name pattern` command line option for a file that is located in a *subdirectory*.
      ```
      saras@Sara MINGW64 ~/Documents/CSE12/docsearch/technical (main)
      $ find -name chapter-1.txt
      ./911report/chapter-1.txt
      ```
    - Example 2 of using `-name pattern`:
      This example demonstrates using the `-name pattern` command line option for a file that is located in a *nested directory*. 
      ```
      saras@Sara MINGW64 ~/Documents/CSE12/docsearch/technical (main)
      $ find -name Annual_Fee.txt
      ./government/Media/Annual_Fee.txt
      ```
    - Source for how I found out about this command: `man` command: `man find`. The manual page referenced through this command is a part of the POSIX Programmer's Manual.
   




  - `-path pattern`:
    - This command line option is used to search for files based on their complete paths. The entire path of a file must match the specified pattern for it to be considered a match. This command is commonly used in the form `find [starting directory] -path "/path/to/find"` and is used to find files by name, starting from the specified directory. It also can be used simply in the form `find -path "/path/to/find"`. In this case, the `find` command will start searching from the current working directory for files or directories that match the specified path pattern.
    - Example 1 of using `-path pattern`:
      This example demonstrates using the `-path pattern` command line option with the full path to a *directory* from the current working directory.
      ```
      saras@Sara MINGW64 ~/Documents/CSE12/docsearch/technical (main)
      $ find -path "./government/Alcohol_Problems"
      ./government/Alcohol_Problems
      ```
    - Example 2 of using `path pattern`:
      This example demonstrates using the `-path pattern` command line option with a relative wildcard path to a *file* from the current working directory.
      ```
      saras@Sara MINGW64 ~/Documents/CSE12/docsearch/technical (main)
      $ find -path "*/Session4-PDF.txt"
      ./government/Alcohol_Problems/Session4-PDF.txt
      ```
    - Source for how I found out about this command: `man` command: `man find`. The manual page referenced through this command is a part of the POSIX Programmer's Manual.

    

  - `-mtime n`:
    - This command line option finds files / directories based on their modification time. This command is commonly used in the form `find /path/to/search -mtime n`. It also can be used simply in the form `find -mtime n"`. In this case, the `find` command will start searching from the current working directory for files / directories that match the specified modification time. If we use a plus sign before `n`, this means we are looking for a file modified more than `n` days ago. If we use a negative sign before `n`, we are looking for a file modified less than `n` days ago. 
    - Example 1:
      This example demonstrates using the `-mtime n` command line option to find files / directories modified less than one day ago when *no such files exist*. Notice that there is no output in this case. 
      ```
      saras@Sara MINGW64 ~/Documents/CSE12/docsearch/technical (main)
      $ find -mtime -1
      ```
    - Example 2:
      Around several minutes after running the command above, I made a modification to the file `chapter-1.txt`. Now, this example uses the same command as the previous example to demonstrate usin the `-mtime n` command line option to find files / directories modified less than one day ago when *such files do exist*.
      ```
      saras@Sara MINGW64 ~/Documents/CSE12/docsearch/technical (main)
      $ find -mtime -1
      ./911report/chapter-1.txt
      ```
      - Source for how I found out about this command: `man` command: `man find`. The manual page referenced through this command is a part of the POSIX Programmer's Manual.
     



  - `-mtime n`:
    - This command line option finds files / directories based on their modification time. This command is commonly used in the form `find /path/to/search -







  
