# Slice

Package slice implements some functions to manipulate slice.

<div STYLE="page-break-after: always;"></div>

## Source:

-   [https://github.com/duke-git/lancet/blob/main/slice/slice.go](https://github.com/duke-git/lancet/blob/main/slice/slice.go)

<div STYLE="page-break-after: always;"></div>

## Usage:

```go
import (
    "github.com/duke-git/lancet/v2/slice"
)
```

<div STYLE="page-break-after: always;"></div>

## Index

-   [AppendIfAbsent](#AppendIfAbsent)
-   [Contain](#Contain)
-   [ContainBy](#ContainBy)
-   [ContainSubSlice](#ContainSubSlice)
-   [Chunk](#Chunk)
-   [Compact](#Compact)
-   [Concat](#Concat)
-   [Count](#Count)
-   [CountBy](#CountBy)
-   [Difference](#Difference)
-   [DifferenceBy](#DifferenceBy)
-   [DifferenceWith](#DifferenceWith)
-   [DeleteAt](#DeleteAt)
-   [Drop](#Drop)
-   [DropRight](#DropRight)
-   [DropWhile](#DropWhile)
-   [DropRightWhile](#DropRightWhile)
-   [Equal](#Equal)
-   [EqualWith](#EqualWith)
-   [Every](#Every)
-   [Filter](#Filter)
-   [Find<sup>deprecated</sup>](#Find)
-   [FindBy](#FindBy)
-   [FindLast<sup>deprecated</sup>](#FindLast)
-   [FindLastBy](#FindLastBy)
-   [Flatten](#Flatten)
-   [FlattenDeep](#FlattenDeep)
-   [ForEach](#ForEach)
-   [ForEachWithBreak](#ForEachWithBreak)
-   [GroupBy](#GroupBy)
-   [GroupWith](#GroupWith)
-   [IntSlice<sup>deprecated</sup>](#IntSlice)
-   [InterfaceSlice<sup>deprecated</sup>](#InterfaceSlice)
-   [Intersection](#Intersection)
-   [InsertAt](#InsertAt)
-   [IndexOf](#IndexOf)
-   [LastIndexOf](#LastIndexOf)
-   [Map](#Map)
-   [FilterMap](#FilterMap)
-   [FlatMap](#FlatMap)
-   [Merge](#Merge)
-   [Reverse](#Reverse)
-   [Reduce<sup>deprecated</sup>](#Reduce)
-   [ReduceBy](#ReduceBy)
-   [ReduceRight](#ReduceRight)
-   [Replace](#Replace)
-   [ReplaceAll](#ReplaceAll)
-   [Repeat](#Repeat)
-   [Shuffle](#Shuffle)
-   [IsAscending](#IsAscending)
-   [IsDescending](#IsDescending)
-   [IsSorted](#IsSorted)
-   [IsSortedByKey](#IsSortedByKey)
-   [Sort](#Sort)
-   [SortBy](#SortBy)
-   [SortByField](#SortByField)
-   [Some](#Some)
-   [StringSlice<sup>deprecated</sup>](#StringSlice)
-   [SymmetricDifference](#SymmetricDifference)
-   [ToSlice](#ToSlice)
-   [ToSlicePointer](#ToSlicePointer)
-   [Unique](#Unique)
-   [UniqueBy](#UniqueBy)
-   [Union](#Union)
-   [UnionBy](#UnionBy)
-   [UpdateAt](#UpdateAt)
-   [Without](#Without)
-   [KeyBy](#KeyBy)
-   [Join](#Join)
-   [Partition](#Partition)

<div STYLE="page-break-after: always;"></div>

## Documentation

### <span id="AppendIfAbsent">AppendIfAbsent</span>

<p>If slice doesn't contain the item, append it to the slice.</p>

<b>Signature:</b>

```go
func AppendIfAbsent[T comparable](slice []T, item T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/GNdv7Jg2Taj)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result1 := slice.AppendIfAbsent([]string{"a", "b"}, "b")
    result2 := slice.AppendIfAbsent([]string{"a", "b"}, "c")

    fmt.Println(result1)
    fmt.Println(result2)

    // Output:
    // [a b]
    // [a b c]
}
```

### <span id="Contain">Contain</span>

<p>Check if the target value is in the slice or not.</p>

<b>Signature:</b>

```go
func Contain[T comparable](slice []T, target T) bool
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/_454yEHcNjf)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result1 := slice.Contain([]string{"a", "b", "c"}, "a")
    result2 := slice.Contain([]int{1, 2, 3}, 4)

    fmt.Println(result1)
    fmt.Println(result2)

    // Output:
    // true
    // false
}
```

### <span id="ContainBy">ContainBy</span>

<p>returns true if predicate function return true.</p>

<b>Signature:</b>

```go
func ContainBy[T any](slice []T, predicate func(item T) bool) bool
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/49tkHfX4GNc)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    type foo struct {
        A string
        B int
    }

    array1 := []foo{{A: "1", B: 1}, {A: "2", B: 2}}
    result1 := slice.ContainBy(array1, func(f foo) bool { return f.A == "1" && f.B == 1 })
    result2 := slice.ContainBy(array1, func(f foo) bool { return f.A == "2" && f.B == 1 })

    array2 := []string{"a", "b", "c"}
    result3 := slice.ContainBy(array2, func(t string) bool { return t == "a" })
    result4 := slice.ContainBy(array2, func(t string) bool { return t == "d" })

    fmt.Println(result1)
    fmt.Println(result2)
    fmt.Println(result3)
    fmt.Println(result4)

    // Output:
    // true
    // false
    // true
    // false
}
```

### <span id="ContainSubSlice">ContainSubSlice</span>

<p>Check if the slice contain subslice or not.</p>

<b>Signature:</b>

```go
func ContainSubSlice[T comparable](slice, subSlice []T) bool
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/bcuQ3UT6Sev)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result1 := slice.ContainSubSlice([]string{"a", "b", "c"}, []string{"a", "b"})
    result2 := slice.ContainSubSlice([]string{"a", "b", "c"}, []string{"a", "d"})

    fmt.Println(result1)
    fmt.Println(result2)

    // Output:
    // true
    // false
}
```

### <span id="Chunk">Chunk</span>

<p>Creates an slice of elements split into groups the length of `size`.</p>

<b>Signature:</b>

```go
func Chunk[T any](slice []T, size int) [][]T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/b4Pou5j2L_C)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    arr := []string{"a", "b", "c", "d", "e"}

    result1 := slice.Chunk(arr, 1)
    result2 := slice.Chunk(arr, 2)
    result3 := slice.Chunk(arr, 3)
    result4 := slice.Chunk(arr, 4)
    result5 := slice.Chunk(arr, 5)

    fmt.Println(result1)
    fmt.Println(result2)
    fmt.Println(result3)
    fmt.Println(result4)
    fmt.Println(result5)

    // Output:
    // [[a] [b] [c] [d] [e]]
    // [[a b] [c d] [e]]
    // [[a b c] [d e]]
    // [[a b c d] [e]]
    // [[a b c d e]]
}
```

### <span id="Compact">Compact</span>

<p>Creates an slice with all falsey values removed. The values false, nil, 0, and "" are falsey.</p>

<b>Signature:</b>

```go
func Compact[T comparable](slice []T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/pO5AnxEr3TK)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result1 := slice.Compact([]int{0})
    result2 := slice.Compact([]int{0, 1, 2, 3})
    result3 := slice.Compact([]string{"", "a", "b", "0"})
    result4 := slice.Compact([]bool{false, true, true})

    fmt.Println(result1)
    fmt.Println(result2)
    fmt.Println(result3)
    fmt.Println(result4)

    // Output:
    // []
    // [1 2 3]
    // [a b 0]
    // [true true]
}
```

### <span id="Concat">Concat</span>

<p>Creates a new slice concatenating slice with any additional slices.</p>

<b>Signature:</b>

```go
func Concat[T any](slice []T, slices ...[]T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/gPt-q7zr5mk)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result1 := slice.Concat([]int{1, 2}, []int{3, 4})
    result2 := slice.Concat([]string{"a", "b"}, []string{"c"}, []string{"d"})

    fmt.Println(result1)
    fmt.Println(result2)

    // Output:
    // [1 2 3 4]
    // [a b c d]
}
```

### <span id="Count">Count</span>

<p>Returns the number of occurrences of the given item in the slice.</p>

<b>Signature:</b>

```go
func Count[T comparable](slice []T, item T) int
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/Mj4oiEnQvRJ)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3, 3, 4}

    result1 := slice.Count(nums, 1)
    result2 := slice.Count(nums, 3)

    fmt.Println(result1)
    fmt.Println(result2)

    // Output:
    // 1
    // 2
}
```

### <span id="CountBy">CountBy</span>

<p>Iterates over elements of slice with predicate function, returns the number of all matched elements.</p>

<b>Signature:</b>

```go
func CountBy[T any](slice []T, predicate func(index int, item T) bool) int
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/tHOccTMDZCC)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3, 4, 5}

    isEven := func(i, num int) bool {
        return num%2 == 0
    }

    result := slice.CountBy(nums, isEven)

    fmt.Println(result)

    // Output:
    // 2
}
```

### <span id="Difference">Difference</span>

<p>Creates an slice of whose element not included in the other given slice.</p>

<b>Signature:</b>

```go
func Difference[T comparable](slice, comparedSlice []T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/VXvadzLzhDa)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    s1 := []int{1, 2, 3, 4, 5}
    s2 := []int{4, 5, 6}

    result := slice.Difference(s1, s2)

    fmt.Println(result)

    // Output:
    // [1 2 3]
}
```

### <span id="DifferenceBy">DifferenceBy</span>

<p>DifferenceBy accepts iteratee func which is invoked for each element of slice and values to generate the criterion by which they're compared.</p>

<b>Signature:</b>

```go
func DifferenceBy[T comparable](slice []T, comparedSlice []T, iteratee func(index int, item T) T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/DiivgwM5OnC)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    s1 := []int{1, 2, 3, 4, 5}
    s2 := []int{3, 4, 5}

    addOne := func(i int, v int) int {
        return v + 1
    }

    result := slice.DifferenceBy(s1, s2, addOne)

    fmt.Println(result)

    // Output:
    // [1 2]
}
```

### <span id="DifferenceWith">DifferenceWith</span>

<p>DifferenceWith accepts comparator which is invoked to compare elements of slice to values. The order and references of result values are determined by the first slice.</p>

<b>Signature:</b>

```go
func DifferenceWith[T any](slice []T, comparedSlice []T, comparator func(value, otherValue T) bool) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/v2U2deugKuV)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    s1 := []int{1, 2, 3, 4, 5}
    s2 := []int{4, 5, 6, 7, 8}

    isDouble := func(v1, v2 int) bool {
        return v2 == 2*v1
    }

    result := slice.DifferenceWith(s1, s2, isDouble)

    fmt.Println(result)

    // Output:
    // [1 5]
}
```

### <span id="DeleteAt">DeleteAt</span>

<p>Delete the element of slice from start index to end index - 1.</p>

<b>Signature:</b>

```go
func DeleteAt[T any](slice []T, start int, end ...int)
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/pJ-d6MUWcvK)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result1 := slice.DeleteAt([]string{"a", "b", "c"}, -1)
    result2 := slice.DeleteAt([]string{"a", "b", "c"}, 0)
    result3 := slice.DeleteAt([]string{"a", "b", "c"}, 0, 2)

    fmt.Println(result1)
    fmt.Println(result2)
    fmt.Println(result3)

    // Output:
    // [a b c]
    // [b c]
    // [c]
}
```

### <span id="Drop">Drop</span>

<p>Drop n elements from the start of a slice.</p>

<b>Signature:</b>

```go
func Drop[T any](slice []T, n int) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/jnPO2yQsT8H)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result1 := slice.Drop([]string{"a", "b", "c"}, 0)
    result2 := slice.Drop([]string{"a", "b", "c"}, 1)
    result3 := slice.Drop([]string{"a", "b", "c"}, -1)
    result4 := slice.Drop([]string{"a", "b", "c"}, 4)

    fmt.Println(result1)
    fmt.Println(result2)
    fmt.Println(result3)
    fmt.Println(result4)

    // Output:
    // [a b c]
    // [b c]
    // [a b c]
    // []
}
```

### <span id="DropRight">DropRight</span>

<p>Drop n elements from the end of a slice.</p>

<b>Signature:</b>

```go
func DropRight[T any](slice []T, n int) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/8bcXvywZezG)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result1 := slice.DropRight([]string{"a", "b", "c"}, 0)
    result2 := slice.DropRight([]string{"a", "b", "c"}, 1)
    result3 := slice.DropRight([]string{"a", "b", "c"}, -1)
    result4 := slice.DropRight([]string{"a", "b", "c"}, 4)

    fmt.Println(result1)
    fmt.Println(result2)
    fmt.Println(result3)
    fmt.Println(result4)

    // Output:
    // [a b c]
    // [a b]
    // [a b c]
    // []
}
```

### <span id="DropWhile">DropWhile</span>

<p>Drop n elements from the start of a slice while predicate function returns true.</p>

<b>Signature:</b>

```go
func DropWhile[T any](slice []T, predicate func(item T) bool) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/4rt252UV_qs)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result1 := slice.DropWhile(numbers, func(n int) bool {
        return n != 2
    })
    result2 := slice.DropWhile(numbers, func(n int) bool {
        return true
    })
    result3 := slice.DropWhile(numbers, func(n int) bool {
        return n == 0
    })

    fmt.Println(result1)
    fmt.Println(result2)
    fmt.Println(result3)

    // Output:
    // [2 3 4 5]
    // []
    // [1 2 3 4 5]
}
```

### <span id="DropRightWhile">DropRightWhile</span>

<p>Drop n elements from the end of a slice while predicate function returns true.</p>

<b>Signature:</b>

```go
func DropRightWhile[T any](slice []T, predicate func(item T) bool) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/6wyK3zMY56e)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    numbers := []int{1, 2, 3, 4, 5}

    result1 := slice.DropRightWhile(numbers, func(n int) bool {
        return n != 2
    })
    result2 := slice.DropRightWhile(numbers, func(n int) bool {
        return true
    })
    result3 := slice.DropRightWhile(numbers, func(n int) bool {
        return n == 0
    })

    fmt.Println(result1)
    fmt.Println(result2)
    fmt.Println(result3)

    // Output:
    // [1 2]
    // []
    // [1 2 3 4 5]
}
```

### <span id="Equal">Equal</span>

<p>Check if two slices are equal: the same length and all elements' order and value are equal.</p>

<b>Signature:</b>

```go
func Equal[T comparable](slice1, slice2 []T) bool
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/WcRQJ37ifPa)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    s1 := []int{1, 2, 3}
    s2 := []int{1, 2, 3}
    s3 := []int{1, 3, 2}

    result1 := slice.Equal(s1, s2)
    result2 := slice.Equal(s1, s3)

    fmt.Println(result1)
    fmt.Println(result2)

    // Output:
    // true
    // false
}
```

### <span id="EqualWith">EqualWith</span>

<p>Check if two slices are equal with comparator func.</p>

<b>Signature:</b>

```go
func EqualWith[T, U any](slice1 []T, slice2 []U, comparator func(T, U) bool) bool
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/b9iygtgsHI1)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    s1 := []int{1, 2, 3}
    s2 := []int{2, 4, 6}

    isDouble := func(a, b int) bool {
        return b == a*2
    }

    result := slice.EqualWith(s1, s2, isDouble)

    fmt.Println(result)

    // Output:
    // true
}
```

### <span id="Every">Every</span>

<p>Return true if all of the values in the slice pass the predicate function.</p>

<b>Signature:</b>

```go
func Every[T any](slice []T, predicate func(index int, item T) bool) bool
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/R8U6Sl-j8cD)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3, 5}

    isEven := func(i, num int) bool {
        return num%2 == 0
    }

    result := slice.Every(nums, isEven)

    fmt.Println(result)

    // Output:
    // false
}
```

### <span id="Filter">Filter</span>

<p>Return all elements which match the function.</p>

<b>Signature:</b>

```go
func Filter[T any](slice []T, predicate func(index int, item T) bool) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/SdPna-7qK4T)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3, 4, 5}

    isEven := func(i, num int) bool {
        return num%2 == 0
    }

    result := slice.Filter(nums, isEven)

    fmt.Println(result)

    // Output:
    // [2 4]
}
```

### <span id="Find">Find(deprecated: use FindBy)</span>

<p>Iterates over elements of slice, returning the first one that passes a truth test on function.</p>

<b>Signature:</b>

```go
func Find[T any](slice []T, predicate func(index int, item T) bool) (*T, bool)
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/CBKeBoHVLgq)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3, 4, 5}

    isEven := func(i, num int) bool {
        return num%2 == 0
    }

    result, ok := slice.Find(nums, isEven)

    fmt.Println(*result)
    fmt.Println(ok)

    // Output:
    // 2
    // true
}
```

### <span id="FindBy">FindBy</span>

<p>Iterates over elements of slice, returning the first one that passes a truth test on predicate function.If return T is nil or zero value then no items matched the predicate func. In contrast to Find or FindLast, its return value no longer requires dereferencing.</p>

<b>Signature:</b>

```go
func FindBy[T any](slice []T, predicate func(index int, item T) bool) (v T, ok bool)
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/n1lysBYl-GB)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3, 4, 5}

    isEven := func(i, num int) bool {
        return num%2 == 0
    }

    result, ok := slice.FindBy(nums, isEven)

    fmt.Println(result)
    fmt.Println(ok)

    // Output:
    // 2
    // true
}
```

### <span id="FindLast">FindLast(deprecated: use FindLastBy)</span>

<p>iterates over elements of slice from end to begin, returning the last one that passes a truth test on function.</p>

<b>Signature:</b>

```go
func FindLast[T any](slice []T, predicate func(index int, item T) bool) (*T, bool)
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/FFDPV_j7URd)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3, 4, 5}

    isEven := func(i, num int) bool {
        return num%2 == 0
    }

    result, ok := slice.FindLast(nums, isEven)

    fmt.Println(*result)
    fmt.Println(ok)

    // Output:
    // 4
    // true
}
```

### <span id="FindLastBy">FindLastBy</span>

<p>FindLastBy iterates over elements of slice, returning the last one that passes a truth test on predicate function. If return T is nil or zero value then no items matched the predicate func. In contrast to Find or FindLast, its return value no longer requires dereferencing.</p>

<b>Signature:</b>

```go
func FindLastBy[T any](slice []T, predicate func(index int, item T) bool) (v T, ok bool)
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/8iqomzyCl_s)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3, 4, 5}

    isEven := func(i, num int) bool {
        return num%2 == 0
    }

    result, ok := slice.FindLastBy(nums, isEven)

    fmt.Println(result)
    fmt.Println(ok)

    // Output:
    // 4
    // true
}
```

### <span id="Flatten">Flatten</span>

<p>Flatten slice with one level.</p>

<b>Signature:</b>

```go
func Flatten(slice any) any
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/hYa3cBEevtm)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    arrs := [][][]string{{{"a", "b"}}, {{"c", "d"}}}

    result := slice.Flatten(arrs)

    fmt.Println(result)

    // Output:
    // [[a b] [c d]]
}
```

### <span id="FlattenDeep">FlattenDeep</span>

<p>flattens slice recursive.</p>

<b>Signature:</b>

```go
func FlattenDeep(slice any) any
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/yjYNHPyCFaF)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    arrs := [][][]string{{{"a", "b"}}, {{"c", "d"}}}

    result := slice.FlattenDeep(arrs)

    fmt.Println(result)

    // Output:
    // [a b c d]
}
```

### <span id="ForEach">ForEach</span>

<p>Iterates over elements of slice and invokes function for each element.</p>

<b>Signature:</b>

```go
func ForEach[T any](slice []T, iteratee func(index int, item T))
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/DrPaa4YsHRF)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3}

    var result []int
    addOne := func(_ int, v int) {
        result = append(result, v+1)
    }

    slice.ForEach(nums, addOne)

    fmt.Println(result)

    // Output:
    // [2 3 4]
}
```

### <span id="ForEachWithBreak">ForEachWithBreak</span>

<p>Iterates over elements of slice and invokes function for each element, when iteratee return false, will break the for each loop.</p>

<b>Signature:</b>

```go
func ForEachWithBreak[T any](slice []T, iteratee func(index int, item T) bool)
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/qScs39f3D9W)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    numbers := []int{1, 2, 3, 4, 5}

    var sum int

    slice.ForEachWithBreak(numbers, func(_, n int) bool {
        if n > 3 {
            return false
        }
        sum += n
        return true
    })

    fmt.Println(sum)

    // Output:
    // 6
}
```

### <span id="GroupBy">GroupBy</span>

<p>Iterates over elements of the slice, each element will be group by criteria, returns two slices.</p>

<b>Signature:</b>

```go
func GroupBy[T any](slice []T, groupFn func(index int, item T) bool) ([]T, []T)
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/QVkPxzPR0iA)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3, 4, 5}

    isEven := func(i, num int) bool {
        return num%2 == 0
    }

    even, odd := slice.GroupBy(nums, isEven)

    fmt.Println(even)
    fmt.Println(odd)

    // Output:
    // [2 4]
    // [1 3 5]
}
```

### <span id="GroupWith">GroupWith</span>

<p>Return a map composed of keys generated from the results of running each element of slice thru iteratee.</p>

<b>Signature:</b>

```go
func GroupWith[T any, U comparable](slice []T, iteratee func(T) U) map[U][]T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/ApCvMNTLO8a)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []float64{6.1, 4.2, 6.3}

    floor := func(num float64) float64 {
        return math.Floor(num)
    }

    result := slice.GroupWith(nums, floor) //map[float64][]float64

    fmt.Println(result)

    // Output:
    // map[4:[4.2] 6:[6.1 6.3]]
}
```

### <span id="IntSlice">IntSlice (Deprecated: use generic feature of go1.18+ for replacement)</span>

<p>Convert interface slice to int slice.</p>

<b>Signature:</b>

```go
func IntSlice(slice any) []int
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/UQDj-on9TGN)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []interface{}{1, 2, 3}

    result := slice.IntSlice(nums) //[]int{1, 2, 3}
    fmt.Println(result)

    // Output:
    // [1 2 3]
}
```

### <span id="InterfaceSlice">InterfaceSlice (Deprecated: use generic feature of go1.18+ for replacement)</span>

<p>Convert value to interface slice.</p>

<b>Signature:</b>

```go
func InterfaceSlice(slice any) []any
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/FdQXF0Vvqs-)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    strs := []string{"a", "b", "c"}

    result := slice.InterfaceSlice(strs) //[]interface{}{"a", "b", "c"}
    fmt.Println(result)

    // Output:
    // [a b c]
}
```

### <span id="Intersection">Intersection</span>

<p>Creates a slice of unique values that included by all slices.</p>

<b>Signature:</b>

```go
func Intersection[T comparable](slices ...[]T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/anJXfB5wq_t)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums1 := []int{1, 2, 3}
    nums2 := []int{2, 3, 4}

    result := slice.Intersection(nums1, nums2)

    fmt.Println(result)

    // Output:
    // [2 3]
}
```

### <span id="InsertAt">InsertAt</span>

<p>insert the element into slice at index.</p>

<b>Signature:</b>

```go
func InsertAt[T any](slice []T, index int, value any) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/hMLNxPEGJVE)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result1 := slice.InsertAt([]string{"a", "b", "c"}, 0, "1")
    result2 := slice.InsertAt([]string{"a", "b", "c"}, 1, "1")
    result3 := slice.InsertAt([]string{"a", "b", "c"}, 2, "1")
    result4 := slice.InsertAt([]string{"a", "b", "c"}, 3, "1")
    result5 := slice.InsertAt([]string{"a", "b", "c"}, 0, []string{"1", "2", "3"})

    fmt.Println(result1)
    fmt.Println(result2)
    fmt.Println(result3)
    fmt.Println(result4)
    fmt.Println(result5)

    // Output:
    // [1 a b c]
    // [a 1 b c]
    // [a b 1 c]
    // [a b c 1]
    // [1 2 3 a b c]
}
```

### <span id="IndexOf">IndexOf</span>

<p>Returns the index at which the first occurrence of a item is found in a slice or return -1 if the item cannot be found.</p>

<b>Signature:</b>

```go
func IndexOf[T comparable](slice []T, item T) int
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/MRN1f0FpABb)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    strs := []string{"a", "a", "b", "c"}

    result1 := slice.IndexOf(strs, "a")
    result2 := slice.IndexOf(strs, "d")

    fmt.Println(result1)
    fmt.Println(result2)

    // Output:
    // 0
    // -1
}
```

### <span id="LastIndexOf">LastIndexOf</span>

<p>Returns the index at which the last occurrence of a item is found in a slice or return -1 if the item cannot be found.</p>

<b>Signature:</b>

```go
func LastIndexOf[T comparable](slice []T, item T) int
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/DokM4cf1IKH)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    strs := []string{"a", "a", "b", "c"}

    result1 := slice.LastIndexOf(strs, "a")
    result2 := slice.LastIndexOf(strs, "d")

    fmt.Println(result1)
    fmt.Println(result2)

    // Output:
    // 1
    // -1
}
```

### <span id="Map">Map</span>

<p>Creates an slice of values by running each element in slice thru function.</p>

<b>Signature:</b>

```go
func Map[T any, U any](slice []T, iteratee func(index int, item T) U) []U
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/biaTefqPquw)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3}

    addOne := func(_ int, v int) int {
        return v + 1
    }

    result := slice.Map(nums, addOne)

    fmt.Println(result)

    // Output:
    // [2 3 4]
}
```

### <span id="FilterMap">FilterMap</span>

<p>Returns a slice which apply both filtering and mapping to the given slice. iteratee callback function should returntwo values: 1, mapping result. 2, whether the result element should be included or not.</p>

<b>Signature:</b>

```go
func FilterMap[T any, U any](slice []T, iteratee func(index int, item T) (U, bool)) []U
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/J94SZ_9MiIe)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3, 4, 5}

    getEvenNumStr := func(i, num int) (string, bool) {
        if num%2 == 0 {
            return strconv.FormatInt(int64(num), 10), true
        }
        return "", false
    }

    result := slice.FilterMap(nums, getEvenNumStr)

    fmt.Printf("%#v", result)

    // Output:
    // []string{"2", "4"}
}
```

### <span id="FlatMap">FlatMap</span>

<p>Manipulates a slice and transforms and flattens it to a slice of another type.</p>

<b>Signature:</b>

```go
func FlatMap[T any, U any](slice []T, iteratee func(index int, item T) []U) []U
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/_QARWlWs1N_F)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3, 4}

    result := slice.FlatMap(nums, func(i int, num int) []string {
        s := "hi-" + strconv.FormatInt(int64(num), 10)
        return []string{s}
    })

    fmt.Printf("%#v", result)

    // Output:
    // []string{"hi-1", "hi-2", "hi-3", "hi-4"}
}
```

### <span id="Merge">Merge</span>

<p>Merge all given slices into one slice.</p>

<b>Signature:</b>

```go
func Merge[T any](slices ...[]T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/lbjFp784r9N)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums1 := []int{1, 2, 3}
    nums2 := []int{3, 4}

    result := slice.Merge(nums1, nums2)

    fmt.Println(result)

    // Output:
    // [1 2 3 3 4]
}
```

### <span id="Reverse">Reverse</span>

<p>Reverse the elements order in slice.</p>

<b>Signature:</b>

```go
func Reverse[T any](slice []T)
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/8uI8f1lwNrQ)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    strs := []string{"a", "b", "c", "d"}

    slice.Reverse(strs)

    fmt.Println(strs)

    // Output:
    // [d c b a]
}
```

### <span id="Reduce">Reduce</span>

<p>Reduce slice.(Deprecated: use ReduceBy)</p>

<b>Signature:</b>

```go
func Reduce[T any](slice []T, iteratee func(index int, item1, item2 T) T, initial T) T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/_RfXJJWIsIm)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3}

    sum := func(_ int, v1, v2 int) int {
        return v1 + v2
    }

    result := slice.Reduce(nums, sum, 0)

    fmt.Println(result)

    // Output:
    // 6
}
```

### <span id="ReduceBy">ReduceBy</span>

<p>Produces a value from slice by accumulating the result of each element as passed through the reducer function.</p>

<b>Signature:</b>

```go
func ReduceBy[T any, U any](slice []T, initial U, reducer func(index int, item T, agg U) U) U
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/YKDpLi7gtee)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result1 := slice.ReduceBy([]int{1, 2, 3, 4}, 0, func(_ int, item int, agg int) int {
        return agg + item
    })

    result2 := slice.ReduceBy([]int{1, 2, 3, 4}, "", func(_ int, item int, agg string) string {
        return agg + fmt.Sprintf("%v", item)
    })

    fmt.Println(result1)
    fmt.Println(result2)

    // Output:
    // 10
    // 1234
}
```

### <span id="ReduceRight">ReduceRight</span>

<p>ReduceRight is like ReduceBy, but it iterates over elements of slice from right to left.</p>

<b>Signature:</b>

```go
func ReduceRight[T any, U any](slice []T, initial U, reducer func(index int, item T, agg U) U) U
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/qT9dZC03A1K)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result := slice.ReduceRight([]int{1, 2, 3, 4}, "", func(_ int, item int, agg string) string {
        return agg + fmt.Sprintf("%v", item)
    })

    fmt.Println(result)

    // Output:
    // 4321
}
```

### <span id="Replace">Replace</span>

<p>Returns a copy of the slice with the first n non-overlapping instances of old replaced by new.</p>

<b>Signature:</b>

```go
func Replace[T comparable](slice []T, old T, new T, n int) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/P5mZp7IhOFo)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    strs := []string{"a", "b", "c", "a"}

    result1 := slice.Replace(strs, "a", "x", 0)
    result2 := slice.Replace(strs, "a", "x", 1)
    result3 := slice.Replace(strs, "a", "x", 2)
    result4 := slice.Replace(strs, "a", "x", 3)
    result5 := slice.Replace(strs, "a", "x", -1)

    fmt.Println(result1)
    fmt.Println(result2)
    fmt.Println(result3)
    fmt.Println(result4)
    fmt.Println(result5)

    // Output:
    // [a b c a]
    // [x b c a]
    // [x b c x]
    // [x b c x]
    // [x b c x]
}
```

### <span id="ReplaceAll">ReplaceAll</span>

<p>Returns a copy of the slice with the first n non-overlapping instances of old replaced by new.</p>

<b>Signature:</b>

```go
func ReplaceAll[T comparable](slice []T, old T, new T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/CzqXMsuYUrx)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result := slice.ReplaceAll([]string{"a", "b", "c", "a"}, "a", "x")

    fmt.Println(result)

    // Output:
    // [x b c x]
}
```

### <span id="Repeat">Repeat</span>

<p>Creates a slice with length n whose elements are passed param item.</p>

<b>Signature:</b>

```go
func Repeat[T any](item T, n int) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/1CbOmtgILUU)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result := slice.Repeat("a", 3)

    fmt.Println(result)

    // Output:
    // [a a a]
}
```

### <span id="Shuffle">Shuffle</span>

<p>Creates an slice of shuffled values.</p>

<b>Signature:</b>

```go
func Shuffle[T any](slice []T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/YHvhnWGU3Ge)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3, 4, 5}
    result := slice.Shuffle(nums)

    fmt.Println(res)

    // Output:
    // [3 1 5 4 2] (random order)
}
```

### <span id="IsAscending">IsAscending</span>

<p>Checks if a slice is ascending order.</p>

<b>Signature:</b>

```go
func IsAscending[T constraints.Ordered](slice []T) bool
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/9CtsFjet4SH)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result1 := slice.IsAscending([]int{1, 2, 3, 4, 5})
    result2 := slice.IsAscending([]int{5, 4, 3, 2, 1})
    result3 := slice.IsAscending([]int{2, 1, 3, 4, 5})

    fmt.Println(result1)
    fmt.Println(result2)
    fmt.Println(result3)

    // Output:
    // true
    // false
    // false
}
```

### <span id="IsDescending">IsDescending</span>

<p>Checks if a slice is descending order.</p>

<b>Signature:</b>

```go
func IsDescending[T constraints.Ordered](slice []T) bool
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/U_LljFXma14)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result1 := slice.IsDescending([]int{5, 4, 3, 2, 1})
    result2 := slice.IsDescending([]int{1, 2, 3, 4, 5})
    result3 := slice.IsDescending([]int{2, 1, 3, 4, 5})

    fmt.Println(result1)
    fmt.Println(result2)
    fmt.Println(result3)

    // Output:
    // true
    // false
    // false
}
```

### <span id="IsSorted">IsSorted</span>

<p>Checks if a slice is sorted (ascending or descending).</p>

<b>Signature:</b>

```go
func IsSorted[T constraints.Ordered](slice []T) bool
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/nCE8wPLwSA-)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result1 := slice.IsSorted([]int{5, 4, 3, 2, 1})
    result2 := slice.IsSorted([]int{1, 2, 3, 4, 5})
    result3 := slice.IsSorted([]int{2, 1, 3, 4, 5})

    fmt.Println(result1)
    fmt.Println(result2)
    fmt.Println(result3)

    // Output:
    // true
    // true
    // false
}
```

### <span id="IsSortedByKey">IsSortedByKey</span>

<p>Checks if a slice is sorted by iteratee function.</p>

<b>Signature:</b>

```go
func IsSortedByKey[T any, K constraints.Ordered](slice []T, iteratee func(item T) K) bool
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/tUoGB7DOHI4)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result1 := slice.IsSortedByKey([]string{"a", "ab", "abc"}, func(s string) int {
        return len(s)
    })
    result2 := slice.IsSortedByKey([]string{"abc", "ab", "a"}, func(s string) int {
        return len(s)
    })
    result3 := slice.IsSortedByKey([]string{"abc", "a", "ab"}, func(s string) int {
        return len(s)
    })

    fmt.Println(result1)
    fmt.Println(result2)
    fmt.Println(result3)

    // Output:
    // true
    // true
    // false
}
```

### <span id="Sort">Sort</span>

<p>Sorts a slice of any ordered type(number or string), use quick sort algrithm. Default sort order is ascending (asc), if want descending order, set param `sortOrder` to `desc`. Ordered type: number(all ints uints floats) or string.</p>

<b>Signature:</b>

```go
func Sort[T constraints.Ordered](slice []T, sortOrder ...string)
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/V9AVjzf_4Fk)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    numbers := []int{1, 4, 3, 2, 5}

    slice.Sort(numbers)
    fmt.Println(numbers) // [1 2 3 4 5]

    slice.Sort(numbers, "desc")
    fmt.Println(numbers) // [5 4 3 2 1]

    strings := []string{"a", "d", "c", "b", "e"}

    slice.Sort(strings)
    fmt.Println(strings) //[a b c d e}

    slice.Sort(strings, "desc")
    fmt.Println(strings) //[e d c b a]
}
```

### <span id="SortBy">SortBy</span>

<p>Sorts the slice in ascending order as determined by the less function. This sort is not guaranteed to be stable.</p>

<b>Signature:</b>

```go
func SortBy[T any](slice []T, less func(a, b T) bool)
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/DAhLQSZEumm)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    numbers := []int{1, 4, 3, 2, 5}

    slice.SortBy(numbers, func(a, b int) bool {
        return a < b
    })
    fmt.Println(numbers) // [1 2 3 4 5]

    type User struct {
        Name string
        Age  uint
    }

    users := []User{
        {Name: "a", Age: 21},
        {Name: "b", Age: 15},
        {Name: "c", Age: 100}}

    slice.SortBy(users, func(a, b User) bool {
        return a.Age < b.Age
    })

    fmt.Printf("sort users by age: %v", users)

    // output
    // [{b 15} {a 21} {c 100}]
}
```

### <span id="SortByField">SortByField</span>

<p>Sort struct slice by field. Slice element should be struct, `field` param type should be int, uint, string, or bool. Default sort type is ascending (asc), if descending order, set `sortType` param to desc.</p>

<b>Signature:</b>

```go
func SortByField(slice any, field string, sortType ...string) error
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/fU1prOBP9p1)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    type User struct {
        Name string
        Age  uint
    }

    users := []User{
        {Name: "a", Age: 21},
        {Name: "b", Age: 15},
        {Name: "c", Age: 100}}

    err := slice.SortByField(users, "Age", "desc")
    if err != nil {
        return
    }

    fmt.Println(users)

    // Output:
    // [{c 100} {a 21} {b 15}]
}
```

### <span id="Some">Some</span>

<p>Return true if any of the values in the list pass the predicate function.</p>

<b>Signature:</b>

```go
func Some[T any](slice []T, predicate func(index int, item T) bool) bool
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/4pO9Xf9NDGS)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3, 5}

    isEven := func(i, num int) bool {
        return num%2 == 0
    }

    result := slice.Some(nums, isEven)

    fmt.Println(result)

    // Output:
    // true
}
```

### <span id="StringSlice">StringSlice (Deprecated: use generic feature of go1.18+ for replacement)</span>

<p>Convert interface slice to string slice.</p>

<b>Signature:</b>

```go
func StringSlice(slice any) []string
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/W0TZDWCPFcI)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    strs := []interface{}{"a", "b", "c"}

    result := slice.StringSlice(strs) //[]string{"a", "b", "c"}
    fmt.Println(result)

    // Output:
    // [a b c]
}
```

### <span id="SymmetricDifference">SymmetricDifference</span>

<p>Create a slice whose element is in given slices, but not in both slices.</p>

<b>Signature:</b>

```go
func SymmetricDifference[T comparable](slices ...[]T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/1CbOmtgILUU)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums1 := []int{1, 2, 3}
    nums2 := []int{1, 2, 4}

    result := slice.SymmetricDifference(nums1, nums2)

    fmt.Println(result)

    // Output:
    // [3 4]
}
```

### <span id="ToSlice">ToSlice</span>

<p>Creates a slice of give items.</p>

<b>Signature:</b>

```go
func ToSlice[T any](items ...T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/YzbzVq5kscN)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result := slice.ToSlice("a", "b", "c")

    fmt.Println(result)

    // Output:
    // [a b c]
}
```

### <span id="ToSlicePointer">ToSlicePointer</span>

<p>Returns a pointer to the slices of a variable parameter transformation</p>

<b>Signature:</b>

```go
func ToSlicePointer[T any](items ...T) []*T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/gx4tr6_VXSF)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    str1 := "a"
    str2 := "b"

    result := slice.ToSlicePointer(str1, str2)

    expect := []*string{&str1, &str2}

    isEqual := reflect.DeepEqual(result, expect)

    fmt.Println(isEqual)

    // Output:
    // true
}
```

### <span id="Unique">Unique</span>

<p>Remove duplicate elements in slice.</p>

<b>Signature:</b>

```go
func Unique[T comparable](slice []T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/AXw0R3ZTE6a)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result := slice.Unique([]string{"a", "a", "b"})
    fmt.Println(result)

    // Output:
    // [a b]
}
```

### <span id="UniqueBy">UniqueBy</span>

<p>Call iteratee func with every item of slice, then remove duplicated.</p>

<b>Signature:</b>

```go
func UniqueBy[T comparable](slice []T, iteratee func(item T) T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/UR323iZLDpv)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/slice"
)

func main() {
    nums := []int{1, 2, 3, 4, 5, 6}
    result := slice.UniqueBy(nums, func(val int) int {
        return val % 3
    })

    fmt.Println(result)

    // Output:
    // [1 2 0]
}
```

### <span id="Union">Union</span>

<p>Creates a slice of unique values, in order, from all given slices. using == for equality comparisons.</p>

<b>Signature:</b>

```go
func Union[T comparable](slices ...[]T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/hfXV1iRIZOf)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums1 := []int{1, 3, 4, 6}
    nums2 := []int{1, 2, 5, 6}

    result := slice.Union(nums1, nums2)

    fmt.Println(result)

    // Output:
    // [1 3 4 6 2 5]
}
```

### <span id="UnionBy">UnionBy</span>

<p>UnionBy is like Union, what's more it accepts iteratee which is invoked for each element of each slice.</p>

<b>Signature:</b>

```go
func UnionBy[T any, V comparable](predicate func(item T) V, slices ...[]T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/HGKHfxKQsFi)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3, 4}

    divideTwo := func(n int) int {
        return n / 2
    }
    result := slice.UnionBy(divideTwo, nums)

    fmt.Println(result)

    // Output:
    // [1 2 4]
}
```

### <span id="UpdateAt">UpdateAt</span>

<p>Update the slice element at index. if param index &lt 0 or index &lt= len(slice), will return error. </p>

<b>Signature:</b>

```go
func UpdateAt[T any](slice []T, index int, value T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/f3mh2KloWVm)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result1 := slice.UpdateAt([]string{"a", "b", "c"}, -1, "1")
    result2 := slice.UpdateAt([]string{"a", "b", "c"}, 0, "1")
    result3 := slice.UpdateAt([]string{"a", "b", "c"}, 1, "1")
    result4 := slice.UpdateAt([]string{"a", "b", "c"}, 2, "1")
    result5 := slice.UpdateAt([]string{"a", "b", "c"}, 3, "1")

    fmt.Println(result1)
    fmt.Println(result2)
    fmt.Println(result3)
    fmt.Println(result4)
    fmt.Println(result5)

    // Output:
    // [a b c]
    // [1 b c]
    // [a 1 c]
    // [a b 1]
    // [a b c]
}
```

### <span id="Without">Without</span>

<p>Creates a slice excluding all given items.</p>

<b>Signature:</b>

```go
func Without[T comparable](slice []T, items ...T) []T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/bwhEXEypThg)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result := slice.Without([]int{1, 2, 3, 4}, 1, 2)

    fmt.Println(result)

    // Output:
    // [3 4]
}
```

### <span id="KeyBy">KeyBy</span>

<p>Converts a slice to a map based on a callback function.</p>

<b>Signature:</b>

```go
func KeyBy[T any, U comparable](slice []T, iteratee func(item T) U) map[U]T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/uXod2LWD1Kg)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    result := slice.KeyBy([]string{"a", "ab", "abc"}, func(str string) int {
        return len(str)
    })

    fmt.Println(result)

    // Output:
    // map[1:a 2:ab 3:abc]
}
```

### <span id="Join">Join</span>

<p>Join the slice item with specify separator.</p>

<b>Signature:</b>

```go
func Join[T any](s []T, separator string) string
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/huKzqwNDD7V)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3, 4, 5}

    result1 := slice.Join(nums, ",")
    result2 := slice.Join(nums, "-")

    fmt.Println(result1)
    fmt.Println(result2)

    // Output:
    // 1,2,3,4,5
    // 1-2-3-4-5
}
```

### <span id="Partition">Partition</span>

<p>Partition all slice elements with the evaluation of the given predicate functions. </p>

<b>Signature:</b>

```go
func Partition[T any](slice []T, predicates ...func(item T) bool) [][]T
```

<b>Example:<span style="float:right;display:inline-block;">[Run](https://go.dev/play/p/lkQ3Ri2NQhV)</span></b>

```go
import (
    "fmt"
    "github.com/duke-git/lancet/v2/slice"
)

func main() {
    nums := []int{1, 2, 3, 4, 5}

	result1 := slice.Partition(nums)
	result2 := slice.Partition(nums, func(n int) bool { return n%2 == 0 })
	result3 := slice.Partition(nums, func(n int) bool { return n == 1 || n == 2 }, func(n int) bool { return n == 2 || n == 3 || n == 4 })

	fmt.Println(result1)
	fmt.Println(result2)
	fmt.Println(result3)

	// Output:
	// [[1 2 3 4 5]]
	// [[2 4] [1 3 5]]
	// [[1 2] [3 4] [5]]
}
```