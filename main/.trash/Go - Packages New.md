---
created: 2022-06-05 19:41
updated: 2022-06-05 20:59
---
---
**Links**: [[103 Golang Index]]

---
## Pre Modules Era
- Go programmers typically *keep all their Go code in a single workspace*. 
	- This was a stringent requirement before version *1.13* (released in 2019)
	- After this version more flexibility was provided on where you could store your source code.
	- A *workspace is nothing more than a directory in your file system* whose path is stored in the environment variable called `GOPATH`.
- On Windows , it's in `%USERPROFILE%\go` (For Example: `C: \Users\ad\go`)
- On Mac & Linux, it's in: `~/go` (For Example: `/home/john/go`)
- You can print out the **values of the environment variables** by running the `go env` command.
	- `go env | grep -i gopath`
- Third party tools were used for dependency management

## Packages
- A package is a **collection of go files**.
- **Every go file has to be a part of some package**. 
- Packages in Go are to be *small and many*.

### Different Types of Packages
- **Executable packages**: 
	- That generate executable files which can be run. 
	- The **name** of an executable package is **predefined** and is called `main`.
		- This package must have a **function called main**.
		- This function tells go from where to start executing code.
		- It *doesn't take any input parameters*
- **Non-executable packages**: 
	- (*Libraries or dependencies*) that are *used by other packages*. Example `fmt`
	- They can have *any name*. 
	- They **can not be executed, only imported**.

### Creating & Importing Packages
> [!caution]+ *All files in a directory must belong to the same package*. 
> - It is not allowed to have files belonging to different packages in the same directory.
> - Similarly we cannot have files of a single package in multiple directories

- It is idiomatic to use *simple and short name* for packages (like time, http, list)
- It is not advised to use `_` and camelCase naming for packages.

> [!tip] The normal *convention* is to have the **folder name be same as the package name**.

> [!note]+ Only **function/variables names starting from uppercase letter (considered public) can be used by other packages**.
> If the function/variable names are *lowercase* then they will be *considered private* and won't be exported.

- Think that while importing the package **we import the whole directory**.
- It is common to *name the source file same as that of the package directory*. This is not mandatory.
	- The package will still be imported in the same way, since we import the whole directory and not a single go file.

- [[Go - ProgramFlow#Scope|Scopes in Go]]
- `import` statements belong to the file scope and are only visible in that file.
	- So if you want to use `fmt` in multiple files of the same package then it should be imported in all those source files.

> [!note] It is possible that a package contains a single file.

### init function
- It is **called automatically when a package is initialised**, always **before the main function**.
	- We cannot call it manually.
- We can have *multiple init functions in a file* and *their order of execution will be the order in which they appear*.
- The most common use case of init functions are to **initialise global variables before main is called**.

```go
var array [2]int

func init() {
	fmt.Println("init1")
}

func main() {
	fmt.Println(array)
}

func init() {
	fmt.Println("init2")
	array = [2]int{1, 3}
}

// init1, init2, [1,3]
```

## Modules
- A **module is a collection of Go packages** stored in a file tree with a `go.mod` file at its root.
	- It is like `package.json` in npm and is used for dependency management.
- Basic structure of the `go.mod` file
```go
module <name>
go <version>
require <module-path> <version>
```
- `go mod init name` to initialise a go module
	- Typically its `host hosting the code/user or organisation/repo name`: `github.com/user/repo`
- `go mod tidy`: to add the third party and remove packages from `go.mod` file as and when you add and remove third party imports from your source files.
- We *can use different versions of the same dependency*.

## Compiling and Running Programs
- `go run main.go` is used to compile and run the file. It doesn't create any executable.
- `go build` creates an executable with the same name as directory inside the directory. 
	- If you want to give the executable another option then you use `go build -o other_name`
	- In a directory that contains many Go source files you run `go build`. It will compile all the source files in the current directory and will produce an executable with the name of the directory.
- We can compile the executable binary for any OS in any OS using the `GOOS` and `GOARCH` parameters.
	- `GOOS=linux GOARCH=amd64 go build -o linuxapp`
- `gofmt` is formatting the go files according to a set standard. Eg: `gofmt -w main.go` here -w means it will overwrite the source file.
	- You can also run it on the whole directory `gofmt -w directory_path`
	- or you can run `go fmt` in the parent directory and it will format the code of all the go files.