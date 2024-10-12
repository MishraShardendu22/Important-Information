## http and Gorilla Mux

- **Axios** (like Go's `http.Get` or `http.Post`) is used to retrieve information or send data to APIs.
- **Gorilla Mux** (like **Express.js**) is used to handle routing and incoming requests.

### Let's look at a comparison of **Express.js** and **Go with Gorilla Mux** for handling incoming requests.

#### **Express.js Example (Node.js)**:
```javascript
const express = require('express');
const app = express();  // Initialize the app

// Define a GET route for the home page
app.get('/', (req, res) => {
    res.send('<h1>Welcome to My Express App</h1>');  // Send response
});

// Define a GET route with a path parameter
app.get('/user/:id', (req, res) => {
    const userId = req.params.id;  // Get the dynamic part of the URL
    res.send(`User ID is: ${userId}`);  // Respond with the user ID
});

// Start the server
app.listen(3000, () => {
    console.log('Server is running on port 3000');
});
```

### **Similar Code in Go with Gorilla Mux**:
```go
package main

import (
	"fmt"
	"log"
	"net/http"
	"github.com/gorilla/mux"
)

func main() {
	// Initialize the router
	r := mux.NewRouter()

	// Define a GET route for the home page
	r.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		w.Write([]byte("<h1>Welcome to My GoLang App</h1>")) // Send response
	}).Methods("GET")

	// Define a GET route with a path parameter
	r.HandleFunc("/user/{id}", func(w http.ResponseWriter, r *http.Request) {
		vars := mux.Vars(r)      // Get the dynamic part of the URL
		userId := vars["id"]     // Extract 'id' from the route
		w.Write([]byte(fmt.Sprintf("User ID is: %s", userId))) // Respond with the user ID
	}).Methods("GET")

	// Start the server
	log.Fatal(http.ListenAndServe(":3000", r)) // Start the server on port 3000
}
```

### Breakdown:

1. **Express.js**:
   - `app.get('/', (req, res))`: Defines a route where the server listens for **GET** requests to `/`. 
   - `req.params`: In Express, `req.params` is used to extract route parameters like `/user/:id`.
   - `app.listen(3000)`: Starts the server on port 3000.

2. **Gorilla Mux (Go)**:
   - `r.HandleFunc("/", handler)`: Similar to `app.get`, this defines a route where the server listens for **GET** requests to `/`.
   - `mux.Vars(r)`: This function extracts path parameters, similar to `req.params` in Express.
   - `http.ListenAndServe(":3000", r)`: Starts the server on port 3000 (like `app.listen` in Express).

### Key Similarities:
- **Express.js**: Uses `app.get()` for routing.
- **Gorilla Mux**: Uses `r.HandleFunc()` for routing.
- Both handle dynamic URLs with parameters (`/user/:id` in Express and `/user/{id}` in Gorilla Mux).
- Both use functions (`req, res` in Express and `http.ResponseWriter, *http.Request` in Go) to manage requests and responses.


------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


Q.) "databytes,err := ioutil.ReadAll(response.Body)" this is showing a line-through and when fixing itm this is what is being used "databytes, err := io.ReadAll(io.Reader(response.Body))"


A.) In Go 1.16, the `ioutil` package was deprecated, and its functions were moved to more appropriate places within the `io` and `os` packages. The preferred method is now:

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
