---
created: 2022-06-05 21:11
updated: 2022-06-05 21:30
---
---
**Links**: [[103 Golang Index]]

---
## Modules
- A **module is a collection of Go packages** stored in a file tree with a `go.mod` file at its root.
	- It is like `package.json` in npm and is used for dependency management.
	- We *can use different versions of the same dependency*.
- Basic structure of the `go.mod` file
```go
module <name>
go <version>
require <module-path> <version>
```
- `go mod init name` to initialise a go module
	- Typically its `host hosting the code/user or organisation/repo name`: `github.com/user/repo`
- `go mod tidy`: to add the third party and remove packages from `go.mod` file as and when you add and remove third party imports from your source files.
- If we want to get some modules we can use `go get ...` 

> [!note]- *Module name is the import path prefix* for all packages within the module (local packages).

### Sample Project Structure
![[attachments/Pasted image 20220605211214.png]]
![[attachments/Pasted image 20220605210033.png]]
![[attachments/Pasted image 20220605210054.png]]

> [!note]- **While importing we are importing by directory name and not the package name**. But while using anything inside the source code we are using package name.

- Example
	- ![[attachments/Pasted image 20220605212743.png]]
	- ![[attachments/Pasted image 20220605212826.png]]
	- Better to use directory name as the package name

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