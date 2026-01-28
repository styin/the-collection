# Definition, Initialization
---
```cpp
vector<int> arr;
for (int i = 0; i < 10; i++) {
	arr.push_back(i); // Appending from the end: O(1)
}

arr.insert(arr.begin() + 2, 123); // Inserting at index 2: O(n)
arr.insert(arr.begin(), -1); // Inserting from the beginning: O(n)
arr.pop_back(); // Removing from the end: O(1)
arr.erase(arr.begin() + 2); // Removing from the middle: O(n)

int a = arr[0]; // Indexing at an index: O(1)
arr[0] = 100; // Modifying at an index: O(1)

// Finding element with value: O(n)
int index = find(arr.begin(), arr.end(), 123) - arr.begin()); 
```