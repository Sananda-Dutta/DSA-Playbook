# 🧩 Maximum Points You Can Obtain from Cards
## 🧠 Intuition

We pick exactly k cards from either start or end.

## 👉 Key idea:

Instead of picking from ends → think reverse
Find minimum subarray of size (n - k)
Subtract from total sum
## 🐢 Brute Force Approach
Try all combinations of picking from front/back
Track max sum
```cpp
#include <vector>
using namespace std;

int maxScore(vector<int>& cardPoints, int k) {
    int n = cardPoints.size();
    int maxSum = 0;

    for (int i = 0; i <= k; i++) {
        int sum = 0;

        // take i from front
        for (int j = 0; j < i; j++) {
            sum += cardPoints[j];
        }

        // take remaining from back
        for (int j = 0; j < k - i; j++) {
            sum += cardPoints[n - 1 - j];
        }

        maxSum = max(maxSum, sum);
    }

    return maxSum;
}
```
## ⚡ Better Approach (Sliding Window)
Total sum - minimum subarray of size n-k
## 🚀 Optimal Approach
Find subarray of length n-k with minimum sum
Answer = totalSum - minSubarraySum
```cpp
#include <vector>
#include <climits>
using namespace std;

int maxScore(vector<int>& cardPoints, int k) {
    int n = cardPoints.size();
    int totalSum = 0;

    for (int num : cardPoints) totalSum += num;

    int windowSize = n - k;
    if (windowSize == 0) return totalSum;

    int currSum = 0, minSum = INT_MAX;

    for (int i = 0; i < n; i++) {
        currSum += cardPoints[i];

        if (i >= windowSize) {
            currSum -= cardPoints[i - windowSize];
        }

        if (i >= windowSize - 1) {
            minSum = min(minSum, currSum);
        }
    }

    return totalSum - minSum;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Sliding Window
Complementary Subarray
## 🌍 Real World Use
Optimizing resource selection from two ends
Game strategy problems
