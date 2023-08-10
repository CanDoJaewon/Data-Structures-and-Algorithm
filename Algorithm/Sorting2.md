## Quick Sort
Quicksort is a sorting algorithm that repeatedly partitions the input into low and high parts (each part unsorted), 
and then recursively sorts each of those parts. To partition the input, quicksort chooses a pivot to divide the data into low and high parts. 
The **pivot** can be any value within the array being sorted, commonly the value of the middle array element. 
Ex: For the list (4, 34, 10, 25, 1), the middle element is located at index 2 (the middle of indices [0, 4]) and has a value of 10.

Once the pivot is chosen, the quicksort algorithm divides the array into two parts, referred to as the low partition and the high partition. 
All values in the low partition are less than or equal to the pivot value. 
All values in the high partition are greater than or equal to the pivot value. The values in each partition are not necessarily sorted. 
Ex: Partitioning (4, 34, 10, 25, 1) with a pivot value of 10 results in a low partition of (4, 1, 10) and a high partition of (25, 34). 
Values equal to the pivot may appear in either or both of the partitions.

### Partitioning Algorithm
The partitioning algorithm uses two index variables lowIndex and highIndex, initialized to the left and right sides of the current elements being sorted. 
As long as the value at index lowIndex is less than the pivot value, the algorithm increments lowIndex, because the element should remain in the low partition. 
Likewise, as long as the value at index highIndex is greater than the pivot value, the algorithm decrements highIndex, because the element should remain in the high partition. 
Then, if lowIndex >= highIndex, all elements have been partitioned, and the partitioning algorithm returns highIndex, which is the index of the last element in the low partition. 
Otherwise, the elements at indices lowIndex and highIndex are swapped to move those elements to the correct partitions. 
The algorithm then increments lowIndex, decrements highIndex, and repeats.

### Recursively Sorting Partitions
Once partitioned, each partition needs to be sorted. 
Quicksort is typically implemented as a recursive algorithm using calls to quicksort to sort the low and high partitions. 
This recursive sorting process continues until a partition has one or zero elements, and thus is already sorted.

### Quick Sort Runtime
The quicksort algorithm's runtime is typically O(N log N). 
Quicksort has several partitioning levels, the first level dividing the input into 2 parts, the second into 4 parts, the third into 8 parts, etc. 
At each level, the algorithm does at most N comparisons moving the lowIndex and highIndex indices. 
If the pivot yields two equal-sized parts, then there will be log N levels, requiring the N * log N comparisons.

### The partition() method
The quicksort algorithm works by partitioning a section of the unsorted array into a left part and a right part, based on a chosen element within the array called the pivot.
The partition() method has three parameters: the unsorted array, the start index, and the end index. 
When the method completes, the elements between the start and end indices are reorganized so that the elements in the left part are less than or equal to the pivot and the elements in the right part are greater than or equal to the pivot. The left and right parts may be different sizes, and the method returns the index of the last item in the left part. 
The left and right parts are not, themselves, sorted.

### The partition() method used by quicksort
```
int partition(int[] numbers, int startIndex, int endIndex) {
   // Select the middle value as the pivot.
   int midpoint = startIndex + (endIndex - startIndex) / 2;
   int pivot = numbers[midpoint];
   
   // "low" and "high" start at the ends of the array segment
   // and move towards each other.
   int low = startIndex;
   int high = endIndex;
   
   boolean done = false;
   while (!done) {
      // Increment low while numbers[low] < pivot
      while (numbers[low] < pivot) {
         low = low + 1;
      }
      
      // Decrement high while pivot < numbers[high]
      while (pivot < numbers[high]) {
         high = high - 1;
      }
      
      // If low and high have crossed each other, the loop
      // is done. If not, the elements are swapped, low is
      // incremented and high is decremented.
      if (low >= high) {
         done = true;
      }
      else {
         int temp = numbers[low];
         numbers[low] = numbers[high];
         numbers[high] = temp;
         low++;
         high--;
      }
   }

   // "high" is the last index in the left segment.
   return high;
}
```

