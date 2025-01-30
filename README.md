# Adding Bootstrap to a Vite/React App

To include Bootstrap in your Vite/React project, install it via npm:

```sh
npm install bootstrap
```

Then, modify `main.jsx` to import Bootstrap’s styles:

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App'
import 'bootstrap/dist/css/bootstrap.min.css' // Import Bootstrap styles

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

---

### Adding Bootstrap Icons

To add [Bootstrap Icons](https://icons.getbootstrap.com/), install the package:

```sh
npm install bootstrap-icons
```

Then, modify `main.jsx` to include the icons:

```jsx
import 'bootstrap-icons/font/bootstrap-icons.css' // Import Bootstrap Icons
```

So your final `main.jsx` should look like:

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App'
import 'bootstrap/dist/css/bootstrap.min.css' // Import Bootstrap styles
import 'bootstrap-icons/font/bootstrap-icons.css' // Import Bootstrap Icons

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

Wherever you want to use an icon, simply copy and paste the `<i>` font tag from the [icon library](https://icons.getbootstrap.com/) into your component.

```html
<i class="bi bi-arrow-through-heart-fill"></i>
```

---

### Overriding Bootstrap with Custom SCSS

If you want to customize Bootstrap (e.g., change the `$primary` color), you need to use SCSS. First, install `sass`:

```sh
npm install sass
```

Then, create a `src/styles/custom.scss` file and override Bootstrap variables **before** importing Bootstrap:

```scss
// src/styles/custom.scss

// Override Bootstrap variables before importing Bootstrap
$primary: #ff5733; // Example: Change primary color to orange-red

// Import Bootstrap after variables
@import 'bootstrap/scss/bootstrap';
```

Finally, update `main.jsx` to import the custom SCSS file instead of the default Bootstrap CSS:

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App'
import './styles/custom.scss' // Import customized Bootstrap styles
import 'bootstrap-icons/font/bootstrap-icons.css' // Import Bootstrap Icons

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

Now, your app will use the customized Bootstrap theme with Bootstrap Icons included.
