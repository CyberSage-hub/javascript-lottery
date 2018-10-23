
```go
/*	dir, _ := os.Getwd() //当前的目录
	println(dir)
	err := os.MkdirAll(dir+"/md/demo.txt", os.ModePerm)
	if err != nil {
		fmt.Println(err)
	}*/
	data, _ := os.Readlink("src") //我的linux返回的是/home/widuu/go/src
	fmt.Println(data)
	f, _ := os.Create("widuu_2.go")
	defer f.Close()

	fmt.Println(f)
	fd, _ := f.Stat()
	fmt.Println(fd.Mode())
	fmt.Println(fd.ModTime())
	os.Chmod("widuu_2.go",0777)
  ```
