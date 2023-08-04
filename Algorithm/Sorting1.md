# Sorting Algorithm
> Sorting is the process of converting a list of elements into ascending (or descending) order.
> For exmaple, given a list of numbers (17, 3, 44, 6, 9), the list after sorting is (3, 6, 9, 17, 44).
> You may have carried out sorting when arranging papers in alphabetical order, or arranging envelopes to have ascending zip codes (as required for bulk mailings).

### Problem
The challenge of sorting is that a program can't **"see"** the entire list to know where to move an element. 
Instead, a program is limited to simpler steps, typically **observing or swapping** just two elements at a time. 
So sorting just by swapping values is an important part of sorting algorithms.

Here are the list of sorting algorithm:
1. Selection Sort
2. Insertion Sort
3. Shell Sort
4. Quick Sort
5. Merge Sort
6. Radix Sort
7. etc, a lot of sorting algorithms.


### Selection Sort
> Selection sort is a sorting algorithm that treats the input as two parts, a sorted part and an unsorted part, and repeatedly selects the proper next value to move from the unsorted part to the end of the sorted part.

example code
```
for (i = 0; i < numbersSize - 1; ++i) {

   // Find index of smallest remaining element
   indexSmallest = i
   for (j = i + 1; j < numbersSize; ++j) {

      if (numbers[j] < numbers[indexSmallest]) {
         indexSmallest = j
      }
   }

   // Swap numbers[i] and numbers[indexSmallest]
   temp = numbers[i]
   numbers[i] = numbers[indexSmallest]
   numbers[indexSmallest] = temp
}
```
Description:
1. Selection sort treats the input as two parts, a sorted and unsorted part. Variables i and j keep track of the two parts.
2. The selection sort algorithm searches the unsorted part of the array for the smallest element; indexSmallest stores the index of the smallest element found.
3. Elements at i and indexSmallest are swapped.
4. Indices for the sorted and unsorted parts are updated.
5. The unsorted part is searched again, swapping the smallest element with the element at i.
6. The process repeats until all elements are sorted.


The selectionSort() method takes the array as a parameter, and has no return value since the array is sorted in-place by the algorithm.
The outer loop uses the variable i to hold the index position that will be sorted next in the array. 
The inner loop uses the variable j to examine all indices from i+1 to the end of the array. 
When the j loop finishes, the variable indexSmallest will store the index position of the smallest item in the array from i onward. 
The final step is to swap the values at position i and indexSmallest.

Final code
```
import java.util.Arrays;

public class SelectionSortDemo {
   private static void selectionSort(int[] numbers) {
      for (int i = 0; i < numbers.length - 1; i++) {
         // Find index of smallest remaining element
         int indexSmallest = i;
         for (int j = i + 1; j < numbers.length; j++) {
            if (numbers[j] < numbers[indexSmallest]) {
               indexSmallest = j;
            }
         }
         
         // Swap numbers[i] and numbers[indexSmallest]
         int temp = numbers[i];
         numbers[i] = numbers[indexSmallest];
         numbers[indexSmallest] = temp;
      }
   }

   public static void main(String[] args) {
      // Create an array of numbers to sort
      int[] numbers = { 10, 2, 78, 4, 45, 32, 7, 11 };
      
      // Display the contents of the array
      System.out.println("UNSORTED: " + Arrays.toString(numbers));
      
      // Call the selectionSort method
      selectionSort(numbers);
      
      // Display the sorted contents of the array
      System.out.println("SORTED: " + Arrays.toString(numbers));
   }
}
```

### Insertion Sort
description: The insertionSort() method has one parameter, numbers, which is an unsorted array of elements. The array is sorted in place.

The index variable i denotes the starting position of the current element in the unsorted part. Initially, the first element (i.e., element at index 0) is assumed to be sorted, so the outer for loop assigns i with 1 to begin. The inner while loop inserts the current element into the sorted part by repeatedly swapping the current element with the elements in the array's sorted part that are larger. Once a smaller or equal element is found in the array's sorted part, the current element has been inserted in the correct location and the while loop terminates.

