洗牌算法：产生一个随机序列

```go
package main

import (
	"fmt"
	"math/rand"
	"time"
)

func main() {
	fmt.Println(Shuffle([]int{10,20,30,40}))
}

func Shuffle(vals []int) []int  {
	newVals := make([]int,0,len(vals))
	r := rand.New(rand.NewSource(time.Now().Unix()))
	for _,i := range r.Perm(len(vals)) {
		newVals = append(newVals, vals[i])
	}
	return newVals
}

```

关键步骤：r.Perm()，解释：
```go
// Perm returns, as a slice of n ints, a pseudo-random permutation of the integers [0,n).
func (r *Rand) Perm(n int) []int {
	m := make([]int, n)
	// In the following loop, the iteration when i=0 always swaps m[0] with m[0].
	// A change to remove this useless iteration is to assign 1 to i in the init
	// statement. But Perm also effects r. Making this change will affect
	// the final state of r. So this change can't be made for compatibility
	// reasons for Go 1.
	for i := 0; i < n; i++ {
		j := r.Intn(i + 1)
		m[i] = m[j]
		m[j] = i
	}
	return m
}
```