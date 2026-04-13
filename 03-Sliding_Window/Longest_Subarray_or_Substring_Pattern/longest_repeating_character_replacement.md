# 🧩 Longest Repeating Character Replacement
## 🧠 Intuition

We can replace at most k characters to make all characters same.

## 👉 Key idea:

Maintain:
window size
frequency of most frequent char

Condition:

window_size - maxFreq <= k
## 🐢 Brute Force Approach
Check all substrings
Replace characters → check validity
```cpp
#include <string>
using namespace std;

int characterReplacement(string s, int k) {
    int n = s.size();
    int maxLen = 0;

    for (int i = 0; i < n; i++) {
        int freq[26] = {0};
        int maxFreq = 0;

        for (int j = i; j < n; j++) {
            freq[s[j] - 'A']++;
            maxFreq = max(maxFreq, freq[s[j] - 'A']);

            int len = j - i + 1;
            if (len - maxFreq <= k) {
                maxLen = max(maxLen, len);
            }
        }
    }

    return maxLen;
}
```
## ⚡ Better Approach (Sliding Window)
(Not have)
## 🚀 Optimal Approach
### Steps:
Expand window
Track maxFreq
If invalid → shrink
Track max length
```cpp
#include <string>
#include <vector>
using namespace std;

int characterReplacement(string s, int k) {
    vector<int> freq(26, 0);
    int left = 0, maxFreq = 0, maxLen = 0;

    for (int right = 0; right < s.size(); right++) {
        freq[s[right] - 'A']++;
        maxFreq = max(maxFreq, freq[s[right] - 'A']);

        while ((right - left + 1) - maxFreq > k) {
            freq[s[left] - 'A']--;
            left++;
        }

        maxLen = max(maxLen, right - left + 1);
    }

    return maxLen;
}
```
## ⏱ Complexity Analysis
Time Complexity: O(n)
Space Complexity: O(1)
## 🔁 Pattern
Sliding Window
Max Frequency Trick
## 🌍 Real World Use
Error-tolerant pattern detection
Signal correction with limited modifications
