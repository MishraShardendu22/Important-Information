## "databytes,err := ioutil.ReadAll(response.Body)" this is showing a line-through and when fixing itm this is what is being used "databytes, err := io.ReadAll(io.Reader(response.Body))"

In Go 1.16, the `ioutil` package was deprecated, and its functions were moved to more appropriate places within the `io` and `os` packages. The preferred method is now:

```go
databytes, err := io.ReadAll(response.Body)
```

Here's why:
- The `ioutil.ReadAll` function was deprecated because the `io` package already had similar functionality and consolidating it there simplifies the standard library.
- The `io.ReadAll` is the replacement for reading all data from an `io.Reader` like `response.Body`.

So, it's better to use the newer, non-deprecated version as follows:

```go
databytes, err := io.ReadAll(response.Body)
```
