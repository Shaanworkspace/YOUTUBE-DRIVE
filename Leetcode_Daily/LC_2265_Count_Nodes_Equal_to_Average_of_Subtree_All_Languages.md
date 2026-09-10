# LeetCode 2265 - Count Nodes Equal to Average of Subtree

**Problem Link:** https://leetcode.com/problems/count-nodes-equal-to-average-of-subtree/

**Approach:** DFS — for each node, compute subtree sum and count, then check if node value equals sum/count.
Time: O(n) | Space: O(h) where h = tree height

---

## Java

```java
class Solution {
    int ans = 0;

    public int averageOfSubtree(TreeNode root) {
        dfs(root);
        return ans;
    }

    private int[] dfs(TreeNode node) {
        if (node == null) {
            return new int[]{0, 0};
        }

        int[] left = dfs(node.left);
        int[] right = dfs(node.right);

        int sum = node.val + left[0] + right[0];
        int count = 1 + left[1] + right[1];

        if (sum / count == node.val) {
            ans++;
        }

        return new int[]{sum, count};
    }
}
```

---

## Python

```python
class Solution:
    def averageOfSubtree(self, root: TreeNode) -> int:
        self.ans = 0

        def dfs(node):
            if not node:
                return (0, 0)

            left = dfs(node.left)
            right = dfs(node.right)

            total = node.val + left[0] + right[0]
            count = 1 + left[1] + right[1]

            if total // count == node.val:
                self.ans += 1

            return (total, count)

        dfs(root)
        return self.ans
```

---

## C++

```cpp
class Solution {
public:
    int ans = 0;

    int averageOfSubtree(TreeNode* root) {
        dfs(root);
        return ans;
    }

    pair<int,int> dfs(TreeNode* node) {
        if (!node) return {0, 0};

        auto left = dfs(node->left);
        auto right = dfs(node->right);

        int sum = node->val + left.first + right.first;
        int count = 1 + left.second + right.second;

        if (sum / count == node->val) ans++;

        return {sum, count};
    }
};
```

---

## C

```c
struct TreeNode {
    int val;
    struct TreeNode *left;
    struct TreeNode *right;
};

int ans;

int* dfs(struct TreeNode* node) {
    static int result[2];
    if (!node) {
        result[0] = 0; result[1] = 0;
        return result;
    }

    int* left = dfs(node->left);
    int* right = dfs(node->right);

    int sum = node->val + left[0] + right[0];
    int count = 1 + left[1] + right[1];

    if (sum / count == node->val) ans++;

    static int ret[2];
    ret[0] = sum; ret[1] = count;
    return ret;
}

int averageOfSubtree(struct TreeNode* root) {
    ans = 0;
    dfs(root);
    return ans;
}
```
