## [AstroJS Documentation](https://docs.astro.build/en/getting-started/)

## My Learnings :
 
 **Hydration Strategies** in Astro, they allow you to specify when and how your component should be rendered on the client side. Here's an explanation of each one:

1. **`client:idle`**:
   - This hydration strategy waits until the browser is **idle** to load the component. This means the browser will prioritize rendering the static content first, and only when it has spare processing power (i.e., when the page is fully loaded and the user isn’t interacting), will it load your component. 
   - Useful for non-essential components that don’t need to be interactive immediately.

2. **`client:load`**:
   - This tells Astro to load and hydrate the component as soon as the page **loads**. It's a good strategy for interactive components that the user might need right away, like a navbar or a dynamic footer. 
   - **Quick hydration**, but less performance efficient compared to the others.

3. **`client:media`**:
   - This one delays loading the component until a specified **media query** is matched. For example, you can set it to load only if the screen width is larger than 768px (for desktop views). You define the media query in the component.
   - Great for responsive design, loading only what's necessary based on device type or screen size.

4. **`client:visible`**:
   - This strategy waits until the component is actually **visible** in the viewport before it gets hydrated. It uses the **Intersection Observer API** to track when the component comes into view. This is useful for content further down the page, so that it only loads when the user scrolls to it.
   - Helps in optimizing performance by not loading everything at once.

5. **`client:only`**:
   - The component will **only** render on the client and will not be rendered statically. This is for components that don't make sense to pre-render on the server and only work on the client (e.g., those heavily dependent on browser APIs or dynamic data).
   - It's often used when you want a component to be completely client-rendered with no static fallback.

Each strategy helps you balance performance and interactivity based on the needs of your site.

