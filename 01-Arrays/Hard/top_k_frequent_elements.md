# 🧩 Top K Frequent Elements
## 🧠 Intuition

We need the k most frequent elements.

## 👉 Key idea:

Count frequencies
Extract top k using heap or bucket sort
## 🐢 Brute Force Approach
Count frequency
Sort by frequency
```cpp
#include <vector>
#include <unordered_map>
#include <algorithm>
using namespace std;

vector<int> topKFrequent(vector<int>& nums, int k) {
    unordered_map<int, int> mp;

    for (int num : nums) {
        mp[num]++;
    }

    vector<pair<int, int>> freq(mp.begin(), mp.end());

    sort(freq.begin(), freq.end(), [](auto& a, auto& b) {
        return a.second > b.second;
    });

    vector<int> result;
    for (int i = 0; i < k; i++) {
        result.push_back(freq[i].first);
    }

    return result;
}
```
## ⚡ Better Approach (Min Heap)
Maintain heap of size k
```cpp
#include <vector>
#include <unordered_map>
#include <queue>
using namespace std;

vector<int> topKFrequent(vector<int>& nums, int k) {
    unordered_map<int, int> mp;
    for (int num : nums) mp[num]++;

    priority_queue<pair<int,int>, vector<pair<int,int>>, greater<>> pq;

    for (auto& it : mp) {
        pq.push({it.second, it.first});
        if (pq.size() > k) pq.pop();
    }

    vector<int> result;
    while (!pq.empty()) {
        result.push_back(pq.top().second);
        pq.pop();
    }

    return result;
}
```
## 🚀 Optimal Approach (Bucket Sort)
Frequency range is limited (0 → n)
Use buckets
```cpp
#include <vector>
#include <unordered_map>
using namespace std;

vector<int> topKFrequent(vector<int>& nums, int k) {
    unordered_map<int, int> mp;
    for (int num : nums) mp[num]++;

    int n = nums.size();
    vector<vector<int>> bucket(n + 1);

    for (auto& it : mp) {
        bucket[it.second].push_back(it.first);
    }

    vector<int> result;

    for (int i = n; i >= 0 && result.size() < k; i--) {
        for (int num : bucket[i]) {
            result.push_back(num);
            if (result.size() == k) break;
        }
    }

    return result;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(n)
## 🔁 Pattern
HashMap + Heap
Bucket Sort
## 🌍 Real World Use
Trending items (top k searches, hashtags)
Frequency-based ranking systems
