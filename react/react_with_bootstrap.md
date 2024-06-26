## React
### Components
React components can have props given by its parent.
```jsx
function App(){
    return(
        <div>
         <Welcome person="Charlie"></Welcome>
         <Welcome person="Jessica"></Welcome>
         <Welcome person="Tonya"></Welcome>
        </div>
    )
}
function Welcome(props){
    return <h1>Welcome, {props.person}</h1>
}
```
or can maintain an internal state.
```jsx
function App(){
    return <Welcome message="Good evening, "></Welcome>
}

function Welcome(props){
    const [name,setName] = useState("Rodriguez")
    return <h1>{props.message} {name}</h1>
}
```
### `{}`
Curly braces `{}` interpolate a JS expression.
```jsx
<div>
 <h2>{name}</h2>
 <a href={url} target="_blank">My Website</a>
 {
    classes.map(clazz=>
     <div.key={clazz.name}>
      <p>{clazz.name} is worth {clazz.creds} credits</p>
    </div>
      )
 } 
</div>
```
### `useState` Hook
```jsx
const [name,setName]= useState("James");
console.log(name);
setName("Jim");
console.log(name);//still James?
```
`setName` happens asynchronously.
The mutator can be called like
```jsx
setName("Jim");
```
or with a callback function of the previous value.
```jsx
setName(oldName=>oldName.substring(0,oldName.length-1))
```
We cannot do `push`
```jsx
const [names,setNames]= useState(["James"])
setNames((oldNames)=>[...oldNames,"Jim"]);
```
### useEffect Hook
Used to perform an action on component load or state change.
```jsx
useEffect(()=>{
    alert("the page has been reloaded");
},[])
useEffect(()=>{
    alert("You change your name to"+name);
},[name])
```
It takes a callback function and an array of state dependencies as arguments.  
Empty array means whenever the page loads.
### Imports and Exports
Functions must be exported to be used in other files
```jsx
export default FindMyBadgers;
```
This can then be imported,e.g.
```jsx
import FindMyBadgers from "./components/FindMyBadgers";

import {Card,Button} from "react-bootstrap";
```

