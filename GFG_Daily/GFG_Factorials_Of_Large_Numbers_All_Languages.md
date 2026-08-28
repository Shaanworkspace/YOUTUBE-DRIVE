# GeeksforGeeks — Factorials of Large Numbers

Problem: https://www.geeksforgeeks.org/problems/factorials-of-large-numbers2508
Asked at: Morgan Stanley, Microsoft, Samsung, MakeMyTrip, MAQ Software, Adobe, Philips, BrowserStack

Store the factorial of n as a list/array of digits (most-significant first) and multiply
digit-by-digit with carry. This avoids overflow for n up to 1000 (or more) and is the
optimal interview solution GFG expects.

---

## Java

```java
class Solution {
    public ArrayList<Integer> factorial(int n) {
        ArrayList<Integer> digits = new ArrayList<>();
        digits.add(1);
        for (int i = 2; i <= n; i++) {
            int carry = 0;
            for (int j = digits.size() - 1; j >= 0; j--) {
                int value = digits.get(j) * i + carry;
                digits.set(j, value % 10);
                carry = value / 10;
            }
            while (carry > 0) {
                digits.add(0, carry % 10);
                carry = carry / 10;
            }
        }
        return digits;
    }
}
```

---

## Python

```python
class Solution:
    def factorial(self, n):
        digits = [1]
        for i in range(2, n + 1):
            carry = 0
            for j in range(len(digits) - 1, -1, -1):
                value = digits[j] * i + carry
                digits[j] = value % 10
                carry = value // 10
            while carry > 0:
                digits.insert(0, carry % 10)
                carry //= 10
        return digits
```

---

## C++

```cpp
class Solution {
  public:
    vector<int> factorial(int n) {
        vector<int> digits = {1};
        for (int i = 2; i <= n; i++) {
            int carry = 0;
            for (int j = (int)digits.size() - 1; j >= 0; j--) {
                int value = digits[j] * i + carry;
                digits[j] = value % 10;
                carry = value / 10;
            }
            while (carry > 0) {
                digits.insert(digits.begin(), carry % 10);
                carry /= 10;
            }
        }
        return digits;
    }
};
```

---

## C

```c
int* factorial(int n, int *size_of_array) {
    int cap = 5000;
    int *digits = (int*)malloc(cap * sizeof(int));
    digits[0] = 1;
    int len = 1;
    for (int i = 2; i <= n; i++) {
        int carry = 0;
        for (int j = 0; j < len; j++) {
            int value = digits[j] * i + carry;
            digits[j] = value % 10;
            carry = value / 10;
        }
        while (carry > 0) {
            if (len >= cap) {
                cap *= 2;
                digits = (int*)realloc(digits, cap * sizeof(int));
            }
            digits[len++] = carry % 10;
            carry /= 10;
        }
    }
    /* reverse so most-significant digit is first */
    for (int i = 0; i < len / 2; i++) {
        int t = digits[i];
        digits[i] = digits[len - 1 - i];
        digits[len - 1 - i] = t;
    }
    *size_of_array = len;
    return digits;
}
```
