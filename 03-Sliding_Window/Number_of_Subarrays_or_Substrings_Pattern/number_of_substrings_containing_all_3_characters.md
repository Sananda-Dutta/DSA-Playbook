# 🧩 Number of Substrings Containing All 3 Characters (a, b, c)
## 🧠 Intuition

We need substrings containing at least one 'a', 'b', and 'c'.

## 👉 Key idea:

Sliding window
When window is valid → all substrings starting from left to end are valid
## 🐢 Brute Force Approach
Generate all substrings
Check if they contain a, b, c
```cpp
#include <string>
using namespace std;

int numberOfSubstrings(string s) {
    int n = s.size();
    int count = 0;

    for (int i = 0; i < n; i++) {
        int freq[3] = {0};

        for (int j = i; j < n; j++) {
            freq[s[j] - 'a']++;

            if (freq[0] > 0 && freq[1] > 0 && freq[2] > 0) {
                count++;
            }
        }
    }

    return count;
}
```
## ⚡ Better Approach (Sliding Window Insight)
## 🚀 Optimal Approach
### Steps:
Maintain count of a, b, c
When valid:
Add (n - right) to answer
Shrink window
```cpp
#include <string>
using namespace std;

int numberOfSubstrings(string s) {
    int n = s.size();
    int count = 0;
    int freq[3] = {0};

    int left = 0;

    for (int right = 0; right < n; right++) {
        freq[s[right] - 'a']++;

        while (freq[0] > 0 && freq[1] > 0 && freq[2] > 0) {
            count += (n - right);
            freq[s[left] - 'a']--;
            left++;
        }
    }

    return count;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Sliding Window
Count Valid Substrings
## 🌍 Real World Use
Pattern detection in strings
Counting valid combinations in sequences