### Example1
```jsx
import {Card,Button} from "react-bootstrap";

function Badger(props){
    return <Card style={{margin: "0.5rem"}}>
        <h2>{props.name}</h2>
        <p>{props.email}<p>
        <Button>Say Name!!</Button>
    </Card>
}

export default Badger;
```
```jsx
import {useState} from "react";
import Badger from "./Badger";

function FindMyBadgers(){ 
    return <div>
        <h1>Find My Badgers</h1>
        <Badger name="Bucky" email="Bucky@wisc.edu"></Badger>
        <Badger name="Pete" email="Pete@wisc.edu"></Badger>
        </div>
}
export default FindMyBadgers;
```
change the hard-coded style of programming
```jsx
import {useState} from "react";
import Badger from "./Badger";

function FindMyBadgers(){
    const [badgers,setBadgers] = useState([{
        name:"Bucky",
        email:"Bucky@wisc.edu"
    },
    {
        name:"Pete",
        email:"pete@wisc.edu"
    }])
    return <div>
        <h1>Find My Badgers</h1>
        {
            badgers.map(badger=><Badger name={badger.name} email={badger.email}></Badger>)
        }
        </div>
}
export default FindMyBadgers;
```
### Infinite Loop
```jsx
import {useState,useEffect} from "react";
import Badger from "./Badger";
function FindMyBadgers(){
    const [badgers,setBadgers] = useState([{
        name:"Bucky",
        email:"Bucky@wisc.edu"
    },
    {
        name:"Pete",
        email:"pete@wisc.edu"
    }])

    //useEffect(()=>{
        .fetch 
            .then(res=>res.json())
            .then((data)=>{
                setBadgers(data.results)
            })
    //},[])

    return <div>
        <h1>Find My Badgers</h1>
        {
            badgers.map(badger=><Badger name={badger.name} email={badger.email}></Badger>)
        }
        </div>
}
```
`useEffect` is going to run this function once on page load and not again.
### Improvement
```jsx
import {Card,Button} from "react-bootstrap";

function Badger(props){

    const [isHovering, setIsHovering] = useState(false);

    function handleClick(){
        alert("Your name is " + props.name)
    }

    return <Card style={{margin: "0.5rem"}}>
        <h2>{props.name}</h2>
        <p>{props.email}<p>
        <Button
            variant={isHovering? "primary" : "success"}
            onClick={handleClick}
            onMouseOver={()=>{setIsHovering(true)}}
            onMouseLeave={()=>{setIsHovering(false)}}
            >Say Name!!</Button>
    </Card>
}

export default Badger;
```
### Example2
bad example below
```jsx
export default function Counter(){
    const [number, setNumber] = useState(0)
    return <div>
        <h1>{number}</h1>
        <button onClick={() => {
            setNumber(n+1);
            setNumber(n+1);
            setNumber(n+1);//when executing this, React will only execute the last setNumber function.
        }}>+3</button>
        </div>
}
```
revised version
```jsx
export default function Counter(){
    const [number, setNumber] = useState(0);
    return <div>
        <h1>{number}</h1>
        <button onClick={() => {
            setNumber(n=>n+1);
            setNumber(n=>n+1);
            setNumber(n=>n+1);//the callback function guarantees that n is going to be the old state and n+1 will be the new state.
        }}>+3</button>
        </div>
}
```
### React `key` Prop
The `key` prop is used by React to speed up rendering.
- Always use a unique key for *parent-most* element rendered in a list.
- This key needs to be *unique among siblings*.
- This key should *usually* not be the index of the item.(what if the order changes?)
### Example 3
```jsx
function AllHurricanes(){
    const [Hurricanes, setHurricanes] = useState([])
    useEffect(()=>{
        fetch("https://cs571.org/api/f23/weekly/week05",{
            headers:{
                "X-CS571_ID": CS571.getBadgerId() 
            }
        }).then(res=>res.json())
        .then(data =>{
                setHurricanes(data)
        })
    },[])

    return <div>
        <h1>Hurricane Finder</h1>
        {
            hurricanes.map(hurr=><Hurricane key={props.id}/>)//you can't access key using props.key
        }
}
```
```jsx
export default function Hurricane(props){
    const startDate = new Date(props.start_date)//not really a state variable.it's not tracking anything.
    const endDate = new Date(props.end_date)
    return <div>
        <h2>{props.name}</h2>
        <p>Category {props.category} {{prop.wind_speed}mph}</p>
        <p>Started on {startDate.toLocaleDateString()} at {startDate.toLocaleTimeString()}</p>
        <p>Ended on {endDate.toLocaleDateString()} at {endDate.toLocaleTimeString()}
    </div>
}
```
with react-bootstrap
```jsx
function AllHurricanes(){
    const [Hurricanes, setHurricanes] = useState([])
    useEffect(()=>{
        fetch("https://cs571.org/api/f23/weekly/week05",{
            headers:{
                "X-CS571_ID": CS571.getBadgerId() 
            }
        }).then(res=>res.json())
        .then(data =>{
                setHurricanes(data)
        })
    },[])

    return <div>
        <h1>Hurricane Finder</h1>
        <Container>
            <Row>
            {
            hurricanes.map(hurr=><Col key={props.id} xs={12} md={6} lg={4}><Hurricane/></Col>)//use the key for the parent-most element
            }
            </Row>
}
```
### Pagination (in react-bootstrap)
```jsx
{
    bigData.slice((page - 1)*16,page*16).map(name=><p>{name}</p>)
}
<Pagination>
    <Pagination.Item active={page === 1} onClick={()=>setPage(1)}>1</Pagination.Item>
    <Pagination.Item active={page === 2} onClick={()=>setPage(2)}>2</Pagination.Item>
    <Pagination.Item active={page === 3} onClick={()=>setPage(3)}>3</Pagination.Item>
    <Pagination.Item active={page === 4} onClick={()=>setPage(4)}>4</Pagination.Item>
```
dynamic version
```jsx
const buildPaginator = () = > {
    let pages = [];
    const num_pages = Math.ceil(hurricanes.length / 6);
    for(let i = 1; i <= num_pages; i++){
        pages.push(
            <Pagination.Item
                key={i}
                active={activePage === i}
                onClick={()=>setActivePage(i)}>
                {i}
                </Pagination.Item>
        )
    }
    return pages;
}
//the following code is just an unfinished demo.
<Pagination>
    {buildPaginator()}
</Pagination>

```
### Note on Hot Reloading
React(Vite) will keep your old state when hot reloading.The prior solution will result in duplicates upon saving your solution.

