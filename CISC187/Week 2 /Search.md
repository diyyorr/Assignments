
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
#include <iostream>
using namespace std;
// linear search using information from what array, number of elements, and the number we need to reach
int linSearch(int arr[], int size, int target, int &steps) {
    steps = 0; // we start counting from 0
    // linear search goes through every element in the element
    for (int i = 0; i < size; i++) {
        steps++; // counts how many steps we are taking

        // if we reach target, we return i which has been our index/counter for which element we are on
        if (arr[i] == target) {
            return i;
        }
  }
return 0;
}

// still using same parameters but this time for binary search
int binSearch(int arr[], int size, int target, int &steps) {
    steps = 0; // start at o 
    int left = 0; // left is the first index
    int right = size - 1; // last index is 99999
    
    while (left <= right) {
        steps++; // count steps
        int mid = (left + right) / 2; // find the middle index
       // if target is found, return the index


        if (arr[mid] == target) {
            return mid;
        }

        // if the target is less than the middle index, then we move the boundary to the left of mid
        if (arr[mid] > target) {
            right = mid - 1;

        // if the target is greater than the middle index, then we move the boundary to the right of mid
        } else {
            left = mid + 1;
        }
  }
return 0;
}

int main() {
    const int SIZE = 100000; // array size constant
    int arr[SIZE]; // create array to hold 100,000 elements
    int steps; // where steps are tracked
    
    // Fill array with 1- 99999
    for (int i = 0; i < SIZE; i++) {
        arr[i] = i;
    }
    
    // Search for 67000
    int target = 67000;

// run our linear searhc operation and record how many steps
    linSearch(arr, SIZE, target, steps);
    cout << "Linear Search steps: " << steps << endl;

// run our binary searhc operation and record how many steps
    binSearch(arr, SIZE, target, steps);
    cout << "Binary Search steps: " << steps << endl;
    
    return 0;
}
```
Linear search checks each element in the array starting from the beginning and moves forward one by one. In this case, the linear search took 67,001 steps to find the value 67000 because it had to go through every number from 0 up to 67000. This shows that as N gets bigger, the number of steps also gets bigger at the same rate. If the array doubled in size, the number of steps would also roughly double. That is why linear search is O(N), because the amount of work depends directly on how big N is. Binary search works differently. It does not check every element. After each step, it cuts the remaining part of the array in half. So instead of going one by one, it keeps dividing the search space by 2 until it finds the number. In this case, it only took 16 steps to find the value in an array of 100,000 elements. Even if the array gets much bigger, the number of steps only increases a little. That is why binary search is O(log N), because it keeps dividing N in half instead of checking each element one at a time.

##

### TASK 5: Write pseudocode for a randomized search algorithm that searches for a given key by randomly selecting indices without repetition. Use a dataset of 100,000 distinct elements, stored in a vector. Each element may be examined at most once during the search. Analyze and state the best-case, average-case, and worst-case time complexities of this algorithm using Big-O notation. Then, implement the algorithm in C++, using only the following standard headers: <vector> for data storage, <random> for random index generation, and <iostream> for input and output. The implementation should track and report the number of comparisons performed during the search. Finally, compare and contrast the randomized search algorithm with linear search and binary search in terms of time complexity, data requirements (such as ordering), and practical efficiency. Discuss scenarios in which each approach may be preferred, highlighting the advantages and limitations of randomized search relative to linear and binary search.

```
#include <iostream>
#include <vector>
#include <random>
using namespace std;

// linear search using information from what array, number of elements, and the number we need to reach
int linSearch(int arr[], int size, int target, int &steps) {

    steps = 0; // we start counting from 0

    // linear search goes through every element in the element
    for (int i = 0; i < size; i++) {
        steps++; // counts how many steps we are taking

        // if we reach target, we return i which has been our index/counter for which element we are on
        if (arr[i] == target) {
            return i;
        }
  }
return 0;
}

// still using same parameters but this time for binary search
int binSearch(int arr[], int size, int target, int &steps) {

    steps = 0; // starts at 0
    int left = 0; // left is the first index
    int right = size - 1; // last index is 99999
    
    while (left <= right) {
        steps++; // count steps
        int mid = (left + right) / 2; // find the middle index

       // if target is found, return the index
        if (arr[mid] == target) {
            return mid;
        }

        // if the target is less than the middle index, then we move the boundary to the left of mid
        if (arr[mid] > target) {
            right = mid - 1;

        // if the target is greater than the middle index, then we move the boundary to the right of mid
        } else {
            left = mid + 1;
        }
  }
return 0;
}

// randomized search picks random indices without checking same spot twice
int randomSearch(int arr[], int size, int target, int &steps) {
    steps = 0; // starts at 0
    
    // make an array to remember spots we checked
    vector<bool> checked(size);
    for (int i = 0; i < size; i++) {
        checked[i] = false;
  }
    
    // create a random number gen so we have close to random checking each time
    random_device rd;
    mt19937 gen(rd()); // create a random number
    uniform_int_distribution<> distribution(0, size - 1); // make sure its not bigger than the max size in our array
    
    int count = 0; // how many we checked so far
    
    // keep going until we check everything
    while (count < size) {
        int randIndex = distribution(gen); // pick random spot
        
        // if we checked this already keep picking new spots
        while (checked[randIndex] == true) {
            randIndex = distribution(gen);
        }
        
        checked[randIndex] = true; // mark as checked
        count = count + 1; // add to count
        steps++; // add step
        
        //if found send current index number back
        if (arr[randIndex] == target) {
            return randIndex;
        }
  }
    
    return 0;
}

int main() {
    const int SIZE = 100000; // array size constant
    int arr[SIZE]; // create array to hold 100,000 elements
    int steps; // where steps are tracked
    
    // Fill array with 1- 99999
    for (int i = 0; i < SIZE; i++) {
        arr[i] = i;
    }
    
    // Search for 67000
    int target = 67000;

// run our randomized search operation and record how many steps
    randomSearch(arr, SIZE, target, steps);
    cout << "Randomized Search steps: " << steps << endl;

// run our linear search operation and record how many steps
    linSearch(arr, SIZE, target, steps);
    cout << "Linear Search steps: " << steps << endl;

// run our binary search operation and record how many steps
    binSearch(arr, SIZE, target, steps);
    cout << "Binary Search steps: " << steps << endl;
    
    return 0;
}
```
<img width="332" height="72" alt="image" src="https://github.com/user-attachments/assets/92c168ff-d919-4ceb-a739-cf3cfb595900" />



I believe binary search is the most efficient when the data is sorted because it is the fastest at O(log N). It cuts the array in half each step, so it needs far fewer comparisons than the others. Randomized search would be second since it may sometimes find the value quickly, but its average and worst case are still O(N), the same as linear search. Linear search is third because it checks elements one by one and can take up to N steps. For unsorted data, binary search cannot be used unless we sort first, so linear and randomized are more practical. The big difference in time complexity really shows when the data is already sorted.

