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


### Add a safe owner check (optional chaining `?` prevents crashes)

```jsx
const isOwner = hoot.author?._id === props.user?._id
```


### Wrap the html in a Bootstrap layout (container → card → card-body)

```jsx
  return (
  /* start bootstrap channges */
    <main className="container my-5">
      <div className="card shadow-sm">
        <div class="card-body">
  {/*  end bootstrap changes - CLOSE YOUR <div> TAGS DOWN BELOW! */}

      <header>
        <p>{hoot.category.toUpperCase()}</p>
        <h1>{hoot.title}</h1>
        <p>
          {hoot.author.username} posted on {new Date(hoot.createdAt).toLocaleDateString()}
        </p>
        {/* DELETE BUTTON */}
        {hoot.author._id === props.user._id && (
          <>
            <Link to={`/hoots/${hootId}/edit`}>Edit</Link>
            <button onClick={() => props.handleDeleteHoot(hootId)}>Delete</button>
          </>
        )}
      </header>
      <h2>Comments</h2>
      <CommentForm handleAddComment={handleAddComment} />
       {!hoot.comments.length && <p>There are no comments.</p>}

        {hoot.comments.map((comment) => (
          <p key={comment._id}>{comment.text}</p>
        ))}

  {/*  CLOSE YOUR <div> TAGS HERE! */}
          </div>
        </div>
    </main>
  )
```

<img width="1920" height="1080" alt="Screenshot 2025-08-13 at 11 26 46 AM (2)" src="https://github.com/user-attachments/assets/e6eefea1-fa93-4276-baf6-100342a16490" />


### Style the header 

Add new classNames to the `<p>` tags and `<h1>` tag:

```jsx
      <header>
        <p className="text-muted mb-1">{hoot.category.toUpperCase()}</p>
        <h1 className="card-title">{hoot.title}</h1>
        <p className="text-secondary mb-3">
          {hoot.author.username} posted on {new Date(hoot.createdAt).toLocaleDateString()}
        </p>
```

<img width="612" height="234" alt="Screenshot 2025-08-13 at 11 30 54 AM" src="https://github.com/user-attachments/assets/109fe289-678c-4857-81f4-561cdcdb5d38" />

---

### Add Bootstrap button classes to the Edit and Delete

Wrap the `<Link>` and `<button>` in a new `<div>` - give them all the new classNames listed below:

```jsx
        {hoot.author._id === props.user._id && (
          <div className="d-flex justify-content-center gap-2 mb-4">
            <Link className="btn btn-warning btn-sm" to={`/hoots/${hootId}/edit`}>Edit</Link>
            <button className="btn btn-danger btn-sm" onClick={() => props.handleDeleteHoot(hootId)}>Delete</button>
          </div>
```

<img width="828" height="328" alt="Screenshot 2025-08-13 at 11 35 45 AM" src="https://github.com/user-attachments/assets/4f0cb234-768a-48d2-8a5a-5fdd9cbe88fd" />

---

### Keep the form; add a clearer section title

```diff
- <h2>Comments</h2>
+ <h4 className="mb-3">Comments</h4>
  <CommentForm handleAddComment={handleAddComment} />
```

---

### Improve empty state + render comments as a list group

```diff
- {!hoot.comments.length && <p>There are no comments.</p>}
-
- {hoot.comments.map((comment) => (
-   <p key={comment._id}>{comment.text}</p>
- ))}
+ {!hoot.comments?.length && (
+   <p className="text-muted mt-3">There are no comments.</p>
+ )}
+ {hoot.comments?.length > 0 && (
+   <ul className="list-group mt-3">
+     {hoot.comments.map((comment) => (
+       <li key={comment._id} className="list-group-item">
+         {comment.text}
+       </li>
+     ))}
+   </ul>
+ )}
```

---

### Result



