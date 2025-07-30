
## 🔍 Sliding Window Pattern — Explained in Simple English

### 📘 What is it?

The **Sliding Window pattern** is used when you are asked to:

* Work with **contiguous (next to each other)** elements (like subarrays or substrings),
* And want to **find the best or average result** within those ranges.

Instead of checking every possible subarray, you can **slide a fixed-size window** through the array, improving time from O(N\*K) to **O(N)**.

---

### ✅ When to Use It

Use this when:

* You’re working with **arrays or strings**,
* You’re dealing with **subarrays or substrings**,
* The problem asks for things like:

  * Maximum/Minimum/Average sum
  * Longest substring with conditions
  * Number of valid subarrays

---

## 🧠 Real-Life Analogy

Imagine a **magnifying glass** moving across a book line by line, focusing only on 5 words at a time. Instead of re-reading all 5 words again when you move forward, you just **remove the first word** and **add the next one** — faster, right? That’s how sliding window works.

---

## 🧪 Example Problem (Average of all subarrays of size K)

```python
def find_averages_of_subarrays(k, arr):
    result = []
    window_sum = 0
    window_start = 0

    for window_end in range(len(arr)):
        window_sum += arr[window_end]  # Add the next element

        # Slide the window if we hit the window size `k`
        if window_end >= k - 1:
            result.append(window_sum / k)      # Calculate average
            window_sum -= arr[window_start]    # Subtract the element going out
            window_start += 1                  # Slide the window ahead

    return result
```

---

## 🧰 Sliding Window Pattern – Master Template

## 🧰 C++ Sliding Window Template (Generic)

```cpp
// Use for fixed or variable sliding window
for (int end = 0; end < n; end++) {
    // Expand the window (add arr[end] or s[end] to window state)

    while (/* window condition broken */) {
        // Shrink the window from the start
        // (remove arr[start] or s[start] from window state)
        start++;
    }

    // Use the current window: end - start + 1
}
```
---

## ⚒️ Tips and Tricks

| Use Case                  | Technique                                                         |
| ------------------------- | ----------------------------------------------------------------- |
| Fixed-size window         | Check `if window_end >= k - 1`                                    |
| Variable-size window      | Use `while` loop to shrink based on condition                     |
| Longest subarray          | Use `max_length = max(max_length, window_end - window_start + 1)` |
| Frequency/Character Count | Use a dictionary or hashmap inside window                         |
| Remove duplicates         | Use a set to track seen elements                                  |

---

## 🧪 Common Problems That Use Sliding Window

1. **Maximum Sum Subarray of Size K**
2. **Longest Substring Without Repeating Characters**
3. **Minimum Size Subarray Sum**
4. **Permutation in String**
5. **Longest Substring with K Distinct Characters**

---
Below here are some of the **template-based solutions** using the **Sliding Window pattern**, each representing a different use case:

---

## ✅ 1. **Maximum Sum Subarray of Size K**

```cpp
int maxSumSubarrayOfSizeK(const vector<int>& nums, int k) {
    int maxSum = 0, windowSum = 0;

    for (int end = 0; end < nums.size(); end++) {
        windowSum += nums[end];

        if (end >= k - 1) {
            maxSum = max(maxSum, windowSum);
            windowSum -= nums[end - k + 1];
        }
    }

    return maxSum;
}
```

---

## ✅ 2. **Longest Substring Without Repeating Characters**

```cpp
int lengthOfLongestSubstring(string s) {
    unordered_set<char> charSet;
    int start = 0, maxLength = 0;

    for (int end = 0; end < s.length(); end++) {
        while (charSet.count(s[end])) {
            charSet.erase(s[start]);
            start++;
        }
        charSet.insert(s[end]);
        maxLength = max(maxLength, end - start + 1);
    }

    return maxLength;
}
```

---

## ✅ 3. **Minimum Size Subarray Sum**

```cpp
int minSubArrayLen(int target, vector<int>& nums) {
    int minLen = INT_MAX, sum = 0, start = 0;

    for (int end = 0; end < nums.size(); end++) {
        sum += nums[end];

        while (sum >= target) {
            minLen = min(minLen, end - start + 1);
            sum -= nums[start];
            start++;
        }
    }

    return minLen == INT_MAX ? 0 : minLen;
}
```

---

## ✅ 4. **Permutation in String**

```cpp
bool checkInclusion(string pattern, string text) {
    unordered_map<char, int> freq;
    for (char c : pattern) freq[c]++;

    int matched = 0, start = 0;
    for (int end = 0; end < text.size(); end++) {
        char right = text[end];
        if (freq.count(right)) {
            freq[right]--;
            if (freq[right] == 0) matched++;
        }

        if (end >= pattern.size()) {
            char left = text[start++];
            if (freq.count(left)) {
                if (freq[left] == 0) matched--;
                freq[left]++;
            }
        }

        if (matched == freq.size()) return true;
    }

    return false;
}
```

---

## ✅ 5. **Longest Substring with K Distinct Characters**

```cpp
int longestSubstringWithKDistinct(string s, int k) {
    unordered_map<char, int> charFreq;
    int start = 0, maxLength = 0;

    for (int end = 0; end < s.size(); end++) {
        charFreq[s[end]]++;

        while (charFreq.size() > k) {
            charFreq[s[start]]--;
            if (charFreq[s[start]] == 0) charFreq.erase(s[start]);
            start++;
        }

        maxLength = max(maxLength, end - start + 1);
    }

    return maxLength;
}
```

---

## 🧠 Conclusion

The **Sliding Window** pattern is one of the most practical and widely applicable techniques in DSA. It helps reduce time complexity from **O(N²) to O(N)** in many problems related to arrays and strings.

### ✨ Master this pattern and you'll unlock:

* Efficient solutions to many medium/hard problems
* Real confidence in coding interviews
* A strong base to tackle patterns like **two pointers**, **prefix sums**, and **hash maps**

> 🔑 **Tip**: Identify if the problem is asking about **contiguous** elements and whether the window size is **fixed or variable** — that’s your signal to apply this pattern.

---
