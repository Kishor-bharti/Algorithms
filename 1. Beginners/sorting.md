## Sorting

1. Bubble Sort (optimised)

![bubble-sort](https://github.com/Kishor-bharti/MD-Resources/blob/09cf86de27a1ffa8531830df5fc7730d8d1802f7/bubble-640.gif)

```cpp
class Solution {
  public:
    void bubbleSort(vector<int>& arr) {
        int n = arr.size();

        for(int i = 0; i < n - 1; ++i) {
            bool isSwap = false;  

            for(int j = 0; j < n - i - 1; ++j) {
                if(arr[j] > arr[j + 1]) {
                    swap(arr[j], arr[j + 1]);
                    isSwap = true;  
                }
            }

            if(!isSwap) {
                return; 
            }
        }
    }
};

/*
* Time complexity: O(n^2) in worst case, O(n) in best case.
* Space complexity: O(1)
* Remark: Inplace, Simple, Linear time complexity in best case of optimised bubble sort algorithm!
*/

```
//////////////////////////////////////////////
---

2. Selection sort

![selection-sort](https://github.com/Kishor-bharti/MD-Resources/blob/09cf86de27a1ffa8531830df5fc7730d8d1802f7/selection-600.gif)

```cpp
class Solution {
  public:
    void selectionSort(vector<int>& arr) {
        int n = arr.size();

        for(int i = 0; i < n - 1; ++i) {
            int minIndex = i;

            for(int j = i + 1; j < n; ++j) {
                if(arr[j] < arr[minIndex]) {
                    minIndex = j;
                }
            }

            if(minIndex != i) {
                swap(arr[i], arr[minIndex]);
            }
        }
    }
};

/*
* Time Complexity:
*   Best Case    : O(n^2)
*   Average Case : O(n^2)
*   Worst Case   : O(n^2)
*
* Space Complexity: O(1)
*
* Remarks:
* - Unstable 
* - In-place sorting algorithm
* - Performs minimum number of swaps (at most n-1)
* - NOT adaptive (no early termination possible)
* - Cannot be optimized to O(n) for sorted input
*/
```

```cpp
// (Stable version)
class Solution {
  public:
    void stableSelectionSort(vector<int>& arr) {
        int n = arr.size();

        for(int i = 0; i < n - 1; ++i) {
            int minIndex = i;

            // find minimum element index
            for(int j = i + 1; j < n; ++j) {
                if(arr[j] < arr[minIndex]) {
                    minIndex = j;
                }
            }

            // instead of swap, shift elements
            int key = arr[minIndex];
            while(minIndex > i) {
                arr[minIndex] = arr[minIndex - 1];
                minIndex--;
            }
            arr[i] = key;
        }
    }
};

/*
* Time Complexity:
*   Best / Avg / Worst Case: O(n^2)
*
* Space Complexity: O(1)
*
* Remarks:
* - Stable version of Selection Sort
* - Preserves relative order of equal elements
* - Uses shifting instead of swapping
* - More assignments than normal selection sort
*/
```
//////////////////////////////////////////////
---
3. Insertion sort

![insertion-sort](https://github.com/Kishor-bharti/MD-Resources/blob/09cf86de27a1ffa8531830df5fc7730d8d1802f7/insertion-600.gif)

```cpp
class Solution {
  public:
    void insertionSort(vector<int>& arr) {
        int n = arr.size();

        for(int i = 1; i < n; ++i) {
            int key = arr[i];
            int j = i - 1;

            // Shift elements that are greater than key
            while(j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j--;
            }

            // Place key at its correct position
            arr[j + 1] = key;
        }
    }
};

/*
* Time Complexity:
*   Best Case    : O(n)    (already sorted)
*   Average Case : O(n^2)
*   Worst Case   : O(n^2)
*
* Space Complexity: O(1)
*
* Remarks:
* - In-place sorting algorithm
* - Stable (preserves relative order of equal elements)
* - Adaptive (faster on nearly sorted data)
* - Excellent for small datasets
*/

```
//////////////////////////////////////////////
---

4. Merge sort

![merge-sort](https://github.com/Kishor-bharti/MD-Resources/blob/09cf86de27a1ffa8531830df5fc7730d8d1802f7/merge-sort-400.gif)


```cpp
// merge-sort code...
```