# Searching Algorithm
> Algorithm is a sequence of stpes for accomplishing solving problems.

### Linear Search: 
> It is a searching algorithm that starts at a beginning of a list, and check each element until the key is found or the end of the list is reached.

### Features 
> Searching at first element one-by-one until the key is found.
> It will compare all element if the key is not present.

### Linear Search Algorithm
```
import java.util.Scanner;

public class LinearSearchDemo {
   private static int linearSearch(int[] numbers, int key) {
      for (int i = 0; i < numbers.length; i++) {
         if (numbers[i] == key) {
            return i;
         }
      }
      return -1; // not found
   }

   // Main program to test the linearSearch() method
   public static void main(String[] args) {
      int[] numbers = { 2, 4, 7, 10, 11, 32, 45, 87 };
      System.out.print("NUMBERS: ");
      for (int i = 0; i < numbers.length; i++) {
         System.out.print(numbers[i] + " ");
      }
      System.out.println();
      
      Scanner scnr = new Scanner(System.in);
      System.out.print("Enter an integer value: ");
      int key = scnr.nextInt();
      int keyIndex = linearSearch(numbers, key);
      
      if (keyIndex == -1) {
         System.out.println(key + " was not found.");
      }
      else {
         System.out.printf("Found %d at index %d.\n", key, keyIndex);
      }
   }
}
```
### Binary Search
> Linear search may require searching all list elements, which can lead to long runtimes.   For example, searching for a contact on a smartphone one-by-one from first to last can be time consuming.    Because a contact list is sorted, a faster search, known as binary search

> Definition: a faster algorithm for searching a list if the list's elements are sorted and directly accessible (such as an array).
> Process: Binary search first checks the middle element of the list. If the search key is found, the algorithm returns the matching location.   If the search key is not found, the algorithm repeats the search on the remaining left sublist (if the search key was less than the middle element) or the remaining right sublist (if the search key was greater than the middle element).

### Binary Search Efficiency
> Binary search is incredibly efficient in finding an element within a sorted list.
For a 32 element list, if the search key is not found, the search space is halved to have 16 elements, then 8, 4, 2, 1, and finally none, requiring only 6 steps.
For an N element list, the maximum number of steps required to reduce the search space to an empty sublist is [log2N] + 1 = 6.

### Binary Search Algorithm
```
import java.util.Scanner;

public class BinarySearchDemo {
   private static int binarySearch(int[] numbers, int key) {
      // Variables to hold the low, middle and high indices
      // of the area being searched. Starts with entire range.
      int low = 0;
      int mid = numbers.length / 2;
      int high = numbers.length - 1;
   
      // Loop until "low" passes "high"
      while (high >= low) {
         // Calculate the middle index
         mid = (high + low) / 2;

         // Cut the range to either the left or right half,
         // unless numbers[mid] is the key
         if (numbers[mid] < key) {
            low = mid + 1;
         }
         else if (numbers[mid] > key) {
            high = mid - 1;
         }
         else {
            return mid;
         }
      }
   
      return -1; // not found
   }

   // Main program to test the binarySearch() method
   public static void main(String[] args) {
      int[] numbers = { 2, 4, 7, 10, 11, 32, 45, 87 };
      System.out.print("NUMBERS: ");
      for (int i = 0; i < numbers.length; i++) {
         System.out.print(numbers[i] + " ");
      }
      System.out.println();
      
      Scanner scnr = new Scanner(System.in);
      System.out.print("Enter an integer value: ");
      int key = scnr.nextInt();
      int keyIndex = binarySearch(numbers, key);
      
      if (keyIndex == -1) {
         System.out.println(key + " was not found.");
      }
      else {
         System.out.printf("Found %d at index %d.\n", key, keyIndex);
      }
   }
}
```