### The quicksort() Algorithm
The quicksort() method uses recursion to sort the two parts of the array, thus sorting the full array. 
The method has three parameters: the unsorted array, the start index, and the end index. 
quicksort() starts by calling partition() to partition the array into left (low) and right (high) parts. 
quicksort() then calls itself, using recursion to sort the two array parts.
A program can sort an array by calling quicksort() and specifying startIndex as 0 and endIndex as the index of the last item in the array.
Here's a code exmple.
```
void quicksort(int[] numbers, int startIndex, int endIndex) {
   // Only attempt to sort the array segment if there are
   // at least 2 elements
   if (endIndex <= startIndex) {
      return;
   }
          
   // Partition the array segment
   int high = partition(numbers, startIndex, endIndex);

   // Recursively sort the left segment
   quicksort(numbers, startIndex, high);

   // Recursively sort the right segment
   quicksort(numbers, high + 1, endIndex);
}
```
### Full version of quicksort demo
```
import java.util.Arrays;

public class QuicksortDemo {
   private static int partition(int[] numbers, int startIndex, int endIndex) {
      // Select the middle value as the pivot.
      int midpoint = startIndex + (endIndex - startIndex) / 2;
      int pivot = numbers[midpoint];
   
      // "low" and "high" start at the ends of the array segment
      // and move towards each other.
      int low = startIndex;
      int high = endIndex;
   
      boolean done = false;
      while (!done) {
         // Increment low while numbers[low] < pivot
         while (numbers[low] < pivot) {
            low = low + 1;
         }
      
         // Decrement high while pivot < numbers[high]
         while (pivot < numbers[high]) {
            high = high - 1;
         }
      
         // If low and high have crossed each other, the loop
         // is done. If not, the elements are swapped, low is
         // incremented and high is decremented.
         if (low >= high) {
            done = true;
         }
         else {
            int temp = numbers[low];
            numbers[low] = numbers[high];
            numbers[high] = temp;
            low++;
            high--;
         }
      }

      // "high" is the last index in the left segment.
      return high;
   }
   
   private static void quicksort(int[] numbers, int startIndex, int endIndex) {
      // Only attempt to sort the array segment if there are
      // at least 2 elements
      if (endIndex <= startIndex) {
         return;
      }
          
      // Partition the array segment
      int high = partition(numbers, startIndex, endIndex);

      // Recursively sort the left segment
      quicksort(numbers, startIndex, high);

      // Recursively sort the right segment
      quicksort(numbers, high + 1, endIndex);
   }

   public static void main(String[] args) {
      // Create an array of numbers to sort
      int[] numbers = { 12, 18, 3, 7, 32, 14, 91, 16, 8, 57 };
      
      // Display the unsorted contents of the array
      System.out.println("UNSORTED: " + Arrays.toString(numbers));
      
      // Call the quicksort method
      quicksort(numbers, 0, numbers.length - 1);

      // Display the sorted contents of the array
      System.out.println("SORTED: " + Arrays.toString(numbers));
   }
}

```

## Merge Sort
Merge sort is a sorting algorithm that divides a list into two halves, recursively sorts each half, and then merges the sorted halves to produce a sorted list. 
The recursive partitioning continues until a list of 1 element is reached, as a list of 1 element is already sorted.

<img width="968" alt="Screenshot 2023-08-10 at 3 31 41 PM" src="https://github.com/CanDoJaewon/Data-Structures-and-Algorithm/assets/124026092/0b90a7aa-2712-48ba-8652-47d44b8e9ca6">


**The process:**
1. MergeSort recursively divides the list into two halves.
2. The list is divided until a list of 1 element is found.
3. A list of 1 element is already sorted.
4. At each level, the sorted lists are merged together while maintaining the sorted order.

**The partitioning process:**
The merge sort algorithm uses **"three index variables"** to keep track of the elements to sort for each recursive function call. 
The index variable **"i"** is the index of first element in the list, and the index variable **"k"** is the index of the last element.
The index variable **"j"** is used to divide the list into two halves. 
Elements from i to j are in the left half, and elements from j + 1 to k are in the right half.

### Merge Sort runtime
The merge sort algorithm's runtime is O(N log N). Merge sort divides the input in half until a list of 1 element is reached, which requires log N partitioning levels. 
At each level, the algorithm does about N comparisons selecting and copying elements from the left and right partitions, yielding N * log N comparisons.


