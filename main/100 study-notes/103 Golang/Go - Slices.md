---
created: 2022-05-22 17:51
updated: 2022-05-22 17:53
---
---
**Links**: [[103 Golang Index]]

---
## Slices
- **Dynamic length**
- *Similarities* between array and slice
	- Both a slice and an array can contain only the *same type of elements*
	- We can create a keyed slice like a keyed array
- *Differences* between array and slice
	- The *length of an array is part of its type*, *defined at compile time* and cannot be changed. The *length of a slice is not part of its type* and it *belongs to runtime*.
	- By **default an uninitialised array** has all elements equal to **zero**. An **uninitialised slice** is equal to **nil** (its zero value is nil). 
```go
array1 := [3]string{}
var array2 [3]string
fmt.Printf("%#v\n", array1) // [3]string{"", "", ""}
fmt.Printf("%#v\n", array2) // [3]string{"", "", ""}

slice1 := []string{}
var slice2 []string
fmt.Printf("%#v\n", slice1) // []string{}
fmt.Printf("%#v\n", slice2) // []string(nil)
```
- `nil` doesn't mean the absence of a value but the value hasn't been initialised yet. 
	- A `nil` slice is an empty slice with 0 capacity.
	- This is why we can call the `len` function on an uninitialised slice.
	- We cannot assign elements to a `nil` slice
```go
var values []string
fmt.Printf("%#v\n", values) // []string(nil)
fmt.Println(len(values)) // 0
values[0] = "test" // runtime error; index out of range
// we could do the above operation with arrays since size was fixed and it was initialised automatically with default values
```
- **Creating a slice**:
	- *Uninitialised slice equal to nil* - `var values []int; fmt.Println(value == nil)` - true.  
	- *Initialised slice not equal to nil* - `values := []int{}; fmt.Println(value == nil)` - false.
	- `values := []int{1,2,3}`
	- Using `make` : `make(type, len, capacity)`
		- `values := make([]int, 2)` - same as `[]int{0, 0}`
	- Another way : `type names []string; friends := names{"Dan", "Maria"}`
- *Slices cannot be compared* with the `=` operator, they *can only be compared to nil*. 
	- To compare 2 slices we use a for loop to iterate over the slices and compare element by element.

### Appending values to a slice
- We add values to a slice using `append`.
- This **returns a new slice** with the value appended to it. It **doesn't modify the existing slice**.
- The new slice can be saved back in the same variable.
```go
values1 := []int{1, 2, 3}
fmt.Printf("%p\n", &values1) // 0xc0000ac018

// values1 = append(values1, 45)
values2 := append(values1, 45) 
fmt.Printf("%p\n", &values2) // 0xc0000ac030
fmt.Println(values1, values2) // [1 2 3] [1 2 3 45]
```
> [!caution] In the above example we can't use simple `=` since `values2` hasn't been declared. If you were assigning the `values1` to `append` then using `=` would have been okay

- `append` is a variadic function and *can append more than one value*.
	- `values = append(values, 20,30,40)`
- Another use case of `append` is when we want to append one slice to another slice
```go
values1 := []int{1,2,3}
values2 := []int{4,5,6}
values1 = append(values1, values2...)
```

### Copying Slices
- Copying one slice to another using `copy(dstSlice, srcSlice)`
- It copies the src slice to destination and *returns the number of elements copied*
- When source and destination are of the same length
```go
values1 := []int{1, 2, 3}
values2 := make([]int, len(values1))
nn := copy(values2, values1)
fmt.Println(nn, values1, values2)
// 3 [1 2 3] [1 2 3]
```
- When source and destination are of different length
```go
values1 := []int{1, 2, 3}
values2 := make([]int, 2)
nn := copy(values2, values1)
fmt.Println(nn, values1, values2)
// 2 [1 2 3] [1 2]

values1 := []int{1, 2, 3}
values2 := []int{}
nn := copy(values2, values1)
fmt.Println(nn, values1, values2)
// 0 [1 2 3] []
```
- We don't copy slices using `=` since they will point to the same memory location.

### Slicing
- It doesn't modify the original slice/array but instead **returns a new one**.
- It *works for both arrays and slices*.
- Same rules as that of Python slicing. 
	- Missing start index defaults to 0. 
	- Missing end index defaults to maximum length.
	- Element at the start index is included and element at the end index is not included.
```go
values := []int{1,2,3,4,5}
sliced := values[1:3] // [2,3]
```
- **Slicing can be used for copying slices**
```go
values1 := []int{1,2,3,4,5}
values2 := values1[:]
```
- Some slice examples
```go
s1 := []int{1, 2, 3, 4, 5, 6}

s1 = append(s1[:4], 100) // adds 100 after index 4 (excluded)
fmt.Println(s1)          // -> [1 2 3 4 100]

s1 = append(s1[:4], 200) // overwrites the last element
fmt.Println(s1)          // -> [1 2 3 4 200]
```

### Slice Working (again)
- When creating a slice, behind the scenes Go creates a hidden array called **Backing Array**.

> [!important] Slice occupies less memory than slice

> [!note]- The **backing array stores the elements, not the slice**.

- Go implements a slice as a data structure called **slice header**.
- Slice Header contains 3 fields:
	- The *address* of the backing array (pointer). Address of the first element in the backing array since elements of the array are contiguous.
	- The *length* of the slice. `len()` returns it.
	- The *capacity* of the slice. `cap()` returns it.
- *Slice Header is the runtime representation of a slice*.
- A nil slice doesn't a have backing array. Its `len` & `cap` is 0.
- A slice expression (*slicing*) *doesn't create a new backing array*, the slice returned after the operation *refers to the backing array of the original slice*. 
	- **Slicing creates a new slice header but with the same backing array**.
	- Addresses can be different
	- When a slice is created by slicing an array, that array becomes the backing array of the new slice.
```go
values := []int{1, 2, 3, 4, 5}
v2, v3 := values[0:2], values[1:3]
values[1] = 400
fmt.Println(values, v2, v3) // [1 400 3 4 5] [1 400] [400 3]
```
> [!caution]- Hence we *cannot create a new slice using slicing*. The original and the new slice are connected. In short **don't create new slices using slicing**.
> To create a new slice from the original slice we use the `append` function

```go
values := []int{1, 2, 3, 4, 5}
v2 := []int{}
v2 = append(v2, values[1:3]...)
values[2] = 400
fmt.Println(values, v2)
```
- We can verify that slicing uses the same backing array by using the `cap` function
```go
values := []int{1, 2, 3, 4, 5}
v2 := values[1:3]
fmt.Println(len(v2), cap(v2)) // 3, 5
```
- Another example: 
	- As you can see once the capacity is met, `append` will return a new slice with a larger capacity. On the 4th iteration you will notice a larger capacity and a new pointer address.
```go
s := make([]int, 0, 3)
for i := 0; i < 5; i++ {
    s = append(s, i)
    fmt.Printf("cap %v, len %v, %p\n", cap(s), len(s), s)
}
// cap 3, len 1, 0x1040e130
// cap 3, len 2, 0x1040e130
// cap 3, len 3, 0x1040e130
// cap 6, len 4, 0x10432220
// cap 6, len 5, 0x10432220
```