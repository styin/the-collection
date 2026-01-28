# Definition, Initialization
---
```C++
int arr[10];
int arr[10] = 0; // direct initialization
memset(arr, 0, sizeof(arr)); // memory initialization

arr[0] = 1;
int a = arr[0];
```
# Characteristics
1. Requires specified type, length
2. Reserves a continuous space of memory, sized `n * sizeof(type)`
3. Returns a pointer to the memory space's starting address
4. $O(1)$ for indexing and modifying, (appending and popping)
5. $O(n)$ for inserting, deleting from middle
### Notes
- Static arrays are usually only found in low-level compiler languages, like C/C++, Java, and also Goland
- Python, JavaScript does **not** have static arrays
##### Details for C/C++
- Different from Java and Golang, when a static array is defined without initialization, i.e. `int arr[10];`, the memory space is not zero-initialized and may be polluted by anything that was previously stored there

# Adding to a static array
### Inserting $O(n)$
```C++
int arr[10];
for (int i = 0; i < 4; i++) {
	arr[i] = 1;
}

for (int i = 4; i > 2; i--) { // Rev. traversal to prevent override 
	arr[i] = arr[i - 1]
}

arr[2] = 0;
```
### Array is full! Define a new one... $O(n)$
```cpp
int arr[10] = 1;

int new_arr[20];
for (int i = 0; i < 10; i++) {
	new_arr[i] = arr[i];
}

new_arr[10] = 11;
```
# Deleting from a static array
### Deleting an element from the middle $O(n)$
```cpp
int arr[10] = 1;

for (int i = 1; i < 4; i++) {
	arr[i] = arr[i + i];
}

arr[4] = -1; // to signal "deleted"
```

 