### Handling Text Input
We can get user input using the HTML `input` tag or the React-Bootstrap `Form.Control` component.
We can get user input
- in a controlled way using its `value` and tracking onChange events
- in an uncontrolled manner using `useRef`
```jsx
const [sum,setSum]=useState(0);
const [inputVal,setInputVal]=useState('')

function addVal(){
    setSum((prev)=>parseInt(inputVal));
    return(
        <div>
            <label htmlFor="myInput">Add a number here!</label>
            <input
                id="myInput">
                value={inputVal}
                onChange={(e)=>setInputVal(e.target.value)}
            />
            <button onClick={addVal}>Add</button>
            <p>The total sum is: {sum}</p>
        </div>
    );
}
```
```jsx
<Form.Label htmlFor="name">Name</Form.Label>
<Form.Control value={title} onChange={(e)=>setTitle(e.target.value)} id="name"></Form.Control>
```
### React Fragments
Sometimes we use `<></>` instead of `<div></div>`.  
`<></>` is a React Fragment, a virtual seperator not represented in the real DOM.  
When we want to add style to the block, you should use `<div></div>`.
### State Management in React
#### Passing Callbacks
The original way to do child-to parent communication.
```jsx
const TodoList = (props) =>{
    const [items,setItems] = useState();
    const removeItem = (itemId) =>{
        //Do Remove!
    }

    return <div>
    {
        items.map(it=><TodoItem key={it.id} {...it} >)
    }
}
```
```jsx
const TodoItem = (props)=>{
    const handleRemove = ()=>{
        alert("Removing TODO item!");
        props.remove(props.id);
    }

    return <Card>
        <h2>{props.name}</h2>
        <Button onClick={handleremove}>Remove Task</Button>
        </Card>
}
```
#### Example
Ticket.jsx
```jsx
import { Button, Card } from "react-bootstrap";

const Ticket = (props) => {

    const markTodo = () => {
        props.move(props.status, "todo", props.id)
    }

    const markInProgress = () => {
        props.move(props.status, "inprogress", props.id)
    }

    const markDone = () => {
        props.move(props.status, "done", props.id)
    }

    return <Card style={{margin: "0.25rem"}}>
        <h2 style={{fontSize: "1.25rem"}}>{props.name}</h2>
        <p>{props.description}</p>
        <Button variant="secondary" onClick={markTodo}>todo</Button>
        <Button variant="primary" onClick={markInProgress}>in progress</Button>
        <Button variant="success" onClick={markDone}>done</Button>
    </Card>
}

export default Ticket;
```
TicketLane.jsx
```jsx
import { Col, Row } from "react-bootstrap"
import Ticket from "./Ticket";

const TicketLane = (props) => {
    return <div>
        <Row>
            <h2>{props.status} tickets</h2>
            {
                props.tickets.length === 0 ? <p>There are no tickets here yet!</p> :
                props.tickets.map(tick => {
                    return <Col
                        xs={6}
                        md={4}
                        lg={3}
                        xxl={2}
                        key={tick.id}
                    >
                        <Ticket 
                            {...tick}
                            status={props.status}
                            move={props.move}
                        />
                    </Col>
                })
            }
        </Row>
        <br />
    </div>
}

export default TicketLane;
```
TicketBoard.jsx
```jsx
import { useEffect, useState } from "react";
import { Container } from "react-bootstrap";

import TicketLane from './TicketLane'

const TicketBoard = (props) => {

    const [ticketLanes, setTicketLanes] = useState({
        todo: [],
        inprogress: [],
        done: [],
    })

    useEffect(() => {
        fetch('https://cs571.org/api/f23/weekly/week06', {
            headers: {
                "X-CS571-ID": CS571.getBadgerId()
            }
        })
        .then(res => res.json())
        .then(ticketData => {
            console.log(ticketData);
            setTicketLanes({
                todo: ticketData,
                inprogress: [],
                done: []
            });
        })
    }, []);

    const move = (from, to, tickId) => {

        console.log(`Moving ${tickId} from lane ${from} to lane ${to}!`)

        if (from === to) {
            return;
        }

        setTicketLanes(oldLanes => {
            let fromLane = oldLanes[from].slice(); // shallow copy
            let toLane = oldLanes[to].slice(); // shallow copy
            
            const ticketToMove = fromLane.filter(tick => tick.id === tickId)[0]
            fromLane = fromLane.filter(tick => tick.id !== tickId);
            toLane = [...toLane, ticketToMove];

            return {
                ...oldLanes,
                [from]: fromLane,
                [to]: toLane
            }
        })
    }

    return <div>
        <h1>Ticketß Board</h1>
        <Container fluid>
            {
                Object.keys(ticketLanes).map(laneName => {
                    return <TicketLane
                        move={move}
                        key={laneName}
                        status={laneName}
                        tickets={ticketLanes[laneName]}
                    />
                })
            }
        </Container>
    </div>
}

export default TicketBoard;
```
### `useContext` Hook
A context must be exported.
```jsx
const MyDataContext = createContext([]);
export default MyDataContext;

function ParentComponent(){
    const [data, setData] = useState(["Apples", "Oranges"]);
    return (
        <MyDataContext.Provider value={data}>
            <SomeChildComponent/> 
            //some child component into which you want to pass some data.
        </MyDataContext.Provider>
    );
}
```
```jsx
function SomeChildComponent(){
    const data = useContext(MyDataContext);
    return(
        //some codes
    )
}
```
### Data Storage
|Type|Example|
|-|-|
|Cookies|`document.cookie = 'lang=en'`|
|Session|`sessionStorage.setItem('name','Cole')`|
|Local|`localStorage.getItem('lastLogin')`|
Caution:React re-renders when props changes or when state changes. It doesn't care about session storage or local storage at all.  
Instead, we have to explicitly tell the parent call the function that set or get the data in storage.
  
