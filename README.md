# gopackagetest

This is for learning Go import, package, and module.

## import

> An import path is a string that **uniquely** identifies a package. A package's import path corresponds to its location inside a workspace or in a remote repository

from https://golang.org/doc/code.html#ImportPaths

> The concept of import paths have some important properties:
>
> - Import paths can be globally unique.
> - In conjunction with GOPATH, import path can be translated unambiguously to a directory path.
> - Any directory path under GOPATH can be unambiguously translated to an import path.

from https://stackoverflow.com/a/17541170/1216961

(the package name is `myproject`)
> GOPATH
>
> Assume your project resides here:
>
>```go 
> $GOPATH/src/github.com/myuser/myproject
>```
>
>Your import path should be:
>
>```go 
> import "github.com/myuser/myproject/platform"
>```
>VGO
>
>Assume your go.mod file is:
>
>```go 
>module example.com/myuser/myproject
>```
>Your import path should be:
>
>```go 
>import "example.com/myuser/myproject/platform"
>```

from https://stackoverflow.com/a/52026558/1216961

## package

A package is a directory.

package name v.s. package declaration

> - A package name is the name of the directory contained in src directory.
> - Package declaration which should be the first line of code, can be different than package name.

from https://medium.com/rungo/everything-you-need-to-know-about-packages-in-go-b8bac62b74cc

The package name is the directory name of the source file. In the caller file, it is used in `import` (along with $GOPATH or module name)

The package declaration in the source file is declared after `package`. In the caller file, it used in the code as a global variable after imported.

## module

> A module is a collection of Go packages stored in a file tree with a go.mod file at its root.
from https://blog.golang.org/using-go-modules

## Code example

File structrure:

```bash
$ tree gopackagetest/
gopackagetest/
├── README.md
├── foo
│   └── bar.go
├── go.mod
└── main.go
```

go.mod content:

```bash
$ cat go.mod
module github.com/yetsun/gopackagetest

go 1.12
```

In package `foo`, content of the file `bar.go`:

```go
package baz

var Qux = 123488
```

The package name is `foo`. The package declaration is `baz`. They are different. 

When using this package, in `main.go`, import path is the module name + package name:

```go
import "github.com/yetsun/gopackagetest/foo"
```

Package declaration `baz` is used to create a global variable in main.go:

```go
func main() {
    fmt.Println(baz.Qux)
}
```

Run the code:

```go
$ go run main.go
123488
Hello World
```

Note:
> There's no such thing as "local package".
https://stackoverflow.com/a/52026558/1216961
https://stackoverflow.com/questions/17539407/golang-how-to-import-local-packages-without-gopath