#### Example Code
```
import java.util.Arrays;

public class InsertionSortDemo {
   private static void insertionSort(int[] numbers) {
      for (int i = 1; i < numbers.length; i++) {
         int j = i;
         while (j > 0 && numbers[j] < numbers[j - 1]) {
            // Swap numbers[j] and numbers [j - 1]
            int temp = numbers[j];
            numbers[j] = numbers[j - 1];
            numbers[j - 1] = temp;
            j--;
         }
      }
   }

   public static void main(String[] args) {
      // Create an array of numbers to sort
      int[] numbers = { 10, 2, 78, 4, 45, 32, 7, 11 };
      
      // Display the contents of the array
      System.out.println("UNSORTED: " + Arrays.toString(numbers));
      
      // Call the insertionSort method
      insertionSort(numbers);
      
      // Display the sorted contents of the array
      System.out.println("SORTED: " + Arrays.toString(numbers));
   }
}
```

### Shell Sort
#### Shell sort's interleaved lists
Shell sort is a sorting algorithm that treats the input as a collection of interleaved lists, and sorts each list individually with a variant of the insertion sort algorithm. Shell sort uses gap values to determine the number of interleaved lists. A gap value is a positive integer representing the distance between elements in an interleaved list. For each interleaved list, if an element is at index i, the next element is at index i + gap value.

Shell sort begins by choosing a gap value K and sorting K interleaved lists in place. Shell sort finishes by performing a standard insertion sort on the entire array. Because the interleaved parts have already been sorted, smaller elements will be close to the array's beginning and larger elements towards the end. Insertion sort can then quickly sort the nearly-sorted array.

Any positive integer gap value can be chosen. In the case that the array size is not evenly divisible by the gap value, some interleaved lists will have fewer items than others.

#### Insertion sort for interleaved lists
If a gap value of K is chosen, creating K entirely new lists would be computationally expensive. Instead of creating new lists, shell sort sorts interleaved lists in-place with a variation of the insertion sort algorithm. The insertion sort algorithm variant redefines the concept of "next" and "previous" items. For an item at index X, the next item is at X + K, instead of X + 1, and the previous item is at X - K instead of X - 1.

#### Shell sort algorithm
Shell sort begins by picking an arbitrary collection of gap values. For each gap value K, K calls are made to the insertion sort variant function to sort K interleaved lists. Shell sort ends with a final gap value of 1, to finish with the regular insertion sort.

Shell sort tends to perform well when choosing gap values in descending order. A common option is to choose powers of 2 minus 1, in descending order. Ex: For an array of size 100, gap values would be 63, 31, 15, 7, 3, and 1. This gap selection technique results in shell sort's time complexity being no worse than O(N^(3/2)).

Using gap values that are powers of 2 or in descending order is not required. Shell sort will correctly sort arrays using any positive integer gap values in any order, provided a gap value of 1 is included.

#### Example Code
```
void insertionSortInterleaved(int[] numbers, int startIndex, int gap) {
   for (int i = startIndex + gap; i < numbers.length; i += gap) {
      int j = i;
      while (j - gap >= startIndex && numbers[j] < numbers[j - gap]) {
         // Swap numbers[j] and numbers [j - gap]
         int temp = numbers[j];
         numbers[j] = numbers[j - gap];
         numbers[j - gap] = temp;
         j -= gap;
      }
   }
}
```
#### Shell Sort Algorithm
The shellSort() method calls the insertionSortInterleaved() method repeatedly using different gap sizes and start indices. Ex: If a gapValue is 3, then shellSort() will execute:

insertionSortInterleaved(numbers, 0, 3)
insertionSortInterleaved(numbers, 1, 3)
insertionSortInterleaved(numbers, 2, 3)
All values from zero to gap - 1 are used as startIndex. This process repeats for all gap values. The shellSort() method takes as parameters the array to be sorted, and the array of gap values to be used.
Here's an example code.
```
void shellSort(int[] numbers, int[] gapValues) {
   for (int g = 0; g < gapValues.length; g++) {
      for (int i = 0; i < gapValues[g]; i++) {
         insertionSortInterleaved(numbers, i, gapValues[g]);
      }
   }
}
```
