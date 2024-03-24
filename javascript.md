## JavaScript
### Object
```js
let ta={
    firstname:"Alice",
    lastname:"Smith",
    age:24
};

console.log(Object.keys(ta));
//["firstname","lastname","age"]
```
json:
```js
{
    "firstname":"Alice",
    "lastname":"Smith",
    "age":24
}
```
### Array
```js
let a = [];
a.push(17);
a.pop;
```
### Looping
```js
for(let i = 0; i < 10; i++){}
for(let attr in course){} //loop through object properties(keys)
for(let item of array){}  //loop through array contents
```
### Function
```js 
function fToC(temp){
    return (temp-32)*5/9;
}

const fToC =function(temp){
    return (temp-32)*5/9;
}

const fToC = (temp)=>{
    return (temp-32)*5/9;
}  //anonymous function

const fToC = (temp)=>(temp-32)*5/9;
```

### Manipulating the DOM
```js
let title = document.getElementById("articalTitle");
let loginBtn = document.getElementsByName("login")[0]
let callouts = document.getElementsByClassName("login")[0]

loginBtn.addEventListener("click",()=>{
    alert("You're advancing to the next part of the website.");
});
```
### JSON
- `JSON.parse` JSON string->JS object
- `Json.stringify` JS object->JSON string
```js
const myObj = JSON.parse('{"name":"Cole","age":"15"}');
const myStr = JSON.stringify(myObj);
```

### Request for JSON
- Request can be *synchronous* or *asynchronous*
- Asynchronous requests are recommended as they are non-blocking. Typically, they use a callback when the data is received and lets the browser continue its work while the request is made.
Two key methods: `XMLHttpRequest` (old) and `fetch` (new). `fetch` is a promise-based method.  
`Promise` objects represent the eventual completion/failure of an *asynchronous* operation and its resulting value.

```js
fetch(url,{
    //method:"GET"
    headers:{
        "X-CS571-ID":CS571.getBadgerId()
    }
})
    .then((res)=>res.json)
    .then((data)=>{
        //do something with data
    })
    .catch(error=>console.error(error))

```
callback function:functions passed in a function

### Decalarative vs Imperative programming
Declarative array functions include  `forEach`,`map`,`slice`,`concat`,`filter`,`some`,`every` and `reduce`
#### `forEach`
```js
["Bessy","Rob", "Bartholomew"].forEach(name =>{
    if name.length > 5{
        console.log(`${name} is a long name`);
    }
    else{
        console.log(`${name} is a short name`);
    }
})
```
#### `filter`
```js
const shortNames = ["Bessy","Rob", "Bartholomew"].filter(name => name.length<=5);
const longNames = ["Bessy","Rob", "Bartholomew"].filter(name => name.length>5);
//judge if the return value of the function passed in the filter function is true or false.
```
#### `map`
```js
const nameLengths = ["Bessy","Rob", "Bartholomew"].map(name => name.length);
```

#### `slice` and `concat`
`slice` returns a shallow copy.
```js
["apple","banana","coconut","dragonfruit"].slice(1,3);
//["banana","coconut"]
["apple"].concat(["banana","coconut","dragonfruit"]);
//["apple","banana","coconut","dragonfruit"]
```

#### `some` and `every`
`some()` returns `true` if the callback returns true for *some* element of the array, `false` otherwise.
`every()` returns `true` if the callback returns true for *every* element of the array, `false` otherwise.
```js
["sam","jacob","jess"].some(p=>p==="jess");//true
["sam","jacob","jess"].every(p=>p==="jess");//false
```

#### `reduce`
`reduce` takes a 2-parameter callback (previous and current values) and a start value.
```js
[2,4,-1.1,7.2].reduce((prev,curr)=>prev+curr,1.2);//13.3
```
#### Chaining Declarative Functions
```js
const shortNames = ["Bessy","Rob", "Bartholomew"]
    .filter(name => name.length<=5)
    .map(name => name.length);
```

### Other Async Functions
- `setInterval(callback,interval)` perform a callback function every interval milliseconds.
- `setTimeout(callback,timeout)` perform a callback function in timeout milliseconds.

### `...` Spread Operator
```js
const cats = ["apricat","barnaby","bucky","colby"];
const newCats = [...cats,"darcy"]//["apricat","barnaby","bucky","colby","darcy"]

const defs={}
```
4512
### Vocabulary
- imperative 表示命令的,祈使的;重要紧急的；迫切的；急需处理的
- declarative 陈述的
- imperative programming 命令式编程
- declarative programming 声明式编程
- cumbersome 大而笨重的;冗长的,累赘的,复杂的


### Spread Operator
```js
const defs = {
    erf:"a plot of land",
    popple:"turbulent seas"
};

const newDefs={
    ...defs,
    futz:"waste of time"  
};
```

### `??` Null Coalescing Operator
if left-hand is `null` or `undefined`,use right-hand.
```js
const IS_ENABLED = env.IS_ENABLED?? true;
const USERNAME=document.getElementById("username").value ?? "";

const IS_ENABLED = env.IS_ENABLED?env.IS_ENABLED:true;//always true!
```

### Copys
#### Reference Copy
```js
let MyBasket = {
    basketId: 154,
    items: ["apples","bananas","grapes"];
let myRefCopyBasket = myBasket;
myRefCopyBasket.basketId = 999;
myRefCopyBasket.items.push("Zucchnis");

console.log(myBasket);
console.log(myRefCopyBasket);
}
```

#### Shallow Copy
```js
let  myBasket = {
    basketId: 154,
    items: ["apples","bananas","grapes"];
let myShallowCopyBasket = {...myBasket};
myShallowCopyBasket.basketId = 999;
myShallowCopyBasket.item.push("Zucchnis");

console.log(myBasket);
console.log(myShallowCopyBasket);
}
```
#### Deep Copy
```js
let  myBasket = {
    basketId: 154,
    items: ["apples","bananas","grapes"];
let myDeepCopyBasket = JSON.parse(JSON.stringify(myBasket));
myDeepCopyBasket.basketId = 999;
myDeepCopyBasket.item.push("Zucchnis");

console.log(myBasket);
console.log(mmyDeepCopyBasket);
}
```