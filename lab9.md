app
```jsx
import React from "react";
import { Routes, Route, NavLink } from "react-router-dom";
import Home from "./Home.jsx";
import About from "./About.jsx";
import Contact from "./Contact.jsx";
function App() {
  const linkStyle = ({ isActive }) => ({
    margin: "0 15px",
    textDecoration: "none",
    color: isActive ? "blue" : "black",
    fontWeight: isActive ? "bold" : "normal",
  });
  return (
    <div>
      <nav>
        <NavLink to="/" style={linkStyle} end>Home</NavLink>
        <NavLink to="/about" style={linkStyle}>About</NavLink>
        <NavLink to="/contact" style={linkStyle}>Contact</NavLink>
      </nav>
      <hr />
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>
    </div>
  );
}
export default App;
```

Home
```jsx
import React from 'react';
function Home() {
    return <h2>Home Page</h2>
}
export default Home;
```

About
```jsx
import React from 'react';
function About() {
    return <h2>About Page</h2>;
}
export default About;
```

Contact
```jsx
import React from 'react';
function Contact() {
    return <h2>Contact Page</h2>
}
export default Contact;
```

main
```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import {BrowserRouter} from 'react-router-dom';
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