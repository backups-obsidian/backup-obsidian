---
created: 2022-05-14 21:41
updated: 2022-05-14 23:04
---
---
**Links**: [[../100 home | 100 Home]]

---
- Each Go source file begins with a package declaration which indicates what package the file is part of.
- Every Go program must be included in a package.
- `package main`: 
	- This means file belongs to the main package.
	- This is an *executable package* that generates a standalone application file that can be run.
	- The name of the executable package is predefined and is always called **main**.
	- This package must also have a function named main defined inside it.
	- The main package must have package name main and declare a function main that takes no arguments and returns no value.
	- If a package is not main then it is non executable but can be imported by other packages.

- Package declaration is followed by import statements. 
- The package to be imported is written in quotes.
- `go run main.go` is used to compile and run the file. It doesn't create any executable.
- `go build` creates an executable with the same name as directory inside the directory. If you want to give the executable another option then you use `go build -o other_name`
	- In a directory that contains many Go source files you run `go build`. It will compile all the source files in the current directory and will produce an executable with the name of the directory.
- We can compile the executable binary for any OS in any OS using the `GOOS` and `GOARCH` parameters.
	- `GOOS=linux GOARCH=amd64 go build -o linuxapp`
- `gofmt` is formatting the go files according to a set standard. Eg: `gofmt -w main.go` here -w means it will overwrite the source file.
	- You can also run it on the whole directory `gofmt -w directory_path`
	- or you can run `go fmt` in the parent directory and it will format the code of all the go files.

