# Lab Report 3
By: Sara Standlee
## Part 1 - Bugs
* A failure-inducing input for the buggy program (as a JUnit test): \
  The buggy program:
  ```
  public class ArrayExamples {
    // Changes the input array to be in reversed order
    static void reverseInPlace(int[] arr) {
      for(int i = 0; i < arr.length; i += 1) {
        arr[i] = arr[arr.length - i - 1];
      }
    }
  }
  ```
  Failure inducing input for the buggy program (as JUnit Test):
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
  	public void testReverseInPlace() {
      int[] input1 = { 3 };
      ArrayExamples.reverseInPlace(input1);
      assertArrayEquals(new int[]{ 3 }, input1);
  	}
  }
  ```
* The symptom, as the output of running the tests
* The bug, as the before-and-after code change required to fix it
  ```
  onee
  ```
  ```
  two
  ```
  \
Why this fixed the issue: \
one

  ## Part 2 - Researching Commands
