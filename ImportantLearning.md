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
