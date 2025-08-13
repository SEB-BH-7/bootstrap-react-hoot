<h1>
  <span class="prefix">Front-End UI</span>
  <br />
  <span class="headline">Add Bootstrap to Vite + Style a Detail Page</span>
</h1>

To include Bootstrap in your Vite/React project, install it via npm:

```sh
npm install bootstrap
```

Then, modify `main.jsx` to import Bootstrap’s styles and scripts:

```jsx
import { BrowserRouter } from 'react-router-dom'
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'

// Bootstrap
import 'bootstrap/dist/css/bootstrap.min.css'  // styles
import 'bootstrap'                             // JS (for components that need it)    

import './index.css'
import App from './App.jsx'



createRoot(document.getElementById('root')).render(
  <StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </StrictMode>,
)
```



## Sample Modifications

### Add a spinner where you show “Loading…”. For example, in any component:

   ```jsx
    // HootDetails.jsx
   
    // if (!hoot) return <main>Loading...</main>
    if (!hoot) {
    return (
      <main className="d-flex justify-content-center align-items-center" style={{ minHeight: '40vh' }}>
        <div className="spinner-border" role="status" aria-label="loading"></div>
      </main>
    )
    }
   ```

* Replace any plain “Loading…” text in your app with the spinner above.


<img width="1920" height="1080" alt="Screenshot 2025-08-13 at 11 02 42 AM (2)" src="https://github.com/user-attachments/assets/b4739707-ac91-44a2-9c58-d23256cca8aa" />

