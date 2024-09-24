# Learning

## React Learnings
- **`useState`**: Manages state in a functional component (like tracking form input or toggling between themes).
  
- **`useEffect`**: Handles side effects, like fetching data, setting up listeners, or updating the page title after a render.

- **`useRef`**: Accesses DOM elements or persists values across renders without triggering a re-render (like focusing an input field).

### Real Example:
On a login page:
- `useState` tracks the username and password inputs.
- `useEffect` fetches user data once the component loads.
- `useRef` focuses the cursor on the username input when the page loads.

Example: On Twitter's login page, `useState` would manage the input fields, `useEffect` would fetch user session data, and `useRef` could focus on the username input when the page loads.

## Project Name - NextJS Auth

## Suggestions - 

- [DOM] Password field is not contained in a form: (More info: https://goo.gl/9p2vKq) <input id=​"confirm_password" class=​"block border text-violet-600 rounded-2xl border-gray-300 dark:​border-gray-600 w-full p-4 mb-4 placeholder-orange-400 dark:​placeholder-orange-400 focus:​border-blue-500 dark:​focus:​border-blue-400 focus:​outline-none transition duration-500" placeholder=​"Confirm Password" type=​"password" value=​"12345678" name=​"confirm_password">​

## Answer - 

This message indicates that the `<input>` element for the password field is not inside a `<form>` element. In HTML, form elements like password fields should be within a `<form>` tag to be properly submitted to a server.
Here’s how it should be structured:

```html
  <form action="your-action-url" method="post">
    <input id="confirm_password" class="block border text-violet-600 rounded-2xl border-gray-300 dark:border-gray-600 w-full p-4 mb-4 placeholder-orange-400 dark:placeholder-orange-400 focus:border-blue-500 dark:focus:border-blue-400 focus:outline-none transition duration-500" placeholder="Confirm Password" type="password" value="12345678" name="confirm_password">
    <!-- Other form elements like submit button -->
  </form>
```

This ensures that the password field, along with other form elements, is included in the form submission.


# [JWT](https://fusionauth.io/articles/tokens/jwt-components-explained)

# Headers
| **Algorithm**         |      **Type**        |      **Key Type**       | **Security Level** |         **Performance**       | **Use Case** |
|-----------------------|----------------------|-------------------------|--------------------|-------------------------------|--------------|
| **HS256/HS384/HS512** | Symmetric            | Shared Secret           | Moderate  |           High (fast)                  | Internal systems with single-party verification.          |
| **RS256/RS384/RS512** | Asymmetric           | Public/Private Key Pair | High      |           Moderate (slower than HS)    | Distributed systems, multi-party verification, APIs.      |
| **ES256/ES384/ES512** | Asymmetric (ECDSA)   | Public/Private Key Pair | High      |           Very High (fast, small keys) | High-security and performance-critical systems            |
| **PS256/PS384/PS512** | Asymmetric (RSA-PSS) | Public/Private Key Pair | Very High |           Slower (high overhead) | Highly secure systems with enhanced cryptographic requirements. |



# Stateless authentication
Stateless authentication is a type of authentication mechanism where the server does not store any session information about the user. Instead, all the information needed to authenticate a user is included in a token, which is passed back and forth between the client and the server.

JWT (JSON Web Token) is a widely used standard for stateless authentication. In a stateless authentication system using JWT, the server doesn't store any information about the user or their session. Instead, the server generates a JWT containing all the necessary information, and the client stores and sends this token with each request.


## CSRF
### What is a CSRF Attack?

**CSRF (Cross-Site Request Forgery)** is a type of attack where a malicious website, email, or program causes a user’s browser to perform unwanted actions on a trusted site where the user is authenticated. Essentially, the attacker tricks the user into making a request on another website without their consent.

#### How CSRF Works:
1. **Authentication**: A user logs into a legitimate website (e.g., their banking site), and the website sets a cookie in the browser to track the user session.
2. **Malicious Request**: The attacker sends the user a link or includes malicious code on another site. When the user clicks or visits that malicious site, it sends an unwanted request to the legitimate site (e.g., transferring money from the user's bank account).
3. **Request Execution**: Since the user is already logged in and their browser sends cookies automatically with every request, the request appears legitimate to the server.

The server processes the request thinking it came from the authenticated user, which allows the attack to succeed.

### How JWT Protects Against CSRF:
JWT (JSON Web Tokens) **by itself does not inherently protect against CSRF attacks**, but it can help reduce the risk if implemented correctly, particularly when combined with best practices.

#### 1. **JWT in Headers (Bearer Token)**
When JWT is stored and sent using **Authorization headers** (as a Bearer token), it **does not automatically get sent with every request** like a cookie does. This prevents the attacker from forcing the user's browser to send the token without the user's consent.

- CSRF attacks rely on the automatic inclusion of cookies in requests. Since JWTs are sent manually (by JavaScript) via headers (usually under the `Authorization: Bearer <token>`), they don't suffer from the same vulnerability.
  
- If the JWT is stored in **localStorage** or **sessionStorage**, it won't be sent along with every request, making it immune to typical CSRF attacks.

#### 2. **Double Submit Cookie Approach (with JWTs)**
Another strategy to protect against CSRF while using JWTs is to combine JWTs with a **double-submit cookie**. Here’s how it works:
- The server issues a JWT to the client and stores it in localStorage or sessionStorage.
- Additionally, the server also issues a CSRF token stored in a cookie.
- For each request, the client sends the JWT in the `Authorization` header and includes the CSRF token from the cookie in the request body or header.
- The server verifies that the CSRF token from the request matches the one stored in the cookie, thus preventing CSRF attacks.

#### 3. **Stateful Authentication and CSRF**
JWTs are often used in **stateless authentication**. In this scenario, CSRF is less of a concern because the server doesn't store any session information. If the server doesn't maintain a session, there is nothing for an attacker to hijack.

### CSRF Vulnerability with JWTs
- **JWT in Cookies**: If you store JWTs in cookies and they are sent with every request, you may still be vulnerable to CSRF attacks. In this case, you'd still need to use anti-CSRF tokens.
  
- **Conclusion**: JWTs offer protection primarily by avoiding automatic transmission of tokens with requests, but they need to be implemented securely (e.g., stored in localStorage or sessionStorage). However, if JWTs are stored in cookies, additional measures like anti-CSRF tokens or same-site cookie attributes are necessary to prevent CSRF.

### Best Practices to Protect Against CSRF (with JWT):
1. **Store JWT in localStorage/sessionStorage** rather than cookies.
2. **Use the `Authorization` header** to send JWTs in API requests.
3. **Implement Same-Site cookies** for any session cookies (if using cookies at all).
4. **Double-submit cookie pattern** if you're forced to store JWTs in cookies.
5. **Use a CSRF token** in the request body or headers when dealing with forms.

By following these practices, JWT can be a good tool for mitigating CSRF risks.




# Prefetching in Next.js and React

## Prefetching in Next.js

**Prefetching** is a performance optimization technique used in Next.js to enhance user experience by loading page content before it's requested. This helps make navigation faster and reduces perceived latency.

### How Prefetching Works

1. **Automatic Prefetching**:
   - Next.js automatically prefetches pages for links that are visible in the viewport when using the `<Link>` component from `next/link`.
   - Prefetching occurs when a link is visible and the browser is idle, or when the user hovers over a link. The page's JavaScript and data are loaded in advance.

2. **Implementation**:
   - **`<Link>` Component**: Uses Next.js's `<Link>` component for automatic prefetching.
   - **Intersection Observer**: Utilizes the Intersection Observer API to detect when a link is in the viewport.

3. **Disabling Prefetching**:
   - To disable prefetching for a specific link, set the `prefetch` prop to `false`.

   ```jsx
   import Link from 'next/link';

   <Link href="/about" prefetch={false}>
     About
   </Link>
   ```

4. **Server-Side Handling**:
   - Prefetching requests the server to provide the necessary data, ensuring correct and updated content upon navigation.

5. **Customizing Prefetch Behavior**:
   - You can customize prefetch behavior using the `prefetch` prop:
     - `prefetch={true}`: Default behavior, prefetches automatically.
     - `prefetch={false}`: Disables prefetching for the link.
     - `prefetch="viewport"`: Only prefetch when the link is in the viewport (default for Next.js 13 and later).

### Documentation

- [Next.js Link Component](https://nextjs.org/docs/api-reference/next/link)
- [Prefetching in Next.js](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#prefetching)

## Prefetching in React

In React, prefetching behavior is not built-in like in Next.js, but you can achieve similar functionality using libraries or custom hooks.

### Achieving Prefetching in React

1. **React Router**:
   - If you use React Router, you can manually implement prefetching using hooks and lazy loading.

   ```jsx
   import { Suspense, lazy, useEffect } from 'react';
   import { useLocation } from 'react-router-dom';

   const AboutPage = lazy(() => import('./AboutPage'));

   function App() {
     const location = useLocation();

     // Prefetch the About page when the user hovers over or focuses on a link
     useEffect(() => {
       if (location.pathname === '/') {
         import('./AboutPage');
       }
     }, [location]);

     return (
       <Suspense fallback={<div>Loading...</div>}>
         <AboutPage />
       </Suspense>
     );
   }
   ```

2. **React Query**:
   - Use libraries like [TanStack Query (React Query)](https://tanstack.com/query/latest) to manage and prefetch data.

   ```jsx
   import { useEffect } from 'react';
   import { useQuery, useQueryClient } from '@tanstack/react-query';

   function fetchAboutPageData() {
     return fetch('/api/about').then((res) => res.json());
   }

   function App() {
     const queryClient = useQueryClient();

     // Prefetch data for the About page
     useEffect(() => {
       queryClient.prefetchQuery({
         queryKey: ['aboutData'],
         queryFn: fetchAboutPageData
       });
     }, [queryClient]);

     return <div>Your App</div>;
   }
   ```

### Documentation

- [React Router](https://reactrouter.com/)
- [TanStack Query (React Query)](https://tanstack.com/query/latest)

Implementing prefetching can significantly enhance the performance and user experience of your web applications.


# Question : In backend the middle-ware needs req, res, error, and next (error is optional) here in Next.js we only give request, why ?

You're correct that in some backend frameworks, like Express.js, middleware functions typically take `req`, `res`, `next`, and sometimes `err` for error handling. In Express, middleware functions generally look like this:

```javascript
function middleware(req, res, next) {
  // Logic goes here
  next(); // Move to the next middleware
}
```

However, **Next.js middleware** works differently. It's not the same as Express-style middleware. In Next.js, the middleware function operates at a lower level and doesn't use `req`, `res`, or `next` like traditional server-side frameworks. Instead, it uses `NextRequest` and `NextResponse`.

### For Express.js:
If you're using **Express.js** or a similar framework, the correct format for middleware should be:

```javascript
function middleware(req, res, next) {
    try {
        // Your middleware logic
        next(); // Call next to proceed
    } catch (error) {
        next(error); // Pass error to error-handling middleware
    }
}
```

### For **Next.js Middleware**:
If you are working with **Next.js** middleware, you should follow its structure. Next.js doesn't pass `req`, `res`, `next`, or `err` directly like Express. Instead, you work with `NextRequest` and `NextResponse`, as shown below:

```typescript
import { NextRequest, NextResponse } from 'next/server';

export function middleware(request: NextRequest) {
    // Example: redirect if user is not authenticated
    const response = NextResponse.next();
    
    // Return the response (Next.js handles routing for you)
    return response;
}
```

### Summary:

- **Express.js**: Middleware expects `req`, `res`, `next`, and optionally `error`.
- **Next.js**: Middleware only takes `NextRequest`, and you handle the response by returning `NextResponse` without `req`, `res`, or `next`.

Each framework has its own middleware structure, and it’s important to use the correct pattern for each one.




# Handling API Requests in Next.js: A Comprehensive Guide

In modern web development, handling different types of HTTP requests efficiently is crucial. This article explores how to manage GET and POST requests in a Next.js API route, with a focus on username verification.

## The Legacy Approach

In the past, particularly with the Pages Router in Next.js, it was common to see code that checked the request method within a single handler:

```javascript
if(request.method !== "GET"){ 
    return Response.json( 
        { 
            success: false, 
            message : "This Method Is Not Allowed !!", 
        }, 
        { 
            status: 405, 
        } 
    ) 
}
```

However, this approach is no longer recommended in newer Next.js versions, especially with the App Router. GET and POST requests are typically handled separately for better organization and clarity.
A Modern Approach: Unified Request Handling
For scenarios where you need to handle multiple request types in a single function, here's a more comprehensive approach:

```javascript
export async function handleRequest(request: Request) { 
    const method = request.method;  
    if (method === "POST") { 
        return Response.json( 
            { 
                success: false, 
                message: "This Method Is Not Allowed !!", 
            }, 
            { 
                status: 405, 
            } 
        ); 
    } 
 
    if (method === "GET") { 
        await dbConnect(); 
        try { 
            const { searchParams } = new URL(request.url); 
            const queryParam = { username: searchParams.get("username") }; 
 
            const result = UserNameQueryShcema.safeParse(queryParam); 
 
            if (!result.success) { 
                const usernameErrors = result.error.format().username?._errors || []; 
                return Response.json( 
                    { 
                        success: false, 
                        message: usernameErrors.length > 0 
                            ? usernameErrors.join(", ") 
                            : "Invalid query parameters", 
                    }, 
                    { status: 400 } 
                ); 
            } 
 
            const { username } = result.data; 
            const existingUserVerified = await UserModel.findOne({ 
                username, 
                isVerified: true, 
            }); 
 
            if (existingUserVerified) { 
                return Response.json( 
                    { 
                        success: false, 
                        message: "Username already exists and is Verified, Please try another username !!", 
                    }, 
                    { status: 401 } 
                ); 
            } 
 
            return Response.json( 
                { 
                    success: true, 
                    message: "Username is unique", 
                }, 
                { status: 200 } 
            ); 
        } catch (err) { 
            console.log("There was an Error Checking the UserName", err); 
            return Response.json( 
                { 
                    success: false, 
                    message: "Something went wrong", 
                }, 
                { status: 500 } 
            ); 
        } 
    } 
}
```

This function handles both GET and POST requests:

It first checks the request method.
For POST requests, it returns a "Method Not Allowed" response.
For GET requests, it performs username verification:

Connects to the database
Parses and validates the username from the query parameters
Checks if the username already exists and is verified
Returns appropriate responses based on the results



Key Features

Method Differentiation: The function distinguishes between GET and POST requests, allowing for method-specific handling.

Error Handling: It includes comprehensive error handling, including validation errors and database errors.

## Conclusion (TLDR)
This would work in old system in case of pages router (legacy system) but after updation it doesen't work.


# HTTP METHODS : 

1. **OPTIONS**:
   - **Scenario**: You’re at a restaurant and you want to know what dishes the chef can prepare. You ask the waiter about the available options (methods).
   - **HTTP Equivalent**: An OPTIONS request helps you understand what methods (e.g., GET, POST) are allowed for a particular resource.

2. **GET**:
   - **Scenario**: You decide what to order based on the menu. You ask for the details of a dish (e.g., the description and price).
   - **HTTP Equivalent**: A GET request fetches the details of a resource without changing anything.

3. **POST**:
   - **Scenario**: You place an order for a new dish. You’re adding something new to the menu.
   - **HTTP Equivalent**: A POST request submits data to create a new resource.

4. **PUT**:
   - **Scenario**: You don’t like the description of the dish you ordered, so you ask the waiter to update the entire description.
   - **HTTP Equivalent**: A PUT request replaces the entire resource with the provided data.

5. **PATCH**:
   - **Scenario**: You want to change just the price of the dish you ordered without altering its description.
   - **HTTP Equivalent**: A PATCH request updates only specific parts of a resource.

6. **DELETE**:
   - **Scenario**: You decide to remove a dish from the menu entirely.
   - **HTTP Equivalent**: A DELETE request removes a specified resource.

7. **HEAD**:
   - **Scenario**: You want to check if the dish you ordered is still available, but you don’t need all the details—just the fact that it’s still on the menu.
   - **HTTP Equivalent**: A HEAD request checks the headers (metadata) of a resource without fetching the full data.

8. **TRACE**:
   - **Scenario**: You suspect that someone might be altering your orders, so you ask to see exactly what the waiter wrote down.
   - **HTTP Equivalent**: A TRACE request echoes back the received request, useful for debugging.

9. **CONNECT**:
   - **Scenario**: You want a private room in the restaurant where you can discuss sensitive matters without anyone listening in.
   - **HTTP Equivalent**: A CONNECT request establishes a tunnel for private, encrypted communication, like setting up an SSL connection.


In Mongoose, which is an Object Data Modeling (ODM) library for MongoDB and Node.js, the `.populate()` method is used to automatically replace the specified field(s) with the documents from other collections.

# What `.populate()` Does

- **Joins Documents**: It allows you to perform a join-like operation between collections. For example, if you have a reference to another document in a field, `.populate()` will fetch the referenced document(s) and include them in the query result.

- **References**: It is used when you have a reference (or ObjectId) to another document and want to retrieve the details of that document along with your main document.

### Example Scenario

Consider a simple scenario where you have two collections: `User` and `Message`. Each `User` document might have a reference to `Message` documents in a `messages` field.

**User Model:**
```javascript
const userSchema = new mongoose.Schema({
    name: String,
    messages: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Message' }]
});

const User = mongoose.model('User', userSchema);
```

**Message Model:**
```javascript
const messageSchema = new mongoose.Schema({
    content: String,
    timestamp: Date
});

const Message = mongoose.model('Message', messageSchema);
```

When you query a `User` document and use `.populate('messages')`, it will replace the `messages` field (which contains ObjectIds) with the actual `Message` documents:

```javascript
User.findById(userId).populate('messages').exec((err, user) => {
    if (err) {
        console.error(err);
        return;
    }
    console.log(user);
});
```

### Result

Without `.populate()`, the `user` object might look like this:
```json
{
    "_id": "userId",
    "name": "John Doe",
    "messages": ["messageId1", "messageId2"]
}
```

With `.populate('messages')`, it will look like this:
```json
{
    "_id": "userId",
    "name": "John Doe",
    "messages": [
        {
            "_id": "messageId1",
            "content": "Hello!",
            "timestamp": "2024-09-01T12:00:00Z"
        },
        {
            "_id": "messageId2",
            "content": "Goodbye!",
            "timestamp": "2024-09-02T12:00:00Z"
        }
    ]
}
```

### Summary

- **`.populate()`** is used in Mongoose to replace ObjectId references in documents with the actual documents from another collection.
- It is helpful for joining related documents and simplifying queries that involve relationships between collections.
