app
```jsx
import React,{useState} from "react";
import "./index.css";

export default function App(){
  const [tasks,set]=useState([]);
  const [filter,setF]=useState("all");
  const [f,setForm]=useState({name:"",date:"",desc:""});

  const add=(e)=>{
    e.preventDefault();
    if(f.name&&f.date){
      set([...tasks,{...f,done:false}]);
      setForm({name:"",date:"",desc:""});
    }
  };

  const toggle=(i)=>{
    set(tasks.map((t,j)=>j===i?{...t,done:!t.done}:t));
  };

  return(
    <div className="app">
      <h1>Reminder App</h1>

      <form onSubmit={add}>
        {["name","date","desc"].map(k=>(
          <input
            key={k}
            type={k==="date"?"date":"text"}
            placeholder={k}
            value={f[k]}
            onChange={e=>setForm({...f,[k]:e.target.value})}
          />
        ))}
        <button>Add</button>
      </form>

      <div className="filters">
        {["all","done","notdone"].map(v=>(
          <button key={v} onClick={()=>setF(v)}>{v}</button>
        ))}
      </div>

      <ul>
        {tasks
          .filter(t =>
            filter==="all"
              ? true
              : filter==="done"
              ? t.done
              : !t.done
          )
          .map((t,i)=>(
            <li key={i} onClick={()=>toggle(i)} className={t.done?"done":""}>
              <b>{t.name}</b> - {t.date} {t.desc && `| ${t.desc}`}
            </li>
        ))}
      </ul>
    </div>
  );
}
```

index
```css
.app {
  max-width: 400px;
  margin: auto;
  font-family: sans-serif;
}

form, .filters {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-bottom: 1rem;
}

input, button {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  padding: 8px;
  border-bottom: 1px solid #eee;
  cursor: pointer;
}

.done {
  text-decoration: line-through;
  color: gray; 
}
```

app
```jsx
#root {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
  text-align: center;
}

.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;

}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.react:hover {
  filter: drop-shadow(0 0 2em #61dafbaa);
}

@keyframes logo-spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

@media (prefers-reduced-motion: no-preference) {
  a:nth-of-type(2) .logo {
    animation: logo-spin infinite 20s linear;
    -webkit-animation: logo-spin infinite 20s linear;
}
}

@media (prefers-reduced-motion: no-preference) {
}
.card {
  padding: 2em;

}

.read-the-docs {
  color: #888;
  
}
```

main
```jsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>,
)
```