# Tier 1: Essential C++ Functions (Must-Know for Every Problem)

These functions and features are the absolute bedrock of competitive programming and LeetCode in C++. You will use multiple items from this list in virtually every problem you solve.

---

## Table of Contents
1. [[TC: O(N log N) | SC: O(log N)] `sort` (with custom comparator / lambda)](#1-tc-on-log-n--sc-olog-n-sort-with-custom-comparator--lambda)
2. [[TC: O(1) amortized | SC: O(N)] `vector`, `pair`, `emplace_back`](#2-tc-o1-amortized--sc-on-vector-pair-emplace_back)
3. [[TC: O(log N) / O(1) | SC: O(N)] `map`, `set`, `unordered_map`, `unordered_set`](#3-tc-olog-n--o1--sc-on-map-set-unordered_map-unordered_set)
4. [[TC: O(log N) | SC: O(N)] `priority_queue` (min-heap via `greater<>`)](#4-tc-olog-n--sc-on-priority_queue-min-heap-via-greater)
5. [[TC: O(log N) | SC: O(1)] `lower_bound` / `upper_bound`](#5-tc-olog-n--sc-o1-lower_bound--upper_bound)
6. [[TC: O(1) | SC: O(1)] `min`, `max`, `swap`](#6-tc-o1--sc-o1-min-max-swap)
7. [[TC: O(N) | SC: O(1)] `reverse`](#7-tc-on--sc-o1-reverse)
8. [[TC: O(N) | SC: O(1)] `accumulate` (with `0LL`)](#8-tc-on--sc-o1-accumulate-with-0ll)
9. [[TC: O(1) | SC: O(1)] `ios::sync_with_stdio(false); cin.tie(nullptr);`](#9-tc-o1--sc-o1-iossync_with_stdiofalse-cintienullptr)
10. [[TC: O(1) | SC: O(N)] `queue`, `stack`, `deque`](#10-tc-o1--sc-on-queue-stack-deque)
11. [[TC: O(1) | SC: O(1)] `auto [a, b] = p;` (Structured Bindings)](#11-tc-o1--sc-o1-auto-a-b--p-structured-bindings)
12. [[TC: O(1) | SC: O(1)] `INT_MAX`, `LLONG_MAX`](#12-tc-o1--sc-o1-int_max-llong_max)
13. [[TC: O(N) | SC: O(1)] `memset`, `fill`](#13-tc-on--sc-o1-memset-fill)
14. [[TC: O(len) | SC: O(len)] `to_string`, `stoi`, `substr`](#14-tc-olen--sc-olen-to_string-stoi-substr)
15. [[TC: O(1) | SC: O(1)] `#define all(x)`](#15-tc-o1--sc-o1-define-allx)

---

### 1. [TC: O(N log N) | SC: O(log N)] `sort` (with custom comparator / lambda)
- **Time Complexity:** $O(N \log N)$
- **Space Complexity:** $O(\log N)$ auxiliary (introsort recursion stack)
- **Header:** `<algorithm>`
- **What it does:** Sorts elements in a range in $O(N \log N)$ time; lambdas allow custom ordering such as sorting intervals, descending order, or multi-criteria sorting.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<std::pair<int, int>> intervals = {{1, 4}, {2, 3}, {1, 2}};

    // Sort by start ascending; if start is equal, sort by end descending
    std::sort(intervals.begin(), intervals.end(), [](const auto& a, const auto& b) {
        if (a.first != b.first) return a.first < b.first;
        return a.second > b.second;
    });

    for (auto& [start, end] : intervals) {
        std::cout << "[" << start << "," << end << "] ";
    }
}
```
**Input:** `[(1, 4), (2, 3), (1, 2)]`
**Output:** `[1,4] [1,2] [2,3] `

---

### 2. [TC: O(1) amortized | SC: O(N)] `vector`, `pair`, `emplace_back`
- **Time Complexity:** $O(1)$ amortized for `emplace_back` and random access; $O(N)$ when reallocation occurs.
- **Space Complexity:** $O(N)$
- **Header:** `<vector>`, `<utility>`
- **What it does:** `vector` is a dynamic array, `pair` stores two heterogeneous values, and `emplace_back` constructs elements directly in container memory avoiding copies.

```cpp
#include <iostream>
#include <vector>
#include <utility>

int main() {
    std::vector<std::pair<int, std::string>> items;
    // In-place construction without creating temporary std::pair
    items.emplace_back(1, "apple");
    items.emplace_back(2, "banana");

    for (const auto& item : items) {
        std::cout << item.first << ":" << item.second << " ";
    }
}
```
**Input:** Insert `(1, "apple")`, `(2, "banana")`
**Output:** `1:apple 2:banana `

---

### 3. [TC: O(log N) / O(1) | SC: O(N)] `map`, `set`, `unordered_map`, `unordered_set`
- **Time Complexity:** `map`/`set`: $O(\log N)$ find/insert/delete; `unordered_map`/`unordered_set`: $O(1)$ average, $O(N)$ worst-case.
- **Space Complexity:** $O(N)$
- **Header:** `<map>`, `<set>`, `<unordered_map>`, `<unordered_set>`
- **What it does:** `map`/`set` store sorted unique keys in $O(\log N)$ using red-black trees; `unordered_map`/`unordered_set` provide average $O(1)$ lookups and frequency counting via hashing.

```cpp
#include <iostream>
#include <unordered_map>
#include <set>

int main() {
    std::unordered_map<char, int> freq;
    std::string s = "leetcode";
    for (char c : s) freq[c]++;

    std::set<int> ordered_unique = {5, 1, 3, 5, 1};

    std::cout << "freq['e']: " << freq['e'] << "\n";
    std::cout << "set: ";
    for (int x : ordered_unique) std::cout << x << " ";
}
```
**Input:** String `"leetcode"`, values `{5, 1, 3, 5, 1}`
**Output:**
```text
freq['e']: 3
set: 1 3 5 
```

---

### 4. [TC: O(log N) | SC: O(N)] `priority_queue` (min-heap via `greater<>`)
- **Time Complexity:** $O(1)$ peek (`top`), $O(\log N)$ `push` and `pop`, $O(N)$ for range constructor (heapify).
- **Space Complexity:** $O(N)$
- **Header:** `<queue>`
- **What it does:** Implements a binary heap providing $O(1)$ peek and $O(\log N)$ push/pop; defaults to max-heap, but `std::greater<T>` turns it into a min-heap.

```cpp
#include <iostream>
#include <queue>
#include <vector>

int main() {
    // Min-heap: smallest element always on top
    std::priority_queue<int, std::vector<int>, std::greater<int>> min_pq;
    for (int x : {5, 1, 8, 3}) min_pq.push(x);

    while (!min_pq.empty()) {
        std::cout << min_pq.top() << " ";
        min_pq.pop();
    }
}
```
**Input:** Push `5, 1, 8, 3`
**Output:** `1 3 5 8 `

---

### 5. [TC: O(log N) | SC: O(1)] `lower_bound` / `upper_bound`
- **Time Complexity:** $O(\log N)$ on random access iterators (vector, array); $O(N)$ on forward lists/sets.
- **Space Complexity:** $O(1)$
- **Header:** `<algorithm>`
- **What it does:** Binary search on sorted ranges: `lower_bound` finds the first element $\ge x$; `upper_bound` finds the first element $> x$ in $O(\log N)$ time.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> nums = {10, 20, 20, 20, 30};
    auto lb = std::lower_bound(nums.begin(), nums.end(), 20);
    auto ub = std::upper_bound(nums.begin(), nums.end(), 20);

    std::cout << "lower_bound index: " << (lb - nums.begin()) << "\n";
    std::cout << "upper_bound index: " << (ub - nums.begin()) << "\n";
}
```
**Input:** `nums = [10, 20, 20, 20, 30]`, target `20`
**Output:**
```text
lower_bound index: 1
upper_bound index: 4
```

---

### 6. [TC: O(1) | SC: O(1)] `min`, `max`, `swap`
- **Time Complexity:** $O(1)$ (or $O(K)$ for initializer list of $K$ elements).
- **Space Complexity:** $O(1)$
- **Header:** `<algorithm>`, `<utility>`
- **What it does:** `min` and `max` return the minimum or maximum of 2 or more values (via initializer list); `swap` exchanges values or container contents in $O(1)$.

```cpp
#include <iostream>
#include <algorithm>

int main() {
    int a = 15, b = 27;
    int smallest = std::min({a, b, 9, 42});
    int largest = std::max(a, b);
    std::swap(a, b);

    std::cout << "smallest: " << smallest << ", largest: " << largest << "\n";
    std::cout << "a: " << a << ", b: " << b << "\n";
}
```
**Input:** `a = 15, b = 27`, list `{15, 27, 9, 42}`
**Output:**
```text
smallest: 9, largest: 27
a: 27, b: 15
```

---

### 7. [TC: O(N) | SC: O(1)] `reverse`
- **Time Complexity:** $O(N)$ where $N$ is the number of elements in the range.
- **Space Complexity:** $O(1)$ in-place.
- **Header:** `<algorithm>`
- **What it does:** Reverses the elements of a sequence in-place in $O(N)$ time; useful for palindrome verification and reconstructing shortest paths.

```cpp
#include <iostream>
#include <string>
#include <algorithm>

int main() {
    std::string s = "algorithm";
    std::reverse(s.begin(), s.end());
    std::cout << s << "\n";
}
```
**Input:** `"algorithm"`
**Output:** `mhtirogla`

---

### 8. [TC: O(N) | SC: O(1)] `accumulate` (with `0LL`)
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$
- **Header:** `<numeric>`
- **What it does:** Computes the sum of elements in a range; supplying `0LL` as the initial accumulator avoids 32-bit integer overflow.

```cpp
#include <iostream>
#include <vector>
#include <numeric>

int main() {
    std::vector<int> nums = {1000000000, 1000000000, 1000000000};
    // 0LL guarantees long long accumulation (avoids 32-bit overflow)
    long long total = std::accumulate(nums.begin(), nums.end(), 0LL);
    std::cout << "Sum: " << total << "\n";
}
```
**Input:** `nums = [1000000000, 1000000000, 1000000000]`
**Output:** `Sum: 3000000000`

---

### 9. [TC: O(1) | SC: O(1)] `ios::sync_with_stdio(false); cin.tie(nullptr);`
- **Time Complexity:** $O(1)$
- **Space Complexity:** $O(1)$
- **Header:** `<iostream>`
- **What it does:** Disables synchronization between C++ standard streams and C `stdio`, and unties `cin` from `cout`, preventing I/O bottlenecks and TLE on large test cases.

```cpp
#include <iostream>

void fast_io() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);
}

int main() {
    fast_io();
    std::cout << "Fast I/O initialized\n";
}
```
**Input:** None
**Output:** `Fast I/O initialized`

---

### 10. [TC: O(1) | SC: O(N)] `queue`, `stack`, `deque`
- **Time Complexity:** $O(1)$ for push, pop, front, back, top.
- **Space Complexity:** $O(N)$ where $N$ is the number of stored elements.
- **Header:** `<queue>`, `<stack>`, `<deque>`
- **What it does:** Core linear adapters: `queue` (FIFO for BFS), `stack` (LIFO for DFS/monotonic stack), and `deque` (double-ended queue for sliding window maximum).

```cpp
#include <iostream>
#include <queue>
#include <stack>
#include <deque>

int main() {
    std::queue<int> q;   q.push(1); q.push(2);
    std::stack<int> st;  st.push(10); st.push(20);
    std::deque<int> dq;  dq.push_front(100); dq.push_back(200);

    std::cout << "queue front: " << q.front() << "\n";
    std::cout << "stack top: " << st.top() << "\n";
    std::cout << "deque back: " << dq.back() << "\n";
}
```
**Input:** Queue push 1, 2; Stack push 10, 20; Deque push 100 front, 200 back
**Output:**
```text
queue front: 1
stack top: 20
deque back: 200
```

---

### 11. [TC: O(1) | SC: O(1)] `auto [a, b] = p;` (Structured Bindings)
- **Time Complexity:** $O(1)$
- **Space Complexity:** $O(1)$
- **Header:** Built-in C++17 language feature
- **What it does:** Unpacks pairs, tuples, or struct members into distinct named variables cleanly (C++17), eliminating verbose `.first` and `.second`.

```cpp
#include <iostream>
#include <map>
#include <string>

int main() {
    std::map<std::string, int> scores = {{"Alice", 95}, {"Bob", 88}};

    for (const auto& [name, score] : scores) {
        std::cout << name << " got " << score << "\n";
    }
}
```
**Input:** Map `{"Alice": 95, "Bob": 88}`
**Output:**
```text
Alice got 95
Bob got 88
```

---

### 12. [TC: O(1) | SC: O(1)] `INT_MAX`, `LLONG_MAX`
- **Time Complexity:** $O(1)$ (compile-time constants)
- **Space Complexity:** $O(1)$
- **Header:** `<climits>`
- **What it does:** Defined in `<climits>` as the maximum values for 32-bit signed int ($\approx 2.14 \times 10^9$) and 64-bit signed long long ($\approx 9.22 \times 10^{18}$); used for minimum tracking.

```cpp
#include <iostream>
#include <climits>
#include <algorithm>

int main() {
    int min_val = INT_MAX;
    long long min_cost = LLONG_MAX;

    min_val = std::min(min_val, 42);
    std::cout << "min_val: " << min_val << "\n";
    std::cout << "INT_MAX: " << INT_MAX << "\n";
}
```
**Input:** Initialize tracking with `INT_MAX`
**Output:**
```text
min_val: 42
INT_MAX: 2147483647
```

---

### 13. [TC: O(N) | SC: O(1)] `memset`, `fill`
- **Time Complexity:** $O(N)$ where $N$ is byte count for `memset` or element count for `fill`.
- **Space Complexity:** $O(1)$
- **Header:** `<cstring>` (for `memset`), `<algorithm>` (for `fill`)
- **What it does:** `memset` sets blocks of memory byte-by-byte (fast for 0 and -1); `std::fill` sets any value across an iterator range safely.

```cpp
#include <iostream>
#include <cstring>
#include <vector>
#include <algorithm>

int main() {
    int memo[5];
    std::memset(memo, -1, sizeof(memo)); // Sets each byte to 0xFF (-1)

    std::vector<int> dp(5);
    std::fill(dp.begin(), dp.end(), 100); // Sets all values to 100

    std::cout << "memo[0]: " << memo[0] << ", dp[0]: " << dp[0] << "\n";
}
```
**Input:** Size 5 arrays
**Output:** `memo[0]: -1, dp[0]: 100`

---

### 14. [TC: O(len) | SC: O(len)] `to_string`, `stoi`, `substr`
- **Time Complexity:** `to_string`/`stoi`: $O(D)$ where $D$ is the number of digits; `substr(pos, len)`: $O(\text{len})$.
- **Space Complexity:** $O(\text{len})$ for new string allocations.
- **Header:** `<string>`
- **What it does:** `to_string` converts numbers to strings, `stoi` parses numeric strings into integers, and `substr(pos, len)` extracts a sub-string.

```cpp
#include <iostream>
#include <string>

int main() {
    std::string s = "leetcode2024";
    std::string prefix = s.substr(0, 8); // pos = 0, length = 8
    int year = std::stoi(s.substr(8, 4));
    std::string next_year = std::to_string(year + 1);

    std::cout << prefix << " -> " << year << " -> " << next_year << "\n";
}
```
**Input:** `"leetcode2024"`
**Output:** `leetcode -> 2024 -> 2025`

---

### 15. [TC: O(1) | SC: O(1)] `#define all(x)`
- **Time Complexity:** $O(1)$ (preprocessor macro expansion)
- **Space Complexity:** $O(1)$
- **Header:** Macro definition
- **What it does:** Ubiquitous macro that expands to `(x).begin(), (x).end()`, reducing boilerplate code in algorithms.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

#define all(x) (x).begin(), (x).end()

int main() {
    std::vector<int> nums = {4, 1, 3, 2};
    std::sort(all(nums));

    for (int x : nums) std::cout << x << " ";
}
```
**Input:** `nums = [4, 1, 3, 2]`
**Output:** `1 2 3 4 `
