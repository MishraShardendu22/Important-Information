## [Links to hte Docs](https://redis.io/docs/latest/develop/connect/clients/go/)

Connect
The following example shows the simplest way to connect to a Redis server:

``` GoLang
import (
	"context"
	"fmt"
	"github.com/redis/go-redis/v9"
)

func main() {    
    client := redis.NewClient(&redis.Options{
        Addr:	  "localhost:6379",
        Password: "", // No password set
        DB:		  0,  // Use default DB
        Protocol: 2,  // Connection protocol
    })
}
```
