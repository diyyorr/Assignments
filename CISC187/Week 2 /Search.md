
### TASK 1: How many steps would it take to perform a linear search for the number 8 in the ordered array, [2, 4, 6, 8, 10, 12, 13]?

The linear search would require 4 steps. First 2, then 4, then 6, then 8 (MATCH). Linear search stops there after finding match.

##

### TASK 2: How many steps would binary search take for the previous example?

Only 1 step would be necessary. Since binary searches start from the middle, it would begin at 8 which is currently in the middle of the element.
##

### TASK 3: What is the maximum number of steps it would take to perform a binary search on an array of size 100,000?

Log2(N) -> Log2(100,000) = 16.6 so the max number of steps required for binary searches on an array of 100,000 would be 17.

##

### TASK 4: Write a C++ program that implements both linear search and binary search algorithms using an array of 100,000 elements. The program should record and report the number of steps (comparisons) performed during each search operation. In addition, analyze and justify the observed behavior by providing a theoretical explanation using Big-O notation, demonstrating why linear search exhibits O(N) complexity and binary search exhibits O(logN) complexity.

```
int numbers[100];
cout << &numbers[0];
```

##

### TASK 5: Write pseudocode for a randomized search algorithm that searches for a given key by randomly selecting indices without repetition. Use a dataset of 100,000 distinct elements, stored in a vector. Each element may be examined at most once during the search. Analyze and state the best-case, average-case, and worst-case time complexities of this algorithm using Big-O notation. Then, implement the algorithm in C++, using only the following standard headers: <vector> for data storage, <random> for random index generation, and <iostream> for input and output. The implementation should track and report the number of comparisons performed during the search. Finally, compare and contrast the randomized search algorithm with linear search and binary search in terms of time complexity, data requirements (such as ordering), and practical efficiency. Discuss scenarios in which each approach may be preferred, highlighting the advantages and limitations of randomized search relative to linear and binary search.

```
int numbers[100];
cout << &numbers[0];
```
When researching for C++ (similarily for other langauges as well), I found  that the memory address is the location where the array is stored in memory, either a specific point in an array or the beginning of it. With C++ specifically, you can create an array then use the & operator to find the specific address (where is it stored in memory). When running the code above, I get the memory address which is also the starting address.
