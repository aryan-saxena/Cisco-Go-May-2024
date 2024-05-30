# Go Foundation

## Magesh Kuppan
- tkmagesh77@gmail.com

## Schedule
| What          | When |
| ------------- | ------------------ |
| Commence      | 09:00 AM |
| Tea Break     | 10:30 AM (20 mins) |
| Lunch Break   | 12:30 PM (1 hour) |
| Tea Break     | 03:00 PM (20 mins) |
| Wind up       | 05:00 PM |

## Methodology
- No powerpoints
- Code & Discussion
- No dedicated time for Q&A

## Repository
[Git](https://github.com/tkmagesh/cisco-go-may-2024)

## Software Requirements
- Go tools (https://go.dev/dl)
    - Verification
        ```shell
        go version
        ```
- [Visual Studio Code](https://code.visualstudio.com)
- [Go extensions for VSCode](https://marketplace.visualstudio.com/items?itemName=golang.Go)
- Any Git Client

## Why Go?
- Simplicity
    - ONLY 25 keywords
    - Not(s)
        - No access modifiers (no public/private etc)
        - No classes (ONLY structs)
        - No inheritance (ONLY composition)
        - No reference types (everything is a value)
        - No exceptions (ONLY errors)
        - No try..catch..finally 
        - No implicit type conversion
        - No pointer arithmatic
- Performance
    - Compiled to target platform
    - Tooling support for cross-compilation
    - On par with C++
- Managed (memory) Environment
    - Builtin Garbage Collector
- Concurrency Support
    - Uses lightweight threads called Goroutines (alernatives to OS Threads)
    - Goroutines are extremely cheap (~4kb vs ~2MB for OS Threads)
    - Builtin scheduler to schedule the goroutines
    - Language support for concurrency
        - go keyword, channel (data type), channel operator ( <- ), for..range & select..case language constructs
    - APIs support (standard library)
        - "sync" package
        - "sync/atomic" packages

## Compile & Execute
### Compile
```shell
go build [file_name.go]

go build -o [binary_name] [file_name.go]
```

### Compile & Execute
```shell
go run [file_name.go]
```

### To list all the environment variables
```shell
go env
```

### To list a few environment variables
```shell
go env [var_1] [var_2]
```

### Env variables for cross compilation
- GOOS
- GOARCH

### To get the list of supported platforms (for compilation)
```shell
go tool dist list
```

### To cross compile
```shell
GOOS=[target_os] GOARCH=[target_arch] go build [filename.go]

ex:
GOOS=linux GOARCH=amd64 go build 01-hello-world.go
```

## Data types
- string
- bool
- Integers
    - int8
    - int16
    - int32
    - int64
    - int
- Unsigned Integers
    - uint8
    - uint16
    - uint32
    - uint64
    - uint
- Floating point
    - float32
    - float64
- Complex Types
    - complex64 [ real (float32) + imaginary (float32) ]
    - complex128 [ real (float64) + imaginary (float64) ]
- Type aliases
    - byte (alias for uint8)
    - rune (alias for int32, unicode code point)

## Variables
### using 'var' (To declare variables)
```go
    var [var_name] [data_type]
    var [var_1], [var_2] [data_type]
```

### using ':=' (To declare & initialize)
```go
    [var_name] := [data]
```

### Function Scope
- Can use :=
- Cannot have unused variables

### Package Scope
- CANNOT use :=
- Can have unused variables

## IOTA 
    - auto generated constants

## Programming Constructs
### if else
### switch case
### for

## Functions
- More than one return results
- Anonymous functions
- Functions can be assigned to variables
- Higher Order Functions
    - Pass functions as arguments 
    - Return functions as return values
- Deferred functions (functions whose executions are postponed)

## Errors
- Error is just any object implementing "error" interface
- Errors are not "thrown" but returned
- Errors are the last in the list of return results (by convention)
- Creating an error
    - errors.New()
    - fmt.Errorf()
    - Custom type (struct) implementing the "error" interface 

## Panic & Recovery
### Panic
- State of the application where the application execution cannot proceed further
- Creating a panic
    - using the "panic()" function
    - typically the panic is created with an error

### Recovery
- recover() returns the error that resulted in a panic OR nil if no panic

## Pointer
- Address in the memory
- Pointers are type safe in go
- Used to pass the data as reference
- Pointer arithmatic are NOT supported

## Collections (Array, Slice & Map)
### Array
- Fixed sized typed collection
- Memory is allocated and initialized with the default (zero) value of the underlying data type during declaration
- Arrays are just values

### Slice
- Varying sized typed collection
- Memory is NOT allocated and initialized during declaration
- Slice maintains a pointer to an underlying array
- use "append()" to dynamically add new items to the slice
![image](./images/slices.png)

### Map
- Typed collection of key/value pairs
- Initialize using the "make()" 

## Modules & Packages
### Module
- Any code that need to be versioned and deployed together
- Typically a module is a folder with "go.mod" file
- "go.mod" file
    - manifest file for the module with metadata information
    - name of the module
        - the complete repo path (recommended)
    - go runtime version targetted
    - dependencies
- Create a module
```shell
go mod init <module_name>
```
- Execute a module
```shell
go run .
```
- Build a module
```shell
go build .
OR
go build -o [bindary_name] .
```
- To use a 3rd party a package (downloaded in the GOPATH/pkg/mod folder)
```shell
go get [module_name]
```
- To sync the go.mod file with dependency info
```shell
go mod tidy
```
- To download the dependencies documented in the go.mod fule
```shell
go mod download
```
- To localize the dependencies (in "vendor" folder)
```shell
go mod vendor
```
- To install a go module as a command-line tool (installed in the GOPATH/bin folder)
```shell
go install [module_name]
```
- Other useful mod commands
```shell
go mod graph
go mod why [module_name]
go list -m all
```
#### Reference
[Documentation](https://go.dev/ref/mod)


### Package
- internal organization of a module
- typically a folder
- Can be nested

## Structs
- like classes
- custom type to hold related data

## Methods 
- Functions with receivers

## Interfaces
- Contracts
- Interfaces are implicitly implemented
- Can be composed

## Concurrency Programming
- Designing with multiple execution paths
- Typically achieved with OS Threads
- OS Threads are costly
    - ~2MB of memory
    - Creation & Destruction of threads are costly
    - Thread context switch are time consuming
![image](./images/os-thread-concurrency.png)

## GO Concurrency
- A concurrent operation is represented as a light-weight thread called "goroutine"
- Goroutines are cheap
    - ONLY ~4kb per goroutine
    - Minimum thread context switch
- Built in scheduler to schedule the goroutines
![image](./images/go-concurrency.png)

### Concurrency Features in Go
- Concurrency support is built in the language itself
    - go "keyword", channel "data type", channel "operator" ( <- ), range & select-case "constructs"
- APIs
    - sync package
    - sync/atomic package

#### Channels
- Data type designed to enable communication between goroutines in a concurrent safe manner
- Declaration
```go
var ch chan int
```
- Initialization
```go
ch = make(chan int)
```
- Declaration & Initialization
```go
ch := make(chan int)
```
- Operation
    - Using the channel operator ( <- )
    - Send Operation
    ```go
        ch <- 100
    ```
    - Receive Operation
    ```go
        data := <- ch
    ```
- Behavior
![image](./images/channel-behavior.png)


## Http Services (Intro)
- An application that listens and repond to http requests