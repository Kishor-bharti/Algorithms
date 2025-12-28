# Sorting

### Bubble Sort (optimised)

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

### Selection sort

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
### Insertion sort

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

### Merge sort

![merge-sort](https://github.com/Kishor-bharti/MD-Resources/blob/09cf86de27a1ffa8531830df5fc7730d8d1802f7/merge-sort-400.gif) (Recursive, Stable)

    
```cpp
// Recursive & Backtracking
class Solution {
    public:
        void mergeSort(Vector<int> &arr, int st, int end){
            if(st < end){
                int mid = st + (end - st)/2;

                //Recursive call for the left half
                mergeSort(arr, st, mid);

                //Recursive call for the right half
                mergeSort(arr, mid+1, end);

                //merge arr in sorted order while Backtracking
                merge(arr, st, mid, end);
            }
        }

        void merge(vector<int> &arr, int st, int mid, int end){
            vector<int> temp;
            int i = st, j = mid+1;

            while(i <= mid && j <= end){
                if(arr[i] <= arr[j]){
                    temp.push_back(arr[i]);
                    i++;
                }
                else{
                    temp.push_back(arr[j]);
                    j++;
                }
            }

            while(i <= mid){
                temp.push_back(arr[i]);
                i++;
            }

            while(j <= end){
                temp.push_back(arr[j]);
                j++;
            }

            for(int idx = 0; idx < temp.size(); idx++){
                arr[idx + st] = temp[idx];
            }
        }
};
/*
* Time Complexity:
*   Best / Average / Worst Case: O(n log n)
*
* Space Complexity: O(n)
*
* Remarks:
* - Easier to understand and implement
* - UNSTABLE (equal elements may change order)
* - Uses extra space
* - Good for learning divide & conquer
*/
```


```cpp
class Solution {
  public:
    void merge(vector<int>& arr, int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;

        vector<int> L(n1), R(n2);

        for(int i = 0; i < n1; ++i)
            L[i] = arr[left + i];

        for(int j = 0; j < n2; ++j)
            R[j] = arr[mid + 1 + j];

        int i = 0, j = 0, k = left;

        // merge the two sorted halves
        while(i < n1 && j < n2) {
            if(L[i] <= R[j]) {   // <= makes it stable
                arr[k++] = L[i++];
            } else {
                arr[k++] = R[j++];
            }
        }

        // copy remaining elements
        while(i < n1) arr[k++] = L[i++];
        while(j < n2) arr[k++] = R[j++];
    }

    void mergeSort(vector<int>& arr, int left, int right) {
        if(left >= right) return;

        int mid = left + (right - left) / 2;

        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
};

/*
* Time Complexity:
*   Best Case    : O(n log n)
*   Average Case : O(n log n)
*   Worst Case   : O(n log n)
*
* Space Complexity: O(n)
*
* Remarks:
* - Divide and Conquer algorithm
* - Stable sorting algorithm
* - Not in-place (uses extra memory)
* - Preferred when guaranteed O(n log n) time is required
*/
```