# LeetCode 1291 - Sequential Digits

## Java

```java
import java.util.*;

class Solution {
    public List<Integer> sequentialDigits(int low, int high) {

        List<Integer> res = new ArrayList<>();

        String digits = "123456789";

        int startLen = String.valueOf(low).length();
        int endLen = String.valueOf(high).length();

        for (int len = startLen; len <= endLen; len++) {

            for (int start = 0; start <= 9 - len; start++) {

                String sub = digits.substring(start, start + len);
                int num = Integer.parseInt(sub);

                if (num >= low && num <= high)
                    res.add(num);
            }
        }

        return res;
    }
}
```

---

## Python

```python
class Solution:
    def sequentialDigits(self, low: int, high: int) -> list[int]:

        res = []

        digits = "123456789"

        start_len = len(str(low))
        end_len = len(str(high))

        for length in range(start_len, end_len + 1):

            for start in range(10 - length):

                num = int(digits[start:start + length])

                if low <= num <= high:
                    res.append(num)

        return res
```

---

## C++

```cpp
class Solution {
public:
    vector<int> sequentialDigits(int low, int high) {

        vector<int> res;

        string digits = "123456789";

        int startLen = to_string(low).length();
        int endLen = to_string(high).length();

        for (int len = startLen; len <= endLen; len++) {

            for (int start = 0; start <= 9 - len; start++) {

                string sub = digits.substr(start, len);
                int num = stoi(sub);

                if (num >= low && num <= high)
                    res.push_back(num);
            }
        }

        return res;
    }
};
```

---

## C

```c
#include <stdlib.h>
#include <string.h>

int* sequentialDigits(int low, int high, int* returnSize) {

    int* res = (int*)malloc(sizeof(int) * 40);
    *returnSize = 0;

    char digits[] = "123456789";

    int startLen = 0, endLen = 0;
    int temp;

    temp = low;
    while (temp) {
        startLen++;
        temp /= 10;
    }

    temp = high;
    while (temp) {
        endLen++;
        temp /= 10;
    }

    for (int len = startLen; len <= endLen; len++) {

        for (int start = 0; start <= 9 - len; start++) {

            char sub[10];
            strncpy(sub, digits + start, len);
            sub[len] = '\0';

            int num = atoi(sub);

            if (num >= low && num <= high) {
                res[(*returnSize)++] = num;
            }
        }
    }

    return res;
}
```