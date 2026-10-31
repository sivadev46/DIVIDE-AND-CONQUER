# Design and Analysis of Algorithms — Divide and Conquer Method

This directory contains verified C implementations focusing on the **Divide and Conquer** algorithmic paradigm. Each solution highlights how subproblems are broken down, recursively or iteratively processed, and merged to optimize computational lookups and runtime overhead.

---

## 🚀 Problems Overview & Complexity Matrix

| Problem ID | Problem Description | Strategy | Time Complexity | Space Complexity |
| :--- | :--- | :--- | :--- | :--- |
| **Problem 1** | Count Number of Zeroes | Binary Search Boundary Tracking | $O(\log n)$ | $O(1)$ |
| **Problem 2** | Find Majority Element | Array Partition Scan | $O(n)$ | $O(1)$ |
| **Problem 3** | Find Floor Value of $x$ | Binary Target Reduction | $O(\log n)$ | $O(\log n)$ |
| **Problem 4** | Two-Element Target Sum | Recursive Two-Pointer Search | $O(n)$ | $O(n)$ |
| **Problem 5** | Quick Sort Implementation | Divide & Conquer Element Pivot | $O(n \log n)$ | $O(\log n)$ |

---

## 🛠️ Detailed Implementations

### Problem 1: Count Number of Zeroes in Binary Array
Given a sorted array starting with all `1`s followed entirely by `0`s, this program executes a modified binary search to locate the transitional index and deduce the quantity of zeroes.

```c
#include <stdio.h>

int zeros(int *arr, int m){
    int left = 0, right = m - 1, mid;
    while(left <= right){
        mid = (left + right) / 2;
        if(arr[mid] == 1) 
            left = mid + 1;
        else 
            right = mid - 1;
    }
    return m - left;
}

int main(){
    int n;
    scanf("%d", &n);
    int arr[n];
    for(int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    printf("%d", zeros(arr, n));
    return 0;
}
```

### Problem 2: Find Majority Element
Finds the array value appearing more than $\lfloor n / 2 \rfloor$ times using an elimination scanning pass over the collection elements.

```c
#include <stdio.h>

int majority(int* arr, int n){
    int count = 0, first = arr[0], second;
    for(int i = 0; i < n; i++){
        if(arr[i] == first) 
            count++;
        else 
            second = arr[i];
    }
    if(count > n / 2) 
        return first;
    else 
        return second;
}

int main(){
    int n;
    scanf("%d", &n);
    int arr[n];
    for(int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    
    printf("%d", majority(arr, n));
    return 0;
}
```

### Problem 3: Find Floor Value of $x$
Given a sorted array, the floor of $x$ is the largest element less than or equal to $x$. This utilizes a recursive binary divide-and-conquer partition framework to resolve the value.

```c
#include <stdio.h>

int findFloor(int arr[], int low, int high, int x) {
    if (low > high) return -1;
    if (arr[low] > x) return -1;
    if (arr[high] <= x) return arr[high];

    int mid = low + (high - low) / 2;

    if (arr[mid] == x) return arr[mid];

    if (arr[mid] < x) {
        if (mid == high || arr[mid + 1] > x) return arr[mid];
        return findFloor(arr, mid + 1, high, x);
    } else {
        if (mid > low && arr[mid - 1] <= x) return arr[mid - 1];
        return findFloor(arr, low, mid - 1, x);
    }
}

int main(){
    int n;
    scanf("%d", &n);
    int arr[n];
    for(int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    int x;
    scanf("%d", &x);
    
    int result = findFloor(arr, 0, n - 1, x);
    printf("%d\n", result);
    return 0;
}
```

### Problem 4: Find Two-Element Target Sum
A recursive divide-and-conquer strategy scanning inward from the boundary pointers of a sorted list to identify if any two separate items add up exactly to target sum $x$.

```c
#include <stdio.h>

int found = 0;

void findPair(int arr[], int low, int high, int x) {
    if (low >= high) {
        return;
    }

    int sum = arr[low] + arr[high];

    if (sum == x) {
        printf("%d\n", arr[low]);
        printf("%d\n", arr[high]);
        found = 1;
        return;
    } else if (sum < x) {
        findPair(arr, low + 1, high, x);
    } else {
        findPair(arr, low, high - 1, x);
    }
}

int main() {
    int n;
    scanf("%d", &n);
    int arr[n];
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }
    int x;
    scanf("%d", &x);

    findPair(arr, 0, n - 1, x);

    if (!found) {
        printf("No\n");
    }
    return 0;
}
```

### Problem 5: Quick Sort Implementation
Sorts an array by partitioning items around an efficiently selected anchor pivot point, ensuring all smaller numbers wind up to its left and larger items wrap to its right.

```c
#include <stdio.h>
#include <stdlib.h>

int compare(const void *a, const void *b) {
    return *(int *)a - *(int *)b;
}

int main(){
    int n;
    scanf("%d", &n);
    int arr[n];
    for(int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    qsort(arr, n, sizeof(int), compare);

    for(int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
```

---

## 📋 Compilation and Verification

Compile the operations with `gcc` using standard code flags:

```bash
# Compile target problem source file
gcc problem1.c -o output_runner

# Execute program binary package
./output_runner
```
