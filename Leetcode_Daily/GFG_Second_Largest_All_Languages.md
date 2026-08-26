# GeeksforGeeks - Second Largest Element

Problem: https://www.geeksforgeeks.org/problems/second-largest3735/1

Find the second largest element in an array in O(n) time and O(1) extra space.

---

## Java

class Solution {
    public int getSecondLargest(int[] arr) {
        // Step 1: Find the largest element
        int largest = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > largest) {
                largest = arr[i];
            }
        }
        // Step 2: Find the second largest element
        int secondLargest = -1;
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] < largest && arr[i] > secondLargest) {
                secondLargest = arr[i];
            }
        }
        return secondLargest;
    }
}

---

## Python

class Solution:
    def getSecondLargest(self, arr):
        largest = arr[0]
        for i in range(1, len(arr)):
            if arr[i] > largest:
                largest = arr[i]
        secondLargest = -1
        for i in range(len(arr)):
            if arr[i] < largest and arr[i] > secondLargest:
                secondLargest = arr[i]
        return secondLargest

---

## C++

class Solution {
public:
    int getSecondLargest(vector<int>& arr) {
        int largest = arr[0];
        for (int i = 1; i < (int)arr.size(); i++) {
            if (arr[i] > largest) largest = arr[i];
        }
        int secondLargest = -1;
        for (int i = 0; i < (int)arr.size(); i++) {
            if (arr[i] < largest && arr[i] > secondLargest)
                secondLargest = arr[i];
        }
        return secondLargest;
    }
};

---

## C

int getSecondLargest(int arr[], int n) {
    int largest = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > largest) largest = arr[i];
    }
    int secondLargest = -1;
    for (int i = 0; i < n; i++) {
        if (arr[i] < largest && arr[i] > secondLargest)
            secondLargest = arr[i];
    }
    return secondLargest;
}
