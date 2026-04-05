# 🧩 Count Inversions
## 🧠 Intuition

An inversion is a pair (i, j) such that:
👉 i < j and arr[i] > arr[j]

## 👉 Key idea:

While merging in Merge Sort, if left > right → inversions exist
## 🐢 Brute Force Approach
Check all pairs (i, j)
```cpp
#include <vector>
using namespace std;

int countInversions(vector<int>& arr) {
    int n = arr.size();
    int count = 0;

    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            if (arr[i] > arr[j]) count++;
        }
    }

    return count;
}
```
## ⚡ Better Approach (if any)
No major improvement → go optimal
## 🚀 Optimal Approach (Merge Sort)
Divide array
Count inversions while merging

👉 If left[i] > right[j] → all remaining elements in left form inversions

```cpp
#include <vector>
using namespace std;

int merge(vector<int>& arr, int low, int mid, int high) {
    vector<int> temp;
    int left = low, right = mid + 1;
    int count = 0;

    while (left <= mid && right <= high) {
        if (arr[left] <= arr[right]) {
            temp.push_back(arr[left++]);
        } else {
            temp.push_back(arr[right++]);
            count += (mid - left + 1);
        }
    }

    while (left <= mid) temp.push_back(arr[left++]);
    while (right <= high) temp.push_back(arr[right++]);

    for (int i = low; i <= high; i++) {
        arr[i] = temp[i - low];
    }

    return count;
}

int mergeSort(vector<int>& arr, int low, int high) {
    int count = 0;
    if (low >= high) return count;

    int mid = (low + high) / 2;

    count += mergeSort(arr, low, mid);
    count += mergeSort(arr, mid + 1, high);
    count += merge(arr, low, mid, high);

    return count;
}

int countInversions(vector<int>& arr) {
    return mergeSort(arr, 0, arr.size() - 1);
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n log n)
Space Complexity: O(n)
## 🔁 Pattern
Divide & Conquer
Merge Sort
## 🌍 Real World Use
Measuring how far an array is from being sorted
Ranking systems / similarity metrics