### Summary and Final example code
Merge sort algorithm
Merge sort is a sorting algorithm that divides an array into 2 halves, recursively sorts each half, and then merges the sorted halves to produce a sorted array. 
Merge sort uses 2 methods: merge() and mergeSort(). The merge() method merges 2 sequential, sorted partitions within an array and has 4 parameters:

1. The array of numbers containing the 2 sorted partitions to merge
2. The start index of the first sorted partition
3. The end index of the first sorted partition
4. The end index of the second sorted partition


The mergeSort() method sorts a partition in an array and has 3 parameters:

1. The array containing the partition to sort
2. The start index of the partition to sort
3. The end index of the partition to sort
If the partition size is greater than 1, the mergeSort() method recursively sorts the left and right halves of the partition, then merges the sorted halves together.
When the start index is 0 and the end index is the array length minus 1, mergeSort() sorts the entire array.

```
import java.util.Arrays;

public class MergeSortDemo {
   private static void merge(int[] numbers, int i, int j, int k) {
      int mergedSize = k - i + 1;                // Size of merged partition
      int[] mergedNumbers = new int[mergedSize]; // Dynamically allocates temporary
                                                 // array for merged numbers
      int mergePos = 0;                          // Position to insert merged number
      int leftPos = i;                           // Initialize left partition position
      int rightPos = j + 1;                      // Initialize right partition position
      
      // Add smallest element from left or right partition to merged numbers
      while (leftPos <= j && rightPos <= k) {
         if (numbers[leftPos] <= numbers[rightPos]) {
            mergedNumbers[mergePos] = numbers[leftPos];
            leftPos++;
         }
         else {
            mergedNumbers[mergePos] = numbers[rightPos];
            rightPos++;
         }
         mergePos++;
      }
      
      // If left partition is not empty, add remaining elements to merged numbers
      while (leftPos <= j) {
         mergedNumbers[mergePos] = numbers[leftPos];
         leftPos++;
         mergePos++;
      }
   
      // If right partition is not empty, add remaining elements to merged numbers
      while (rightPos <= k) {
         mergedNumbers[mergePos] = numbers[rightPos];
         rightPos++;
         mergePos++;
      }
   
      // Copy merged numbers back to numbers
      for (mergePos = 0; mergePos < mergedSize; mergePos++) {
         numbers[i + mergePos] = mergedNumbers[mergePos];
      }
   }
   
   private static void mergeSort(int[] numbers, int i, int k) {
      int j = 0;
      
      if (i < k) {
         j = (i + k) / 2;  // Find the midpoint in the partition

         // Recursively sort left and right partitions
         mergeSort(numbers, i, j);
         mergeSort(numbers, j + 1, k);
            
         // Merge left and right partition in sorted order
         merge(numbers, i, j, k);
      }
   }

   public static void main(String[] args) {
      // Create an array of numbers to sort
      int[] numbers = { 61, 76, 19, 4, 94, 32, 27, 83, 58 };
      
      // Display the contents of the array
      System.out.println("UNSORTED: " + Arrays.toString(numbers));
      
      // Call the mergeSort method
      mergeSort(numbers, 0, numbers.length - 1);
      
      // Display the sorted contents of the array
      System.out.println("SORTED:   " + Arrays.toString(numbers));
   }
}
```

### Radix Sort
Buckets
Radix sort is a sorting algorithm designed specifically for integers. 
The algorithm makes use of a concept called buckets and is a type of bucket sort.

Any array of integer values can be subdivided into buckets by using the integer values' digits. 
A bucket is a collection of integer values that all share a particular digit value. 
Ex: Values 57, 97, 77, and 17 all have a 7 as the 1's digit, and would all be placed into bucket 7 when subdividing by the 1's digit.

<img width="950" alt="Screenshot 2023-08-04 at 3 04 46 PM" src="https://github.com/CanDoJaewon/Data-Structures-and-Algorithm/assets/124026092/7840ad71-41e4-4fff-8fe2-27f17b8ee413">

### Radix Sort Algorithm
It is a sorting algorithm specifically for an array of integers: 
The algorithm processes one digit at a time starting with the least significant digit and ending with the most significant. 
Two steps are needed for each digit. First, all array elements are placed into buckets based on the current digit's value. 
Then, the array is rebuilt by removing all elements from buckets, in order from lowest bucket to highest.