`sessionStorage` and `localStorage` only store strings! Use `JSON.parse` and `JSON.stringify`.
#### Incorrect Way
```jsx
sessionStorage.setItem('nums',[2,6,19]);
const storeNums = sessionStorage.getItem('nums');
```
#### Correct Way
```jsx
sessionStorage.setItem('nums',JSON.stringify([2,6,19]));
const storeNums = JSON.parse(sessionStorage.getItem('nums'));
```
#### Libraries
- Layout & Design: **React-Bootstrap**, Reactstrap,Material, Elemental, Semantic
- Routing & Navigation: **React Router**, React Navigation, React Location
- State Manegement:Redux, Recoil, MobX, XState
### Multi-Page Apps
#### Routing
```jsx
<BrowserRouter>
    <Routes>
        <Route path="/" element={<Layout />}>
            <Route path="about-us" element={<AboutUs />}/>
            <Route path="other-info" element={<OtherInfo />}/>
        </Route>
    </Routes>
</BrowserRouter>

function Home(){
    return <h2>Home</h2>
}

function AboutUs(){
    return <h2>About Us</h2>
}

function Home(){
    return <h2>Other Info</h2>
}
```
#### Browser `outlet`
`<Outlet/>` shows the component returned by the child route!
```jsx
function Layout(){
    return(
        <>
            <Navbar bg="dark" variant="dark">
                {...}
            </Navbar>
            <Outlet/>
        </>
    );
}
```
#### `useNavigate` Hook
```jsx
export default function OtherInfo(){
    
    const navigate = useNavigate();

    const handleClick = () =>{
        navigate('/home');
    }

    return <div>
        <h2>Other Info</h2>
        <Button onClick={handleClick}>Back to Home</Button>
        </div>
}
```
### CRUD Operations via HTTP
|CRUD Operation|HTTP Method|
|-|-|
|Create|POST|
|Read|GET|
|Update|PUT|
|Delete|DELETE|
PUT and POST requests have a request body.

### POST through Fetch
```jsx
fetch("https://example.com/create-content",{
    method:"POST",
    headers:{
        "Content-Type":"application/json"//must include this header
    }
    body:JSON.stringify({//must stringify
        content:"Hello World!"
    })
}).then(res=>{
    if(res.status === 409){
        alert("This content already exists!")
    }
    return res.json()
}).then(json=>{
    if(json.msg){
        alert(json.msg)
    }
});
```
### Uncontrolled components 
use the `useRef` Hook
```jsx
const inputVal = useRef();
return(
    <div>
        <label htmlFor="myInput">Type something</label>
        <input id="myInput" ref={inputVal}></input>
    </div>
);
```
The value of a ref can be retrieved via its `current` property, e.g.`inputVal.current.value`

### Cookies
```jsx 
fetch("https://example.com/create-content",{
    method:"POST",
    credentials:"include",
    headers:{
        "Content-Type":"application/json"
    }
    body:JSON.stringify({
        content:"Hello World!"
    })
    ...})
```
### Memoization
#### `useCallback` Hook
When re-rendering, it will not recreate this function unless something in the dependency array changed.
```jsx
function MyApp(){
    const myComplicatedFunction = useCallback(()=>{...}, []);
    ...
}
```
#### `useMemo Hook`
The same as `useCallback`, except memoizes the value of a callback function rather than the callback itself.
```jsx
function MyApp(){
    const myComplicatedValue = useMemo(()=>{...}, []);
    ...
}
```
#### `memo`
A pure component is something that does not have any state, it only displays what it's given.  
`memo` is used for creating purely functional components. Given the same props, the function renders the same output.  
```jsx
export default memo(GroceryList);
//It's only going to re-render if its props change.
export default memo(GroceryList,(prevprops,nextprops)=>{
    return prevProps.apples === nextProps.apples &&
        prevProps.bananas === nextProps.bananas;
})//if the callback funcion return true, the function won't re-render.
```
The child components are going to re-render if its parent changes, even if the props don't change. We can prevent that from happening if we do memoization.

### Custom Hooks
`useStorage` is a custom hook that changes the session storage at the same time the state changes.
```jsx
import {useState,useEffect} from 'react';
export default function useStorage(storageKey,initialValue){
    const savedData = JSON.parse(sessionStorage.getItem(storageKey));
    const [data,setData] = useState(savedData ? savedData : initialData);
    useEffect(()=>{
        sessionStorage.setItem(storageKey, JSON.stringify(data));
    },[storageKey,data]);
    return [data,setData];
} 
```
### Vocabulary
- malicious 恶意的
- interpolate 插入
- credentials 证书
- verbose 冗长的
