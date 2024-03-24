## TypeScript
```typescript
let str = 'string'

let str:string = 'abc'

int numArr = [1,2,3]
const result = numArrat.find(item => item > 2) as number
result*5
```
types: `string`, `number`, `boolean`, `null` , `undefined`
```ts
let v1: string|null = null
let v2 1|2|3|4 = 2 //v2 can only be one of 1,2,3,4
```
### Arrays
```ts
let arr:number[]=[1,2,3]

let arr:Array<string>=['a','b','c']
```
### Tuples
```ts
let t1:[number,string,number?]=[1,'a','b']//the third element doesn't need to be a number.
```
### Function
```ts
function MyFn (a:number,b:string，c=114514):number{
    return 2
}
```
### Interface(object)
```ts
interface Obj{
    name: string,
    age: number
}

const obj:Obj={
    name:'a',
    age:10
}
```

### Type
```ts
type MyType = string|number
let a:MyUserName = 'abc'
```
### Generics
```ts
function myFn<T>(a:T,b:T):T[]{
    return [a,b]
}

myFn<number>(1,2)
myFn(1,2)
```