Radix sort can be implemented in Java using an ArrayList of ten ArrayList<Integer> objects for the buckets. 
The main loop iterates through each relevant digit. The first of two nested loops copies each array element to the appropriate bucket. 
The second nested loop concatenates buckets in order and copies elements back to the array.

When the main loop completes, the array is sorted by absolute value. 
Two additional lists are then built from the array, one with all negative elements, the other with all non-negative elements. 
Then, the reversed negative list is concatenated with the non-negative list into the array to produce the sorted result.

```
import java.util.ArrayList;
import java.util.Arrays;

public class RadixSortDemo {
   // Returns the maximum length, in number of digits, out of all array elements
   private static int radixGetMaxLength(int[] numbers) {
      int maxDigits = 0;
      for (int i = 0; i < numbers.length; i++) {
         int digitCount = radixGetLength(numbers[i]);
         if (digitCount > maxDigits) {
             maxDigits = digitCount;
         }
      }
      return maxDigits;
   }
   
   private static int radixGetLength(int value) {
      if (value == 0) {
         return 1;
      }
      
      int digits = 0;
      while (value != 0) {
         digits++;
         value /= 10;
      }
      return digits;
   }
   
   private static void radixSort(int[] numbers) {
      ArrayList<ArrayList<Integer>> buckets = new ArrayList<ArrayList<Integer>>();
      for (int i = 0; i < 10; i++) {
         buckets.add(new ArrayList<Integer>());
      }
      
      int copyBackIndex = 0;
      
      // Find the max length, in number of digits
      int maxDigits = radixGetMaxLength(numbers);
      
      int pow10 = 1;
      for (int digitIndex = 0; digitIndex < maxDigits; digitIndex++) {
         for (int i = 0; i < numbers.length; i++) {
            int num = numbers[i];
            int bucketIndex = (Math.abs(num) / pow10) % 10;
            buckets.get(bucketIndex).add(num);
         }
         
         // Copy buckets back into numbers array
         copyBackIndex = 0;
         for (int i = 0; i < 10; i++) {
            ArrayList<Integer> bucket = buckets.get(i);
            for (int j = 0; j < bucket.size(); j++) {
               numbers[copyBackIndex] = bucket.get(j);
               copyBackIndex++;
            }
            bucket.clear();
         }
         
         pow10 *= 10;
      }
      
      ArrayList<Integer> negatives = new ArrayList<Integer>();
      ArrayList<Integer> nonNegatives = new ArrayList<Integer>();
      for (int num : numbers) {
         if (num < 0) {
            negatives.add(num);
         }
         else {
            nonNegatives.add(num);
         }
      }
      
      // Copy sorted content to array - negatives in reverse, then non-negatives
      copyBackIndex = 0;
      for (int i = negatives.size() - 1; i >= 0; i--) {
         numbers[copyBackIndex] = negatives.get(i);
         copyBackIndex++;
      }
      for (int i = 0; i < nonNegatives.size(); i++) {
         numbers[copyBackIndex] = nonNegatives.get(i);
         copyBackIndex++;
      }
   }
    
   public static void main(String[] args) {
      // Create an array of numbers to sort
      int[] numbers = { -9, 47, 81, 101, -5, 38, -99, 96, 51, -999, -11, 64 };
      
      // Display the contents of the array
      System.out.println("UNSORTED: " + Arrays.toString(numbers));
      
      // Call the radixSort method
      radixSort(numbers);
      
      // Display the sorted contents of the array
      System.out.println("SORTED:   " + Arrays.toString(numbers));
   }
}
```


## Summary

<img width="950" alt="Screenshot 2023-08-07 at 10 53 28 AM" src="https://github.com/CanDoJaewon/Data-Structures-and-Algorithm/assets/124026092/ed0448f5-5b00-4e01-80f0-cbdd929fe63a">


<img width="973" alt="Screenshot 2023-08-07 at 10 53 55 AM" src="https://github.com/CanDoJaewon/Data-Structures-and-Algorithm/assets/124026092/17e68343-728e-4de6-b43f-b028b73d3665">








