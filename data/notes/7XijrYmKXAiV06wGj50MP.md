
Web components allow you to create custom reusable and encapuslated HTML tags to be used in web pages and apps. They are capable of isolating CSS and JavaScript similar to `<iframe>` - known as a **shadown DOM**. These are framework agnostic and are supported by most modern browsers.

Example:

```JavaScript
// CREATE
class MyButton extends HTMLElement {...}
window.customElements.define('my-button', MyButton);

// USE
<my-button></my-button>
```

### Web Components vs React

According to [React documentation](https://reactjs.org/docs/web-components.html#:~:text=React%20and%20Web%20Components%20are,The%20two%20goals%20are%20complementary.), Web Components and React solve different problems. React is a declarative JS library to address state management and web app "reactivity". Web components exist to address reusability and encapsulation of HTML elements. React components can only be used in React, where as web components can be used anywhere e.g. across different libraries - Vue, React, Angular etc.
