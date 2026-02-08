### TASK 1: Explain how to create an array of 100 elements.
```
int numbers [100];
```
I declare the type of data as well as the name of the array that we can reference. From there, I specifcy the number of elements which the assignment asked for 100.

##

### TASK 2: What will be the size of each element of an array.
```
int numbers [100];
cout << sizeof(numbers[0]);
```
We can use the sizeof operator to get the size of the first element which in this case is 4 bytes since we are using int.

##

### TASK 3: For an array containing 100 elements, provide the number of steps the following operations would take.

Reading : This operation allows us to look at specific elements directly so only 1 step is necessary

Searching for a value not contained within the array : Since the value is not contained within the array, the search operators goes through all 100 elements before confirming it is missing. So it would take 100 steps.

Insertion at the beginning of the array : Since we are inserting from the beginning, we shift all 100 elements to make space for our insertion then insert which totals to 101 steps

Insertion at the end of the array : Placing the value at the end of the array does not shift the existing elemts so only one step

Deletion at the beginning of the array : Deletes first element then shift other 99 to the left so 100 steps

Deletion at the end of the array : Only removes the last element so that takes 1 step

##

### TASK 4: Normally the search operation in an array looks for the first instance of a given value. But sometimes we may want to look for every instance of a given value. For example, say we want to count how many times the value “apple” is found inside an array. How many steps would it take to find all the “apples”?

To check for all possible apple values, the search would have to start from the beginning and go all the way to the end to ensure all possible matches are covered. So in total, it would be N steps (N being total amount of elements).

##

### TASK 5: Research how to find the memory address of an array.
```
int numbers[100];
cout << &numbers[0];
```
When researching for C++ (similarily for other langauges as well), I found  that the memory address is the location where the array is stored in memory, either a specific point in an array or the beginning of it. With C++ specifically, you can create an array then use the & operator to find the specific address (where is it stored in memory). When running the code above, I get the memory address which is also the starting address.










