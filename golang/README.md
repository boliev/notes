# Golang Notes

## Main
Go is a call by value language. Every time you pass a parameter to a function, Go makes a copy of the value that’s passed in. Passing a slice to the append function actually passes a copy of the slice to the function.

## Run and install
```shell
go mod init github.com/boliev/fnl-news
go run main.go //will run the code. The executable file will be deleted after exit
go run —work main.go //will show the executable file
go build main.go //will compile the app
go build -o hello_world hello.go //will an put executable file like hello.go
```

## Code quality
```shell
go fmt ./...
golint ./...
go vet ./...
```
Or we can use [golangci-lint](https://golangci-lint.run/usage/install/)
```shell
golangci-lint run
```
Check for shadowing
```shell
go install golang.org/x/tools/go/analysis/passes/shadow/cmd/shadow@latest
shadow ./...
```

## go get
```shell
go get -u github.com/gin-gonic/gin
go get -u gorm.io/gorm
go get -u gorm.io/driver/postgres
go get github.com/spf13/viper
go get github.com/sirupsen/logrus
go get 'go.uber.org/dig@v1'
go get github.com/dgrijalva/jwt-go
go get github.com/stretchr/testify
```

## Variables
```golang
var power int
power = 900 
```
```golang
var power int = 900
```
```golang
power := 900
```
```golang
name, power := “Vladimir”, 900
```

## Structures
Structures don’t have constructors.
Instead you create a function, that returns an instance of desired type (like a factory). 
Methods must be declared in the same package as their associated type; Go doesn’t allow you add methods to types you don’t control.

```golang
func NewSaiyan(name string, power int) *Saiyan {
    return &Saiyan{
        Name: name,
        Power: power,
    }
}
```

The result of `new(X)` is the same as `&X{}`. It allocates required memory and returns pointer.

```golang
goku := new(Saiyan)
// same as
goku := &Saiyan{}
```

```golang
type person struct {
    name string
    age  int
    pet  string
}

var fred person
bob := person{}
```
```golang
julia := person{
    "Julia",
    40,
    "cat",
}

beth := person{
    age:  30,
    name: "Beth",
}
```

### Composition
```golang
type Person struct {
    Name string
}
func (p *Person) Introduce() {
    fmt.Printf("Hi, I'm %s\n", p.Name)
}
type Saiyan struct {
    *Person
    Power int
}

// and to use it:
goku := &Saiyan{
    Person: &Person{"Goku"},
    Power: 9001,
}
goku.Introduce()
```

The `Saiyan` structure has a field of type `*Person`. Because we didn’t give it an explicit field name, we can implicitly
access the fields and functions of the composed type. However, the Go compiler did give it a field name, consider the
perfectly valid
```golang
goku := &Saiyan{
    Person: &Person{"Goku"},
}
fmt.Println(goku.Name)
fmt.Println(goku.Person.Name)
```

## Arrays
```golang
var scores [10]int
scores[0] = 339
```
```golang
scores := [4]int{9001, 9333, 212, 33}
```
```golang
for index, value := range scores {

}
```
Remove the first element

```golang
arr = arr[1:]
```
Reverse array

```golang
func reverseArr(arr []int) []int {
    for i, j := 0, len(arr)-1; i < j; i, j = i+1, j-1 {
        arr[i], arr[j] = arr[j], arr[i]
    }
    return arr
}
```

## Slices
A slice isn’t comparable. It is a compile-time error to use == to see if two slices are identical or != to see if they are different. The only thing you can compare a slice with is nil.
```golang
var x []int
```
```golang
scores := []int{1,4,293,4,9}
```
```golang
scores := make([]int, 10)
```
We use `make` instead of new because there’s more to creating a slice than just allocating the memory (which is what new does).

```golang
names := []string{"leto", "jessica", "paul"}
checks := make([]bool, 10)
var names []string
scores := make([]int, 0, 20)
```

```golang
var x = []int{1,2,3}
x = append(x, 4)
x = append(x,5,6,7)
```

Add one slice is appended onto another by using the … operator to expand the source slice into individual values

```golang
var x = []int{1,2,3}
y := []int{20,30,40}
x = append(x, y...)
```

## Maps
Maps are not comparable. You can check if they are equal to nil, but you cannot check if two maps have identical keys and values using == or differ using !=
```golang
var nilMap map[string]int
```
```golang
totalWins := map[string]int{}
```
```golang
teams := map[string][]string {
    "Orcas": []string{"Fred", "Ralph", "Bijou"},
    "Lions": []string{"Sarah", "Peter", "Billie"},
    "Kittens": []string{"Waldo", "Raul", "Ze"},
}
```
```golang
m := map[string]int{
    "hello": 5,
    "world": 0,
}
v, ok := m["hello"]
fmt.Println(v, ok)
```
```golang
func main() {
    lookup := make(map[string]int)
    lookup["goku"] = 9001
    power, exists := lookup["vegeta"]
    // prints 0, false
    // 0 is the default value for an integer
    fmt.Println(power, exists)
    // returns 1
    total := len(lookup)
    // has no return, can be called on a nonexisting key
    delete(lookup, "goku")
}
```

```golang
type Saiyan struct {
    Name string
    Friends map[string]*Saiyan
}
goku := &Saiyan{
    Name: "Goku",
    Friends: make(map[string]*Saiyan),
}
goku.Friends["krillin"] = ... //todo load or create Krillin
```
```golang
lookup := map[string]int{
    "goku": 9001,
    "gohan": 2044,
}
```
```golang
for key, value := range lookup {
...
}
```
```golang
commits := map[string]int{
    "rsc": 3711,
    "r":   2138,
    "gri": 1908,
    "adg": 912,
}
```
The delete function takes a map and a key and then removes the key-value pair with the specified key. If the key isn’t present in the map or if the map is nil, nothing happens. The delete function doesn’t return a value.
```golang
m := map[string]int{
    "hello": 5,
    "world": 10,
}
delete(m, "hello")
```

## Functions
Go doesn’t have named and optional input parameters. If you want to emulate named and optional parameters, define a struct that has fields that match the desired parameters, and pass the struct to your function.
In practice, not having named and optional parameters isn’t a limitation. A function shouldn’t have more than a few parameters and named and optional parameters are mostly useful when a function has many inputs. If you find yourself in that situation, your function is quite possibly too complicated.

Since Go is a call by value language, the values passed to functions are copies. For non-pointer types like primitives, structs, and arrays, that means that the called function cannot modify the original. Since the called function has a copy of the original data, the immutability of the original data is guaranteed.

When you pass a nil pointer to a function, you cannot make the value non-nil. You can only reassign the value if there was a value already assigned to the pointer. While confusing at first, it makes sense. Since the memory location was passed to the function via call-by-value, we can’t change the memory address, any more than we could change the value of an int parameter.



## Pointers
A pointer is simply a variable that holds the location in memory where a value is stored.

The `&` is the address operator. It precedes a value type and returns the address of the memory location where the value is stored.

```golang
x := "hello"
pointerToX := &x

```

The `*` is the indirection operator. It precedes a variable of pointer type and returns the pointed-to value. This is called `dereferencing`.

```golang
x := 10
pointerToX := &x
fmt.Println(pointerToX)  // prints a memory address
fmt.Println(*pointerToX) // prints 10
z := 5 + *pointerToX
fmt.Println(z)           // prints 15
```
Before dereferencing a pointer, you must make sure that the pointer is non-nil. Your program will panic if you attempt to dereference a nil pointer.

```golang
var x *int
fmt.Println(x == nil) // prints true
fmt.Println(*x)       // panics”
```
A pointer type is a type that represents a pointer. It is written with a * before a type name. A pointer type can be based on any type.

```golang
x := 10
var pointerToX *int
pointerToX = &x”
```
The other common usage of pointers in Go is to indicate the difference between a variable or field that’s been assigned the zero value and a variable or field that hasn’t been assigned a value at all. If this distinction matters in your program, use a nil pointer to represent an unassigned variable or struct field.


## Sorting
Sort int slice desc

```golang
sort.Sort(sort.Reverse(sort.IntSlice(are)))
```

## MaxInt MinInt
```golang
const MaxInt = int(^uint(0) >> 1)
const MinInt = -MaxInt - 1
```

## Concurrency and Parallelism
### Thread vs Process
 - Process is the app instance, undependent object, who has system recources,. It has its own dedicated address space. One process can't get access to variables and data structures of another process. Only through files or other interprocess communication channels.
 - Thread uses the same stack space as a process. Many threads share the data of thair states. Each thread can iterate with the same memory.

## Questions
 - Race-conditions?
 - Concurrency and Parallelism? What is the difference?
 - unbuffered and buffered channel