+++
date = "2015-08-01"
Description = "Loops and iterations in GoLang."
Keywords = ["Development", "GoLang"]
Section = "post"
Slug = "loops-and-iterations-in-golang"
Tags = ["Go", "Language"]
Title = "Loops And Iterations in GoLang"
+++

Like any other language Go has its way of doing things such as for, while, <!--more-->

## 'os' package

**For loop**

The most simple approach can be done through "os" package. The error handling is Go-like; failing calls return values of type error rather than error numbers.

````go

	// map
	var mapCol = make(map[int]string)
	mapCol[1] = "Hellp"
	mapCol[2] = "me"

	fmt.Println(mapCol)

``
The preferred approach after opening any file is safe closing that file. Go has a modern way of doing this by calling 'defer' statement. It's perfect for situations when resources must be release regardless of which path a function takes to return. For example, in opening multiple files; defer guarantees that  all resources will be safely released if any error occurred during opening one the files.

**While loop**

In order to show the file's content, I created a buffer to keep the chunks that I read and iterate over that to show the content.


```go
	var arrStr [3]int
	arrStr[0] = 10
	arrStr[1] = 12

	slicer := arrStr[1:]
	slicer = append(slicer, 23)
	fmt.Println(slicer)

````

## 'bufio' package

'bufio' provides buffering under the hood and makes really when we're working with lots of reads and writes, specially for text files.
'NewReader' returns a reader whose buffer has default size. For example for reading a file the code looks like below.

```golang

	reader := bufio.NewReader(file) // make a read buffer

	data := make([]byte, 1024)
	count, err := reader.Read(data) // read a chunk

	if err != nil && err != io.EOF {
		panic(fmt.Sprintf("an error occured in reading the file: {%s}", "data"))
	}

	for i := 0; i < count; i++ {
		fmt.Print(string(data[i]))
	}

```

**Writing to a file**

Three methods Write(p byte[]), WriteByte(c byte), WriteString(s string) are all write some content into the buffer.

```Go

	// open output file
	output, err := os.Create("output.txt")

	if err != nil {
		panic(fmt.Sprintf("an error occured in creating the file: {%s}", "output"))
	}

	for i := 0; i < count; i++ {
		n2, err := output.Write(data[:i])
		if err != nil {
			panic(err)
		}
	}

```

## 'bufio' package

Likewise reading from file, 'bufio' provides some methods when writing a buffer to a file.
