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
3. Shall Sort
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
