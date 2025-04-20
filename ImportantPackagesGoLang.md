# GoLang Tool Integrations
This file provides setup instructions for several essential GoLang tools used for development, environment management, and application structuring. These commands make it easier to manage dependencies, handle hot reloading, and manage environment variables in Go.

---

### MongoDB Driver
To integrate MongoDB with GoLang for database operations, use the official MongoDB Go driver. 

```go
go get go.mongodb.org/mongo-driver/mongo
```

### Air (Hot Reloading for Go)
Air is Go's version of nodemon, enabling live reloading as you code. Useful for faster development cycles.

```go
go get -u github.com/air-verse/air
```

### Dotenv (Environment Variables)
To load environment variables from a `.env` file, you can use the `godotenv` package. This is essential for securely managing configurations like API keys and database URIs.

```go
go get github.com/joho/godotenv
```

### Fiber (Express-like Web Framework for Go)
Fiber is a popular web framework inspired by Express.js, offering performance and simplicity for building APIs and web applications.

```go
go get github.com/gofiber/fiber/v2
```

### Middleware for Fiber
Fiber supports middleware for adding functionalities like CORS, logging, and security headers. Common middleware packages include:

```go
go get github.com/gofiber/cors/v2
go get github.com/gofiber/logger/v2
```

### Go Mod Tidy (Dependency Management)
`go mod tidy` is Go's equivalent of `npm install`. It cleans up and ensures all dependencies are included and properly referenced in `go.mod`.

```bash
go mod tidy
```

Command To Clean module cache 
```bash
go clean -modcache
```
