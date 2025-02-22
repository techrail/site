---
draft: true
title: Go slices can act weird
tags:
  - vaibhav
  - golang
date: 2024-05-03
updated: 2024-05-03
---
Check the output of this program:

```go
package main

import "fmt"

func modifySlice(s []int) {
	// Modifying the elements of the slice
	for i := range s {
		s[i] *= 2
	}
	fmt.Println(s)
}

func main() {
	// Creating a slice
	nums := []int{1, 2, 3, 4, 5}

	// Passing the slice to the function
	modifySlice(nums)

	// The original slice has been modified
	fmt.Println(nums) // Output: [2 4 6 8 10]
}
```

and compare it to this one:

```go
package main

import "fmt"

func modifySlice(s []int) {
	// Modifying the elements of the slice
	for i := range s {
		s[i] *= 2
	}
	for i := 0; i < 10; i++ {
		s = append(s, i)
	}
	fmt.Println(s)
}

func main() {
	// Creating a slice
	nums := []int{1, 2, 3, 4, 5}

	// Passing the slice to the function
	modifySlice(nums)

	// The original slice has been modified
	fmt.Println(nums) // Output: [2 4 6 8 10]
}
```

To Prove the point:

```go
package main

import "fmt"

func modifySlice(s []int) {
	// Modifying the elements of the slice
	fmt.Println("A", len(s), cap(s))
	fmt.Printf("A* %p\n", s)
	for i := range s {
		s[i] *= 2
	}
	fmt.Println("B", len(s), cap(s))
	fmt.Printf("B* %p\n", s)
	for i := 0; i < 20; i++ {
		s = append(s, i)
	}
	fmt.Println("C", len(s), cap(s))
	fmt.Printf("C* %p\n", s)
	for i := range s {
		s[i] *= 2
	}
	fmt.Println("E", len(s), cap(s))
	fmt.Printf("E* %p\n", s)
	fmt.Println(s)
}

func main() {
	// var nms *[]int
	// Creating a slice
	nums := []int{1, 2, 3, 4, 5}
	//	nms = &nums

	// Passing the slice to the function
	modifySlice(nums)

	// The original slice has been modified
	fmt.Println("-->>>", nums) // Output: [2 4 6 8 10]
	fmt.Println("D", len(nums), cap(nums))
	fmt.Printf("D* %p\n", nums)
}
```