# Go Channel Direction

## 1. Bidirectional Channel

```go
chan int
```

Bisa **send + receive**.

```go
func worker(ch chan int) {
    ch <- 10      // SEND
    value := <-ch // RECEIVE

    fmt.Println(value)
}
```

---

## 2. Send Only

```go
chan<- int
```

Hanya bisa **send**.

```go
func producer(ch chan<- int) {
    ch <- 10 // SEND

    // value := <-ch // ERROR
}
```

---

## 3. Receive Only

```go
<-chan int
```

Hanya bisa **receive**.

```go
func consumer(ch <-chan int) {
    value := <-ch // RECEIVE

    fmt.Println(value)

    // ch <- 10 // ERROR
}
```

---

## Example

```go
func producer(ch chan<- int) {
    ch <- 100
    ch <- 200
    close(ch)
}

func consumer(ch <-chan int) {
    for value := range ch {
        fmt.Println(value)
    }
}

func main() {
    ch := make(chan int)

    go producer(ch)
    consumer(ch)
}
```

## Quick Reference

```text
chan int    → SEND + RECEIVE
chan<- int  → SEND ONLY
<-chan int  → RECEIVE ONLY
```

### Remember

```text
chan<-   → SEND
<-chan   → RECEIVE
```
