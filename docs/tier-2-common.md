# Tier 2: Very Common C++ Functions & Utilities

These functions and utilities appear frequently in medium to hard LeetCode problems and competitive programming contests. Mastering them will drastically speed up your implementation time and reduce bugs.

---

## Table of Contents
16. [`*min_element`, `*max_element` [TC: O(N) | SC: O(1)]](#16-min_element-max_element)
17. [`unique` + `erase` [TC: O(N) | SC: O(1)]](#17-unique--erase)
18. [`iota` [TC: O(N) | SC: O(1)]](#18-iota)
19. [`gcd`, `lcm` [TC: O(log(min(a, b))) | SC: O(1)]](#19-gcd-lcm)
20. [`__builtin_popcount(ll)`, `__builtin_ctz`, `__builtin_clz` [TC: O(1) | SC: O(1)]](#20-__builtin_popcountll-__builtin_ctz-__builtin_clz)
21. [`next_permutation` [TC: O(N) | SC: O(1)]](#21-next_permutation)
22. [`count`, `count_if`, `find` [TC: O(N) | SC: O(1)]](#22-count-count_if-find)
23. [`binary_search` [TC: O(log N) | SC: O(1)]](#23-binary_search)
24. [`multiset` [TC: O(log N) | SC: O(N)]](#24-multiset)
25. [`bitset` [TC: O(N/64) | SC: O(N/64)]](#25-bitset)
26. [`function<>` for recursive lambdas [TC: O(1) call | SC: O(depth)]](#26-function-for-recursive-lambdas)
27. [`tie`, `tuple` [TC: O(1) | SC: O(1)]](#27-tie-tuple)
28. [`partial_sum` [TC: O(N) | SC: O(1) aux]](#28-partial_sum)
29. [`sqrt`, `pow`, `abs`, `ceil`, `floor` [TC: O(1) | SC: O(1)]](#29-sqrt-pow-abs-ceil-floor)
30. [`isdigit`, `isalpha`, `tolower`, `toupper` [TC: O(1) | SC: O(1)]](#30-isdigit-isalpha-tolower-toupper)
31. [`getline`, `stringstream` / `istringstream` [TC: O(L) | SC: O(L)]](#31-getline-stringstream--istringstream)
32. [`mt19937`, `uniform_int_distribution` [TC: O(1) | SC: O(1)]](#32-mt19937-uniform_int_distribution)
33. [`rotate` [TC: O(N) | SC: O(1)]](#33-rotate)
34. [`all_of`, `any_of`, `none_of` [TC: O(N) | SC: O(1)]](#34-all_of-any_of-none_of)
35. [`nth_element` [TC: O(N) avg | SC: O(log N)]](#35-nth_element)
36. [`__int128` [TC: O(1) | SC: 16B]](#36-__int128)
37. [`emplace`, `m.contains()`, `try_emplace` [TC: O(log N) / O(1) | SC: O(1)]](#37-emplace-mcontains-try_emplace)
38. [`rbegin`, `*s.rbegin()` [TC: O(1) | SC: O(1)]](#38-rbegin-srbegin)
39. [`next`, `prev`, `distance` [TC: O(1) / O(k) | SC: O(1)]](#39-next-prev-distance)
40. [`stable_sort` [TC: O(N log N) | SC: O(N)]](#40-stable_sort)

---

<a id="16-min_element-max_element"></a>
### 16. `*min_element`, `*max_element` [TC: O(N) | SC: O(1)]
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$
- **Header:** `<algorithm>`
- **What it does:** Finds the iterator to the smallest or largest element in a range in $O(N)$ time; dereference (`*`) to access the value.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> nums = {4, 1, 9, 2, 7};
    int min_val = *std::min_element(nums.begin(), nums.end());
    int max_idx = std::max_element(nums.begin(), nums.end()) - nums.begin();

    std::cout << "Min val: " << min_val << ", Max index: " << max_idx << "\n";
}
```
**Input:** `nums = [4, 1, 9, 2, 7]`
**Output:** `Min val: 1, Max index: 2`

---

<a id="17-unique--erase"></a>
### 17. `unique` + `erase` [TC: O(N) | SC: O(1)]
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$ in-place
- **Header:** `<algorithm>`, `<vector>`
- **What it does:** Standard C++ idiom that removes duplicate elements from a sorted container in $O(N)$ time by shifting unique elements and resizing.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> nums = {1, 2, 2, 3, 3, 3, 4};
    // unique shifts duplicates to end and returns new end iterator
    nums.erase(std::unique(nums.begin(), nums.end()), nums.end());

    for (int x : nums) std::cout << x << " ";
}
```
**Input:** `nums = [1, 2, 2, 3, 3, 3, 4]`
**Output:** `1 2 3 4 `

---

<a id="18-iota"></a>
### 18. `iota` [TC: O(N) | SC: O(1)]
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$ auxiliary
- **Header:** `<numeric>`
- **What it does:** Fills a range with sequentially increasing values starting from a base value in $O(N)$ time; ideal for Disjoint Set Union (DSU) parent initialization and index arrays.

```cpp
#include <iostream>
#include <vector>
#include <numeric>

int main() {
    std::vector<int> parent(5);
    std::iota(parent.begin(), parent.end(), 0); // Fills with 0, 1, 2, 3, 4

    for (int p : parent) std::cout << p << " ";
}
```
**Input:** Vector of size 5, initial value `0`
**Output:** `0 1 2 3 4 `

---

<a id="19-gcd-lcm"></a>
### 19. `gcd`, `lcm` [TC: O(log(min(a, b))) | SC: O(1)]
- **Time Complexity:** $O(\log(\min(a, b)))$ via Euclidean algorithm
- **Space Complexity:** $O(1)$
- **Header:** `<numeric>`
- **What it does:** Calculates the greatest common divisor and least common multiple of two integers in logarithmic time using the Euclidean algorithm (C++17).

```cpp
#include <iostream>
#include <numeric>

int main() {
    long long a = 12, b = 18;
    std::cout << "GCD: " << std::gcd(a, b) << "\n";
    std::cout << "LCM: " << std::lcm(a, b) << "\n";
}
```
**Input:** `a = 12, b = 18`
**Output:**
```text
GCD: 6
LCM: 36
```

---

<a id="20-__builtin_popcountll-__builtin_ctz-__builtin_clz"></a>
### 20. `__builtin_popcount(ll)`, `__builtin_ctz`, `__builtin_clz` [TC: O(1) | SC: O(1)]
- **Time Complexity:** $O(1)$ single CPU instruction
- **Space Complexity:** $O(1)$
- **Header:** Compiler built-in (GCC/Clang)
- **What it does:** Fast compiler intrinsics executed via single CPU instructions: `popcount` counts set bits (`1`s), `ctz` counts trailing zeros, and `clz` counts leading zeros.

```cpp
#include <iostream>

int main() {
    int mask = 18; // binary: 0001 0010
    std::cout << "popcount(18): " << __builtin_popcount(mask) << "\n";
    std::cout << "trailing zeros: " << __builtin_ctz(mask) << "\n";

    long long big_mask = 1ULL << 40;
    std::cout << "popcountll: " << __builtin_popcountll(big_mask) << "\n";
}
```
**Input:** `mask = 18 (0b10010)`, `big_mask = 2^40`
**Output:**
```text
popcount(18): 2
trailing zeros: 1
popcountll: 1
```

---

<a id="21-next_permutation"></a>
### 21. `next_permutation` [TC: O(N) | SC: O(1)]
- **Time Complexity:** $O(N)$ worst-case; amortized $O(1)$ over all $N!$ permutations
- **Space Complexity:** $O(1)$ in-place
- **Header:** `<algorithm>`
- **What it does:** Reorders a sequence into the lexicographically next greater permutation in $O(N)$ time; returns `false` when the sequence is reversed back to ascending order.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> p = {1, 2, 3};
    do {
        for (int x : p) std::cout << x;
        std::cout << " ";
    } while (std::next_permutation(p.begin(), p.end()));
}
```
**Input:** `p = [1, 2, 3]`
**Output:** `123 132 213 231 312 321 `

---

<a id="22-count-count_if-find"></a>
### 22. `count`, `count_if`, `find` [TC: O(N) | SC: O(1)]
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$
- **Header:** `<algorithm>`
- **What it does:** `count` counts occurrences of a value, `count_if` counts elements matching a boolean predicate, and `find` locates the first matching element.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> nums = {1, 4, 2, 4, 5, 4};
    int fours = std::count(nums.begin(), nums.end(), 4);
    int evens = std::count_if(nums.begin(), nums.end(), [](int x) { return x % 2 == 0; });
    auto it = std::find(nums.begin(), nums.end(), 5);

    std::cout << "Count of 4: " << fours << ", Evens: " << evens << ", Found at index: " << (it - nums.begin()) << "\n";
}
```
**Input:** `nums = [1, 4, 2, 4, 5, 4]`
**Output:** `Count of 4: 3, Evens: 4, Found at index: 4`

---

<a id="23-binary_search"></a>
### 23. `binary_search` [TC: O(log N) | SC: O(1)]
- **Time Complexity:** $O(\log N)$ on random access iterators
- **Space Complexity:** $O(1)$
- **Header:** `<algorithm>`
- **What it does:** Checks whether a target value exists within a sorted range in $O(\log N)$ time, returning a `bool`.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> sorted = {2, 5, 8, 12, 16, 23};
    bool exists = std::binary_search(sorted.begin(), sorted.end(), 12);
    bool missing = std::binary_search(sorted.begin(), sorted.end(), 10);

    std::cout << "12 found? " << std::boolalpha << exists << "\n";
    std::cout << "10 found? " << std::boolalpha << missing << "\n";
}
```
**Input:** `sorted = [2, 5, 8, 12, 16, 23]`, targets `12`, `10`
**Output:**
```text
12 found? true
10 found? false
```

---

<a id="24-multiset"></a>
### 24. `multiset` [TC: O(log N) | SC: O(N)]
- **Time Complexity:** $O(\log N)$ for `insert`, `find`, and single-element `erase(iterator)`; $O(\log N + K)$ for `erase(val)` where $K$ copies exist.
- **Space Complexity:** $O(N)$
- **Header:** `<set>`
- **What it does:** An ordered associative container that keeps elements sorted while permitting duplicates; supports $O(\log N)$ insertion, deletion, and search.

```cpp
#include <iostream>
#include <set>

int main() {
    std::multiset<int> ms = {5, 2, 5, 8, 2};
    // Erase a single instance of 2 using an iterator
    ms.erase(ms.find(2));

    for (int x : ms) std::cout << x << " ";
}
```
**Input:** Insert `{5, 2, 5, 8, 2}`, erase one `2`
**Output:** `2 5 5 8 `

---

<a id="25-bitset"></a>
### 25. `bitset` [TC: O(N/64) | SC: O(N/64)]
- **Time Complexity:** $O(N/64)$ for bitwise ops (`&`, `|`, `^`, shift); $O(1)$ for single bit `test`, `set`, `flip`.
- **Space Complexity:** $O(N/64)$ bytes ($N$ bits stored packed).
- **Header:** `<bitset>`
- **What it does:** Fixed-size sequence of $N$ bits with $O(N/64)$ space/time operations; ideal for subset sum DP, graph reachability, and boolean flags.

```cpp
#include <iostream>
#include <bitset>

int main() {
    std::bitset<8> b("10110010");
    std::cout << "Count: " << b.count() << "\n";
    std::cout << "Bit 1: " << b.test(1) << "\n";
    b.flip(); // Invert all bits
    std::cout << "Flipped: " << b << "\n";
}
```
**Input:** `"10110010"`
**Output:**
```text
Count: 4
Bit 1: 1
Flipped: 01001101
```

---

<a id="26-function-for-recursive-lambdas"></a>
### 26. `function<>` for recursive lambdas [TC: O(1) call | SC: O(depth)]
- **Time Complexity:** $O(1)$ dispatch overhead per invocation.
- **Space Complexity:** $O(\text{recursion depth})$ on call stack.
- **Header:** `<functional>`
- **What it does:** `std::function` encapsulates callable objects, allowing a lambda function to reference itself recursively without writing a separate helper method.

```cpp
#include <iostream>
#include <functional>

int main() {
    std::function<long long(int)> factorial = [&](int n) -> long long {
        if (n <= 1) return 1;
        return n * factorial(n - 1);
    };

    std::cout << "5! = " << factorial(5) << "\n";
}
```
**Input:** `5`
**Output:** `5! = 120`

---

<a id="27-tie-tuple"></a>
### 27. `tie`, `tuple` [TC: O(1) | SC: O(1)]
- **Time Complexity:** $O(K)$ where $K$ is the number of elements in the tuple.
- **Space Complexity:** $O(1)$
- **Header:** `<tuple>`
- **What it does:** `tuple` stores a fixed-size collection of heterogeneous values; `std::tie` unpacks tuples or creates lexicographical comparisons on the fly.

```cpp
#include <iostream>
#include <tuple>
#include <string>

int main() {
    std::tuple<int, std::string, double> student(101, "Alice", 3.9);
    int id;
    std::string name;
    double gpa;

    std::tie(id, name, gpa) = student;
    std::cout << id << ": " << name << " (" << gpa << ")\n";
}
```
**Input:** `(101, "Alice", 3.9)`
**Output:** `101: Alice (3.9)`

---

<a id="28-partial_sum"></a>
### 28. `partial_sum` [TC: O(N) | SC: O(1) aux]
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$ auxiliary memory (or $O(N)$ for destination buffer).
- **Header:** `<numeric>`
- **What it does:** Computes the prefix sums of a range in $O(N)$ time, writing the running sums into another container or in-place.

```cpp
#include <iostream>
#include <vector>
#include <numeric>

int main() {
    std::vector<int> nums = {2, 4, 6, 8};
    std::vector<int> pref(nums.size());
    std::partial_sum(nums.begin(), nums.end(), pref.begin());

    for (int x : pref) std::cout << x << " ";
}
```
**Input:** `nums = [2, 4, 6, 8]`
**Output:** `2 6 12 20 `

---

<a id="29-sqrt-pow-abs-ceil-floor"></a>
### 29. `sqrt`, `pow`, `abs`, `ceil`, `floor` [TC: O(1) | SC: O(1)]
- **Time Complexity:** $O(1)$ native CPU instructions.
- **Space Complexity:** $O(1)$
- **Header:** `<cmath>`, `<cstdlib>`
- **What it does:** Standard mathematical functions: square root, exponentiation, absolute value, round up, and round down.

```cpp
#include <iostream>
#include <cmath>

int main() {
    std::cout << "sqrt(25.0): " << std::sqrt(25.0) << "\n";
    std::cout << "pow(2.0, 10): " << std::pow(2.0, 10) << "\n";
    std::cout << "ceil(4.2): " << std::ceil(4.2) << "\n";
    std::cout << "floor(4.8): " << std::floor(4.8) << "\n";
    std::cout << "abs(-15): " << std::abs(-15) << "\n";
}
```
**Input:** Values `25.0, (2.0, 10), 4.2, 4.8, -15`
**Output:**
```text
sqrt(25.0): 5
pow(2.0, 10): 1024
ceil(4.2): 5
floor(4.8): 4
abs(-15): 15
```

---

<a id="30-isdigit-isalpha-tolower-toupper"></a>
### 30. `isdigit`, `isalpha`, `tolower`, `toupper` [TC: O(1) | SC: O(1)]
- **Time Complexity:** $O(1)$ table lookup / arithmetic.
- **Space Complexity:** $O(1)$
- **Header:** `<cctype>`
- **What it does:** Character classification and case-conversion functions from `<cctype>` for parsing strings and validating alphanumeric tokens.

```cpp
#include <iostream>
#include <cctype>

int main() {
    char c1 = '7', c2 = 'A';
    std::cout << "isdigit('7'): " << (bool)std::isdigit(c1) << "\n";
    std::cout << "isalpha('A'): " << (bool)std::isalpha(c2) << "\n";
    std::cout << "tolower('A'): " << (char)std::tolower(c2) << "\n";
    std::cout << "toupper('b'): " << (char)std::toupper('b') << "\n";
}
```
**Input:** Characters `'7', 'A', 'b'`
**Output:**
```text
isdigit('7'): 1
isalpha('A'): 1
tolower('A'): a
toupper('b'): B
```

---

<a id="31-getline-stringstream--istringstream"></a>
### 31. `getline`, `stringstream` / `istringstream` [TC: O(L) | SC: O(L)]
- **Time Complexity:** $O(L)$ where $L$ is the number of characters processed.
- **Space Complexity:** $O(L)$ internal stream buffer.
- **Header:** `<string>`, `<sstream>`
- **What it does:** Reads full lines including spaces (`getline`) and splits strings into whitespace-delimited tokens using stream extraction.

```cpp
#include <iostream>
#include <sstream>
#include <vector>

int main() {
    std::string line = "tree graph dp greedy";
    std::istringstream iss(line);
    std::string token;
    std::vector<std::string> words;

    while (iss >> token) {
        words.push_back(token);
    }

    std::cout << "Parsed " << words.size() << " words: ";
    for (const auto& w : words) std::cout << "[" << w << "] ";
}
```
**Input:** `"tree graph dp greedy"`
**Output:** `Parsed 4 words: [tree] [graph] [dp] [greedy] `

---

<a id="32-mt19937-uniform_int_distribution"></a>
### 32. `mt19937`, `uniform_int_distribution` [TC: O(1) | SC: O(1)]
- **Time Complexity:** $O(1)$ per random number generated.
- **Space Complexity:** $O(1)$ generator state buffer (approx 2.5 KB).
- **Header:** `<random>`, `<chrono>`
- **What it does:** Fast 32/64-bit Mersenne Twister pseudo-random number generator; essential for randomized quickselect and anti-hash hacking defense.

```cpp
#include <iostream>
#include <random>
#include <chrono>

int main() {
    std::mt19937 rng(1337); // Seed
    std::uniform_int_distribution<int> dist(1, 100);

    std::cout << "Random numbers: " << dist(rng) << " " << dist(rng) << "\n";
}
```
**Input:** Seed `1337`, Range `[1, 100]`
**Output:** `Random numbers: 42 16` *(depends on seed)*

---

<a id="33-rotate"></a>
### 33. `rotate` [TC: O(N) | SC: O(1)]
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$ in-place
- **Header:** `<algorithm>`
- **What it does:** Left-rotates elements in a range in $O(N)$ time so that the element pointed to by the middle iterator becomes the new first element.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> nums = {1, 2, 3, 4, 5};
    // Rotate so element 3 (index 2) becomes first
    std::rotate(nums.begin(), nums.begin() + 2, nums.end());

    for (int x : nums) std::cout << x << " ";
}
```
**Input:** `nums = [1, 2, 3, 4, 5]`, pivot at index 2
**Output:** `3 4 5 1 2 `

---

<a id="34-all_of-any_of-none_of"></a>
### 34. `all_of`, `any_of`, `none_of` [TC: O(N) | SC: O(1)]
- **Time Complexity:** $O(N)$ worst-case; short-circuits as soon as result is determined.
- **Space Complexity:** $O(1)$
- **Header:** `<algorithm>`
- **What it does:** Tests whether all, any, or none of the elements in a range satisfy a given predicate with short-circuit evaluation.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> nums = {2, 4, 6, 8};
    bool all_even = std::all_of(nums.begin(), nums.end(), [](int x) { return x % 2 == 0; });
    bool any_gt_5 = std::any_of(nums.begin(), nums.end(), [](int x) { return x > 5; });
    bool none_neg = std::none_of(nums.begin(), nums.end(), [](int x) { return x < 0; });

    std::cout << "all_even: " << all_even << ", any_gt_5: " << any_gt_5 << ", none_neg: " << none_neg << "\n";
}
```
**Input:** `nums = [2, 4, 6, 8]`
**Output:** `all_even: 1, any_gt_5: 1, none_neg: 1`

---

<a id="35-nth_element"></a>
### 35. `nth_element` [TC: O(N) avg | SC: O(log N)]
- **Time Complexity:** $O(N)$ average and $O(N)$ worst-case via Introselect.
- **Space Complexity:** $O(\log N)$ recursive call stack.
- **Header:** `<algorithm>`
- **What it does:** Rearranges elements in $O(N)$ average time so that the $n$-th position has the element that would be there if fully sorted; all preceding elements are $\le$ and following elements are $\ge$.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> nums = {9, 2, 7, 1, 5, 3};
    // Find the 3rd smallest element (0-indexed: index 2)
    std::nth_element(nums.begin(), nums.begin() + 2, nums.end());

    std::cout << "3rd smallest element: " << nums[2] << "\n";
}
```
**Input:** `nums = [9, 2, 7, 1, 5, 3]`, rank index `2`
**Output:** `3rd smallest element: 3`

---

<a id="36-__int128"></a>
### 36. `__int128` [TC: O(1) | SC: 16B]
- **Time Complexity:** $O(1)$ arithmetic operations.
- **Space Complexity:** 16 bytes (128 bits) per variable.
- **Header:** Built-in GCC extension
- **What it does:** GCC/Clang built-in 128-bit signed integer type to prevent overflow during intermediate calculations like $a \times b \pmod m$ or cross-multiplication.

```cpp
#include <iostream>

int main() {
    long long a = 2000000000LL;
    long long b = 2000000000LL;
    // a * b overflows 64-bit long long, but fits easily in __int128
    __int128 prod = (__int128)a * b;

    long long mod = 1000000007;
    long long res = (long long)(prod % mod);
    std::cout << "res: " << res << "\n";
}
```
**Input:** `a = 2e9, b = 2e9, mod = 1e9 + 7`
**Output:** `res: 999999979`

---

<a id="37-emplace-mcontains-try_emplace"></a>
### 37. `emplace`, `m.contains()`, `try_emplace` [TC: O(log N) / O(1) | SC: O(1)]
- **Time Complexity:** `std::map`: $O(\log N)$; `std::unordered_map`: $O(1)$ average.
- **Space Complexity:** $O(1)$ auxiliary per call.
- **Header:** `<map>`, `<unordered_map>`
- **What it does:** Modern associative container methods: `contains()` (C++20) checks key existence cleanly; `try_emplace` inserts a key-value pair only if the key doesn't already exist without constructing the value unnecessarily.

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

int main() {
    std::unordered_map<int, std::string> mp = {{1, "one"}};

    std::cout << "Contains 1? " << mp.contains(1) << "\n"; // C++20
    mp.try_emplace(1, "ONE_NEW"); // Does nothing because 1 exists
    mp.try_emplace(2, "two");     // Inserts (2, "two")

    std::cout << "mp[1]: " << mp[1] << ", mp[2]: " << mp[2] << "\n";
}
```
**Input:** Map with `{1: "one"}`, try emplacing keys `1` and `2`
**Output:**
```text
Contains 1? 1
mp[1]: one, mp[2]: two
```

---

<a id="38-rbegin-srbegin"></a>
### 38. `rbegin`, `*s.rbegin()` [TC: O(1) | SC: O(1)]
- **Time Complexity:** $O(1)$
- **Space Complexity:** $O(1)$
- **Header:** `<set>`, `<vector>`, `<iterator>`
- **What it does:** Returns a reverse iterator to the last element of a container; allows accessing the maximum element of a sorted `std::set` or `std::map` in $O(1)$.

```cpp
#include <iostream>
#include <set>

int main() {
    std::set<int> s = {10, 40, 20, 50, 30};
    int max_elem = *s.rbegin(); // Largest element
    int min_elem = *s.begin();  // Smallest element

    std::cout << "Min: " << min_elem << ", Max: " << max_elem << "\n";
}
```
**Input:** `set = {10, 40, 20, 50, 30}`
**Output:** `Min: 10, Max: 50`

---

<a id="39-next-prev-distance"></a>
### 39. `next`, `prev`, `distance` [TC: O(1) / O(k) | SC: O(1)]
- **Time Complexity:** `next`/`prev`: $O(1)$ on random-access iterators, $O(k)$ on bidirectional/forward; `distance`: $O(1)$ on random-access, $O(N)$ on others.
- **Space Complexity:** $O(1)$
- **Header:** `<iterator>`
- **What it does:** Iterator helpers: `next`/`prev` return an iterator advanced forward or backward by $n$ steps without modifying the original; `distance` calculates the number of elements between two iterators.

```cpp
#include <iostream>
#include <vector>
#include <iterator>

int main() {
    std::vector<int> nums = {10, 20, 30, 40, 50};
    auto it = nums.begin();
    auto it3 = std::next(it, 3); // Points to 40
    auto it2 = std::prev(it3, 1); // Points to 30

    std::cout << "*it3: " << *it3 << ", *it2: " << *it2 << "\n";
    std::cout << "distance: " << std::distance(it, it3) << "\n";
}
```
**Input:** `nums = [10, 20, 30, 40, 50]`
**Output:**
```text
*it3: 40, *it2: 30
distance: 3
```

---

<a id="40-stable_sort"></a>
### 40. `stable_sort` [TC: O(N log N) | SC: O(N)]
- **Time Complexity:** $O(N \log N)$ with extra buffer, $O(N \log^2 N)$ in-place.
- **Space Complexity:** $O(N)$ temporary buffer.
- **Header:** `<algorithm>`
- **What it does:** Sorts elements in $O(N \log N)$ time while guaranteeing that equal elements retain their original relative order.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

struct Student {
    std::string name;
    int grade;
};

int main() {
    std::vector<Student> students = {{"Alice", 90}, {"Bob", 85}, {"Charlie", 90}};
    std::stable_sort(students.begin(), students.end(), [](const auto& a, const auto& b) {
        return a.grade > b.grade;
    });

    for (const auto& s : students) {
        std::cout << s.name << ":" << s.grade << " ";
    }
}
```
**Input:** `[("Alice", 90), ("Bob", 85), ("Charlie", 90)]`
**Output:** `Alice:90 Charlie:90 Bob:85 ` *(Alice preserves order before Charlie)*
