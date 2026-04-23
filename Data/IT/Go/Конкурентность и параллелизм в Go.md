Хотя [[Горутины и каналы в Go|каналы]] являются предпочтительным способом общения в [[Go|Go]], иногда требуется просто синхронизировать выполнение (дождаться завершения) или защитить общую память (переменные).

## WaitGroup

В пакете `sync` есть механизм синхронизации, не связанный с передачей данных: `WaitGroup`. Он используется для того, чтобы дождаться завершения коллекции [[Горутины и каналы в Go|горутин]].

**Методы `WaitGroup`:**

- `WaitGroup.Add(delta int)`: Увеличение внутреннего счетчика.

- `WaitGroup.Done()`: Уменьшение счетчика.

- `WaitGroup.Wait()`: Блокирует поток, пока счетчик не станет равен нулю.

## Mutex

Для защиты доступа к общим переменным от одновременного изменения несколькими горутинами используется `Mutex` из пакета `sync`.

**Методы `Mutex`:**

- `Mutex.Lock()`: Блокирует доступ к защищаемому коду.

- `Mutex.Unlock()`: Разблокирует доступ.

**Важно:** защищаемая переменная и `Mutex` должны быть в одной структуре. Следует использовать `defer mu.Unlock()` сразу после `mu.Lock()` для гарантии, что мьютекс будет снят, даже при панике.

## Пример использования WaitGroup + Mutex

Полный пример использования `WaitGroup` и `Mutex` для создания безопасного счетчика и параллельного подсчета.

**Пример:**

```Go
package main

import "fmt"
import "sync"
  

type SafeCounter struct {
    mu    sync.Mutex
    count int
}
  

func (c *SafeCounter) Increment() {
    c.mu.Lock()
    defer c.mu.Unlock()

    c.count += 1
}
 

func runCounter(c *SafeCounter, wg *sync.WaitGroup) {
    defer wg.Done()

    for i := 0; i < 1000; i++ {
        c.Increment()
    }
}
   

func main() {
    counter := &SafeCounter{}
    var wg sync.WaitGroup

    for i := 0; i < 5; i++ {
        wg.Add(1)
        go runCounter(counter, &wg)
    }

    wg.Wait()
    fmt.Println("Final count: ", counter.count)
}
```