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

After connecting, you can test the connection by storing and retrieving a simple string:

``` GoLang
ctx := context.Background()

err := client.Set(ctx, "foo", "bar", 0).Err()
if err != nil {
    panic(err)
}

val, err := client.Get(ctx, "foo").Result()
if err != nil {
    panic(err)
}
fmt.Println("foo", val)
```

Redis allows you to create multiple databases within a single Redis server instance. Each of these databases is indexed with integers starting from 0. By default, Redis has 16 databases (0 to 15), but this can be configured.

Key Characteristics:

Each database is isolated; keys in one database do not affect keys in another.
You specify which database to use by providing its index when creating a client connection.
Example
Let's say you have the following two databases in your Redis server:

Database 0:

Keys: user:1 -> {"name": "Alice"}
Keys: user:2 -> {"name": "Bob"}
Database 1:

Keys: order:1 -> {"item": "Laptop", "quantity": 1}
Keys: order:2 -> {"item": "Phone", "quantity": 2}
When you connect to Database 0 with CreateClient(0), you can access the user:1 and user:2 keys, but you cannot see the order:1 and order:2 keys in Database 1 unless you connect to that database (using CreateClient(1)).


### Cleaning the URL

The `cleanURL` variable is constructed to isolate the domain portion of a given URL. Here's how it works step-by-step:

1. **Trimming HTTP/HTTPS Prefix**: 
   - The `strings.TrimPrefix` function removes the `http://` or `https://` prefix if they are present. This ensures that the comparison focuses only on the actual domain name.
  
   Example:
   - Input: `http://example.com`
   - After trimming: `example.com`
   
2. **Removing "www." Prefix**: 
   - It removes the `www.` prefix to standardize the domain name for comparison. Many domains can be accessed both with and without `www`, so this helps treat them as equivalent.
  
   Example:
   - Input: `www.example.com`
   - After trimming: `example.com`

3. **Extracting the Main Domain**: 
   - `strings.Split(cleanURL, "/")[0]` splits the string at the first `/` and retrieves the first element, which is the main domain. This also ensures that if there are any additional path components in the URL (like `/about`), they are removed.
  
   Example:
   - Input: `example.com/about`
   - After splitting: `example.com`

### Final `cleanURL` Examples

Here are some examples of how different URLs would be transformed into `cleanURL`:

| Input URL                    | `cleanURL`           |
|------------------------------|----------------------|
| `http://example.com`         | `example.com`        |
| `https://example.com`        | `example.com`        |
| `http://www.example.com`     | `example.com`        |
| `https://www.example.com`    | `example.com`        |
| `www.example.com`            | `example.com`        |
| `example.com/about`          | `example.com`        |
| `http://example.com/about`   | `example.com`        |
| `http://example.com:8080`    | `example.com:8080`   |  (If port is present, it remains unchanged)

### Why Compare `cleanURL` with `domain`

The purpose of comparing `cleanURL` with the `domain` stored in the environment variable is to determine if the URL provided is the same as the main domain of your application. This check is useful for several reasons:

1. **Security**: 
   - In web applications, you often want to restrict certain actions or resources to the main domain of your application. This helps prevent issues like cross-site request forgery (CSRF) or redirecting to malicious sites.

2. **Routing Logic**: 
   - If your application needs to differentiate between requests to the main site and requests to other domains, this check allows you to handle them accordingly.

3. **User Experience**: 
   - You might want to enforce that users only interact with your main domain (for consistency, branding, etc.), and this comparison helps in implementing that logic.

### Summary

By transforming the URL into `cleanURL`, the function ensures a standardized format for comparison with the main domain. This approach helps maintain security and correct routing behavior within the application, allowing it to make informed decisions based on the domain from which requests originate.
