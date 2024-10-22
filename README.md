# play-typescript

My personal playground for typescript coding and learning.

## :pushpin: Summary
### Table of contents
- [TypeScript](#label-typescript)
- [Compiler options(tsconfig.json)](#label-compiler-options(tsconfig-json))
- [Types](#label-types)
- [Index signature](#label-index-signature)
- [Enum](#label-enum)
- [Any](#label-any)
- [Unknown](#label-unknown)
- [Void](#label-void)
- [Never](#label-never)
- [Type compatibility](#label-type-compatibility)
- [Algebraic type](#label-algebraic-type)
- [Type inference](#label-type-inference)
- [Type assertion](#label-type-assertion)
- [Type narrowing](#label-type-narrowing)
- [Discriminated union(tagged union)](#label-discriminated-union(tagged-union))
- [Function](#label-function)
- [Interface](#label-interface)

## :label: TypeScript
- TypeScript is a strongly typed programming language that builds on Javascript, giving you better tooling at any scale.
<br><br>

### Type system
- Static type system
   - Determine the variable type statically before executing the code.
   - Java
- Dynamical type system
   - Determine the variable type dynamically while executing the code.
   - Javascript 
- Gradual type system
   - Ensure type safety through pre-execution checks.
   - Automatically infer the type of variables.
   - Typescript
- Property-based type system
   - In other words, Structural type system.
   - A structural type system determines type equality based on the structure (i.e., properties and methods) of the type. 
   - Two types are considered interchangeable if they have the same structure, even if they have different names.
   - Typescript, Go, Scala
- Nominal type system
   - A nominal type system determines type equality based on the name of the type. 
   - That is, even if two types have the same structure, they are considered different types if their names are different.
   - Java, C#, C++
<br><br>

## :label: Compiler options(tsconfig.json)
```json
{
  "compilerOptions": {
    "target": "ESNext",
    "module": "ESNext",
    "outDir": "dist",
    "strict": false,
    "moduleDetection": "force",
    "skipLibCheck": true
  },
  "include": [
    "src"
  ]
}
```
- target
   - This specifies the ECMAScript version that the TypeScript compiler will target. 
   - ESNext refers to the latest ECMAScript standard available, ensuring that the code is compiled to use the newest JavaScript features.
<br><br>
- module
   - This determines how the module system is handled in the output JavaScript. 
   - ESNext indicates that the output should use the latest JavaScript module syntax (import and export).
<br><br>
- outDir
   - Specifies the directory where compiled JavaScript files should be placed. 
<br><br>
- strict
   - By default, strict mode enables a set of options that enforce more rigorous type checks. 
   - With this setting false, the code will be more lenient.
<br><br>
- moduleDetection
   - JavaScript treats every file as a separate module, whereas TypeScript treats every file as a global module.
   - To treat all files as individual modules in typescript, you can use the "force" keyword.
   - If you don't want to use to "force" keyword, you must the following keyword in every file:
      ```typescript
      export {}
      ```
   <br>
- skipLibCheck
   - Skips type checking of all declaration (.d.ts) files. 
   - This can speed up the compilation process, but it may cause some subtle type errors to be ignored.
<br><br>
- include: [directory]
   - Specifies the files or directories to include in the compilation. 

## :label: Types
### Type hierarchy
<img width="2297" alt="image" src="https://github.com/user-attachments/assets/23b7f690-d28d-4aa4-abae-8c4d53733a3f">
<br>
   
### Primitive types
- number
   ```typescript
   const num1: number = 123
   const num2: number = -123
   const num3: number = 0.123
   const num4: number = -0.123
   const num5: number = Infinity
   const num6: number = -Infinity
   const num7: number = NaN
   ```
<br>

- string
   ```typescript
   const str1: string = 'hello'
   const str2: string = "hello"
   const str3: string = `hello`
   const str4: string = `hello ${something}`
   ```
<br>

- boolean
   ```typescript
   const bool1: boolean = true
   const bool2: boolean = false
   ```
<br>

- null
   ```typescript
   const null1: null = null
   ```
<br>

- undefined
   ```typescript
   const undefined1: undefined = undefined
   ```
<br>

### Literal types
- Literal types
   ```typescript
   let numA: 10 = 10
   numA = 13 // error - Type '13' is not assignable to type '10'.
   
   const strA: 'hello' = 'hi' // error - Type '"hi"' is not assignable to type '"hello"'.
   const boolA: true = false // error - Type 'false' is not assignable to type 'true'.
   ```
<br>
   
### Array
- Array
   ```typescript
   const numArr: number[] = [1, 2, 3]
   const strArr: string[] = ['hello', 'im', 'Jisung']
   const boolArr: boolean[] = [true, false]
   ```
<br>
   
- When the array elements have different types
   ```typescript
   const multiTypesArr: (string | number)[] = [1, 'hello']
   ```
<br>

- Type of a multidimensional array
   ```typescript
   const multiArr: number[][] = [
     [1, 2, 3],
     [4, 5]
   ]
   ```
<br>

- Tuple
   - An array with fixed length and type
   - Don’t confuse (type | type | ...)[] with a Tuple. A Tuple should be used as [type, type, ...].
```typescript
let tuple1: [number, number] = [1, 2]
tuple1 = [1, 2, 3]   // error - Type '[number, number, number]' is not assignable to type '[number, number]'.
tuple1 = ['1', '2']  // error - Type 'string' is not assignable to type 'number'.

let tuple2: [number, string, boolean] = [1, '2', true]

const users: [string, number][] = [
  ['a', 1],
  ['b', 2],
  ['c', 3],
  ['d', 4]
  [5, 'e'] // error - 1. Type 'number' is not assignable to type 'string'. 2. Type 'string' is not assignable to type 'number'.
]
```
<br>

### Object
- Object
   ```typescript
   let user: { id: number; name: string } = {
     id: 1,
     name: 'Jisung'
   }
   ```
<br>

- Optional property
```typescript
   let user: { id?: number; name: string } = {
     id: 1,
     name: 'Jisung'
   }
   
   user = {
     name: 'kurt'
   }
```
<br>

- Readonly
```typescript
   let config: {
     readonly apiKey: string
   } = {
     apiKey: 'MY API KEY'
   }
   
   config.apiKey = 'hacked' // error - Cannot assign to 'apiKey' because it is a read-only property.
```
<br>

## :label: Type alias
- Type alias
   ```typescript
   type User = {
     id: number
     name: string
     nickname: string
     birth: string
     bio: string
     location: string
   }
   
   let user: User = {
     id: 1,
     name: 'Jisung',
     nickname: 'kurt',
     birth: '2000.01.01',
     bio: 'hi',
     location: 'Daegu'
   }
   ```
<br>
   
## :label: Index signature
- Index signature
   ```typescript
   type CountryCodes = {
     [key: string]: string
   }
   let CountryCodes = {
     Korea: 'ko',
     UnitedState: 'us',
     UnitedKingdom: 'uk'
   }
   ```
<br>

- Caveats
   - When an index signature is defined, all keys must have a consistent type.
      ```typescript
      type CountryCodes = {
        [key: string]: string
        Korea: number // error - Property 'Korea' of type 'number' is not assignable to 'string' index type 'string'.
      }
      let CountryCodes = {
        Korea: 82,
        UnitedState: 'us',
        UnitedKingdom: 'uk'
      }
      ```
<br>
   
## :label: Enum
- Enums allow a developer to define a set of named constants. 
- Using enums can make it easier to document intent, or create a set of distinct cases. 
- TypeScript provides both numeric and string-based enums.

### Numeric enums
   ```typescript
   enum Role {
     ADMIN, // 0
     USER,  // 1
     GUEST  // 2
   }
   const user1 = {
     name: 'Jisung',
     role: Role.ADMIN
   }
   
   const user2 = {
     name: 'Mike',
     role: Role.USER
   }
   
   const user3 = {
     name: 'Tom',
     role: Role.GUEST
   }
   ```
<br>

### String enums
   ```typescript
   enum Language {
     korea = 'ko',
     english = 'en'
   }
   
   const user = {
     name: 'Jisung',
     language: Language.korea
   }
   ```
<br>
   
## :label: Any
- TypeScript also has a special type, any, that you can use whenever you don’t want a particular value to cause typechecking errors.
- When a value is of type any, you can access any properties of it (which will in turn be of type any), call it like a function, assign it to (or from) a value of any type, or pretty much anything else that’s syntactically legal.
- The any type is useful when you don’t want to write out a long type just to convince TypeScript that a particular line of code is okay.
   ```typescript
   let anyValue: any = 10
   anyValue = 'hello'
   
   anyValue = true
   anyValue = {}
   anyValue = () => {}
   
   anyValue.toUpperCase()
   anyValue.toFixed()
   
   let num: number = 10
   num = anyValue
   ```
<br>
   
## :label: Unknown
- The unknown type represents any value. This is similar to the any type, but is safer because it’s not legal to do anything with an unknown value.
- This is useful when describing function types because you can describe functions that accept any value without having any values in your function body.
- Conversely, you can describe a function that returns a value of unknown type.
   ```typescript
   let unknownValue: unknown
   
   unknownValue = ''
   unknownValue = 1
   unknownValue = () => {}
   
   let num: number = 10
   num = unknownValue // error - Type 'unknown' is not assignable to type 'number'.
   
   // if you want to use the above, do it like this:
   if (typeof unknownValue === 'number') {
     num = unknownValue
   }
   ```
<br>
   
## :label: Void
- void represents the return value of functions which don’t return a value.
- In JavaScript, a function that doesn’t return any value will implicitly return the value undefined. 
- However, void and undefined are not the same thing in TypeScript.
   ```typescript
   function func(): void {
     console.log('hello')
   }
   
   let a: void
   a = 1 // error - Type 'number' is not assignable to type 'void'.
   a = 'hello' // error - Type 'string' is not assignable to type 'void'.
   a = {} // error - Type '{}' is not assignable to type 'void'.
   a = undefined
   a = null
   ```
<br>
   
## :label: Never
- The never type represents values which are never observed. 
- In a return type, this means that the function throws an exception or terminates execution of the program.
- never also appears when TypeScript determines there’s nothing left in a union.
   ```typescript
   function func(): never {
     throw new Error()
   }
   
   let a: never
   a = 1 // error - Type 'number' is not assignable to type 'void'.
   a = {} // error - Type '{}' is not assignable to type 'void'.
   a = '' // error - Type 'string' is not assignable to type 'void'.
   a = undefined // error - Type 'undefined' is not assignable to type 'void'.
   a = null // error - Type 'null' is not assignable to type 'void'.
   
   let anyValue: any
   a = anyValue // error - Type 'any' is not assignable to type 'void'.
   ```
<br>

## :label: Type compatibility
### Type compatibility table
<img width="909" alt="image" src="https://github.com/user-attachments/assets/3c90180b-1220-41ea-b606-d7a75c87fc1d">
<br>

### Type compatibility
- In typescript, upcasting is allowed for all types, but downcasting is not allowed.
   ```typescript
   let unknownValue: unknown
   let anyValue: any
   let numValue: number
   let voidValue: void
   let stringValue: string
   let boolValue: boolean
   
   unknownValue = anyValue
   unknownValue = numValue
   unknownValue = voidValue
   unknownValue = stringValue
   unknownValue = boolValue
   
   numValue = unknownValue    // error - Type 'unknown' is not assignable to type 'number'.
   voidValue = unknownValue   // error - Type 'unknown' is not assignable to type 'void'.
   stringValue = unknownValue // error - Type 'unknown' is not assignable to type 'string'.
   boolValue = unknownValue   // error - Type 'unknown' is not assignable to type 'boolean'.
   ```
   <br>

- Caveats
   - You need to be aware of a few exceptions:
      - unknown type can be downcast to any type specifically. In other words, you can assign an unknown type to an any type. 
         ```typescript
         let unknownValue: unknown
         let anyValue: any
         
         anyValue = unknownValue
         ```
         <br>
      - The any type ignores the type hierarchy.
      - So it can be downcast to any other type, and any type can be upcast to any.   
      - Except for the never type.
         ```typescript
         let unknownValue: unknown
         let anyValue: any
         let numValue: number
         let voidValue: void
         let stringValue: string
         let boolValue: boolean
         let neverValue: never
         
         // upcasting
         anyValue = unknownValue
         anyValue = numValue
         anyValue = voidValue
         anyValue = stringValue
         anyValue = boolValue
         anyValue = neverValue
         
         // downcasting
         unknownValue = anyValue
         numValue = anyValue
         voidValue = anyValue
         stringValue = anyValue
         boolValue = anyValue
         neverValue = anyValue // error - Type 'any' is not assignable to type 'never'.
         ```
      <br>
   
#### Object type compatibility
- Typescript is property-based type system.
   ```typescript
   type Animal = {
     name: string
     color: string
   }
   
   type Dog = {
     name: string
     color: string
     breed: string
   }
   
   let animal: Animal = {
     name: 'Cat',
     color: 'white'
   }
   
   let dog: Dog = {
     name: 'ppoddo',
     color: 'gold',
     breed: 'maltipoo'
   }
   
   // animal: super, dog: sub
   animal = dog // upcasting
   dog = animal // error - downcasting
   ```
<br>

- Excess property checking(error)
   - Excess property checking is a feature that ensures that __object literals__ do not have properties that are not defined in their corresponding type or interface.
   - When you assign an object literal to a variable of a specific type, typescript checks for any extra properties not described by that type.
<br>
  
## :label: Algebraic type
- A newly created type formed by combining different types.
<br>

### Union type
   ```typescript
   let a: string | number // string number union type
   
   a = 'hello'
   a = 1
   
   // array
   let arr: (number | string | boolean)[] = [1, 'hello', true]
   console.log(arr) // Expected output: [ 1, 'hello', true ]
   
   // object
   type Dog = {
     name: string
     color: string
   }
   
   type Person = {
     name: string
     language: string
   }
   
   type UnionObject = Dog | Person
   
   let union1: UnionObject = {
     name: '',
     color: ''
   }
   console.log(union1) // Expected output: { name: '', color: '' }
   
   let union2: UnionObject = {
     name: '',
     language: ''
   }
   console.log(union2) // Expected output: { name: '', language: '' }
   
   let union3: UnionObject = {
     name: '',
     color: '',
     language: ''
   }
   console.log(union3) // Expected output: { name: '', color: '', language: '' }
   
   // error - It must be either { name, color } or { name, language }, or { name, color, language }.
   let union4: UnionObject = {
     name: ''
   }
   ```
<br>
   
### Intersection type
   ```typescript
   // primitive type
   let a: number & string // never type
   console.log(a) // Expected output: undefined
   
   // object
   type Dog = {
     name: string
     color: string
   }
   
   type Person = {
     name: string
     language: string
   }
   
   type Intersection = Dog & Person
   
   let intersection: Intersection = {
     name: '',
     color: '',
     language: ''
   }
   
   console.log(intersection) // Expected output: { name: '', color: '', language:'' }
   ```
<br>
   
## :label: Type inference
- When a type specified, the variable will explicitly have an any type.
   - Therefore, the following all have the any type.
      ```typescript
      let value: any // value: any
      
      value = 10 // value: any
      value.toFixed() // value: any
      value.toUpperCase() // value: any
      
      value = 'hello' // value: any
      value.toUpperCase() // value: any
      value.toFixed() // value: any
      ```
<br>

- When a type is not specified, the variable will implicitly have an any type.
   - The implicit any type evolves as shown below:
      ```typescript
      // if nothing is assigned, the any type will be inferred.
      let value // value: any
      
      value = 10 // value: any
      value.toFixed() // value: number
      value.toUpperCase() // value: number, so error - Property 'toUpperCase' does not exist on type 'number'.
      
      value = 'hello' // value: any
      value.toUpperCase() // value: string
      value.toFixed() // value: string, so error - Property 'toFixed' does not exist on type 'string'.
      ```
<br>
   
## :label: Type assertion
- Type assertion in typescript allows developers to explicitly define a value’s type, instructing the compiler to treat it as such, even if it cannot infer it.
- This enables overriding the inferred type system when developers are confident in the value’s type.
- When using the value as Type syntax, the type of value must be either a supertype or a subtype of Type.
   ```typescript
   type Person = {
     name: string
     age: number
   }
   
   {
     let person: Person = {} // Type '{}' is missing the following properties from type 'Person': name, age
     person.name = 'jisung'
     person.age = 20
   }
   
   {
     let person = {}
     person.name = 'jisung' // error - Property 'name' does not exist on type '{}'.
     person.age = 20 // error - Property 'age' does not exist on type '{}'.
   }
   
   {
     let person = {} as Person // type assertion
     person.name = 'jisung'
     person.age = 20
   }
   ```
<br>
   
   ```typescript
   type Dog = {
     name: string
     color: string
   }
   
   {
     let dog: Dog = {
       name: 'ppoddo',
       color: 'gold',
       breed: 'maltipoo' // error - Object literal may only specify known properties, and 'breed' does not exist in type 'Dog'.
     }
   }
   
   {
     let dog: Dog = {
       name: 'ppoddo',
       color: 'gold',
       breed: 'maltipoo'
     } as Dog // type assertion, but it may cause runtime errors, so caution is needed.
   }
   ```
<br>
   
   ```typescript
   let num1 = 10 as never // num1: never
   let num2 = 10 as unknown // num2: unknown
   
   let num3 = 10 as string // error - Conversion of type 'number' to type 'string' may be a mistake because neither type sufficiently overlaps with the other. If this was intentional, convert the expression to 'unknown' first.
   ```
<br>
   
### Const assertion
   ```typescript
   let num = 10 as const // num: 10 - variable can not change
   num = 11 // error - Type '11' is not assignable to type '10'.
   
   let dog = {
     name: 'ppoddo',
     color: 'gold'
   } as const // Property values cannot be changed.
   
   dog.color = 'white' // error - Cannot assign to 'color' because it is a read-only property.
   ```
<br>

### Non-null assertion
   ```typescript
   type Post = {
     title: string
     author?: string
   }
   
   let post: Post = {
     title: 'post1',
     author: 'jisung'
   }
   
   const len1: number = post.author?.length //error - Type 'number | undefined' is not assignable to type 'number'.
   const len2: number = post.author!.length // non-null assertion
   ```
<br>
   
## :label: Type narrowing
   ```typescript
     type Person = {
       name: string
       age: number
     }
   
     function func(value: number | string | Date | null | Person) {
       value // value: number | string
       value.toFixed() // error - Property 'toFixed' does not exist on type 'string | number'.
       value.toUpperCase() // error - Property 'toUpperCase' does not exist on type 'string | number'.
   
       // type guard
       if (typeof value === 'number') {
         console.log(value.toFixed()) // value: number
       }
       // type guard
       else if (typeof value === 'string') {
         console.log(value.toUpperCase()) // value: number
       }
       // type guard
       else if (value instanceof Date) {
         console.log(value.getTime())
       }
   
       // type guard
       else if (value && 'age' in value) {
         console.log(`${value.name} is ${value.age} years old.`)
       }
     }
   
   ```
<br>
   
## :label: Discriminated union(tagged union)
- before use discriminated union
   ```typescript
   type Admin = {
     name: string
     kickCount: number
   }
   
   type Member = {
     name: string
     point: number
   }
   
   type Guest = {
     name: string
     visitCount: number
   }
   
   type User = Admin | Member | Guest
   
   function login(user: User) {
     if ('kickCount' in user) {
       console.log(
         `${user.name}, you have kicked out ${user.kickCount} users so far.`
       )
     } else if ('point' in user) {
       console.log(
         `${user.name}, you have collected ${user.point} points so far.`
       )
     } else {
       console.log(
         `${user.name}, you have visited ${user.visitCount} times so far.`
       )
     }
   }
   ```
<br>

- after use discriminated union
   ```typescript
   type Admin = {
     tag: 'ADMIN'
     name: string
     kickCount: number
   }
   
   type Member = {
     tag: 'MEMBER'
     name: string
     point: number
   }
   
   type Guest = {
     tag: 'GUEST'
     name: string
     visitCount: number
   }
   
   type User = Admin | Member | Guest
   
   function login(user: User) {
     switch (user.tag) {
       case 'ADMIN':
         console.log(
           `${user.name}, you have kicked out ${user.kickCount} users so far.`
         )
         break
       case 'MEMBER':
         console.log(
           `${user.name}, you have collected ${user.point} points so far.`
         )
         break
       case 'GUEST':
         console.log(
           `${user.name}, you have visited ${user.visitCount} times so far.`
         )
         break
     }
   }
   ```
<br>

- before use discriminated union
   ```typescript
   type AsyncTask = {
     state: 'LOADING' | 'FAILED' | 'SUCCESS'
     error?: {
       message: string
     }
     response?: {
       data: string
     }
   }
   
   function processResult(task: AsyncTask) {
     switch (task.state) {
       case 'LOADING':
         console.log('loading..')
         break
       case 'FAILED':
         console.log(`error: ${task.error?.message}`)
         break
       case 'SUCCESS':
         console.log(`success: ${task.response?.data}`)
         break
     }
   }
   
   const loading: AsyncTask = {
     state: 'LOADING'
   }
   
   const failed: AsyncTask = {
     state: 'FAILED',
     error: {
       message: 'error'
     }
   }
   
   const success: AsyncTask = {
     state: 'SUCCESS',
     response: {
       data: 'response'
     }
   }
   ```
<br>

- after use discriminated union
   ```typescript
   type LoadingTask = {
     state: 'LOADING'
   }
   
   type FailedTask = {
     state: 'FAILED'
     error: {
       message: string
     }
   }
   
   type SuccessTask = {
     state: 'SUCCESS'
     response: {
       data: string
     }
   }
   
   type AsyncTask = LoadingTask | FailedTask | SuccessTask
   
   function processResult(task: AsyncTask) {
     switch (task.state) {
       case 'LOADING':
         console.log('loading..')
         break
       case 'FAILED':
         console.log(`error: ${task.error.message}`)
         break
       case 'SUCCESS':
         console.log(`success: ${task.response.data}`)
         break
     }
   }
   
   const loading: AsyncTask = {
     state: 'LOADING'
   }
   
   const failed: AsyncTask = {
     state: 'FAILED',
     error: {
       message: 'error'
     }
   }
   
   const success: AsyncTask = {
     state: 'SUCCESS',
     response: {
       data: 'response'
     }
   }
   ```
<br>
   
## :label: Function
### Rest parameter
   ```typescript
   const getSum = (...rest: number[]) => {
     let sum = 0
     rest.forEach((item) => {
       sum = sum + item
     })
   
     return sum
   }
   
   getSum(1, 2, 3)
   getSum(1, 2, 3, 4, 5, 6)
   ```
<br>
   
   - use with tuple
      ```typescript
      const getSum = (...rest: [number, number, number]) => {
        let sum = 0
        rest.forEach((item) => {
          sum = sum + item
        })
      
        return sum
      }
      
      getSum(1, 2, 3)
      getSum(1, 2, 3, 4, 5, 6) // error - Expected 3 arguments, but got 6.
      ```
<br>
   
### Function type expression
   ```typescript
   type Operation = (a: number, b: number) => number
   
   const add: Operation = (a, b) => a + b
   const sub: Operation = (a, b) => a - b
   const multiply: Operation = (a, b) => a * b
   const divide: Operation = (a, b) => a / b
   ```
<br>
   
### Call signature
   ```typescript
   type Operation = {
     (a: number, b: number): number
   }
   
   const add: Operation = (a, b) => a + b
   const sub: Operation = (a, b) => a - b
   const multiply: Operation = (a, b) => a * b
   const divide: Operation = (a, b) => a / b
   ```
<br>
   
### Function type compatibility
1. Is the return type compatible?
   ```typescript
   type A = () => number
   type B = () => 10
   
   let a: A = () => 10
   let b: B = () => 10
   
   // A: super, B: sub
   a = b // upcasting
   b = a // error - downcasting
   ```
<br>

2. Is the parameter type compatible?
   1. When the number of parameters is the same
      ```typescript
      {
        type C = (value: number) => void
        type D = (value: 10) => void
      
        let c: C = (value) => {}
        let d: D = (value) => {}
      
        // When determining function type compatibility based on parameter types, upcasting is not allowed, but downcasting is possible.
        c = d // error - upcasting
        d = c // downcasting
      }
      
      {
        // super
        type Animal = {
          name: string
        }
      
        // sub
        type Dog = {
          name: string
          color: string
        }
      
        let animalFunc = (animal: Animal) => {
          console.log(animal.name)
        }
      
        let dogFunc = (dog: Dog) => {
          console.log(dog.name)
          console.log(dog.color)
        }
      
        // Type '(dog: Dog) => void' is not assignable to type '(animal: Animal) => void'.
        // Types of parameters 'dog' and 'animal' are incompatible.
        // Property 'color' is missing in type 'Animal' but required in type 'Dog'.
        animalFunc = dogFunc // error
      
        let testFunc1 = (animal: Animal) => {
          console.log(animal.name)
          console.log(animal.color) // error - Property 'color' does not exist on type 'Animal'.
        }
      
        dogFunc = animalFunc
      
        let testFunc2 = (dog: Dog) => {
          console.log(dog.name)
        }
      }
      ```
   <br>

   2. When the number of parameters is the same
      ```typescript
      type Func1 = (a: number, b: number) => void
      type Func2 = (a: number) => void
      
      let func1: Func1 = (a, b) => {
        console.log(`a=${a}, b=${b}`)
      }
      
      let func2: Func2 = (a) => {
        console.log(`a=${a}`)
      }
      
      func1(1, 2) // Expected output: a=1, b=2
      func2(3) // Expected output: a=3
      
      func1 = func2
      func1(1, 2) // Expected output: a=1
      
      func2 = func1 // error - Type 'Func1' is not assignable to type 'Func2'. Target signature provides too few arguments. Expected 2 or more, but got 1.
      ```
      <br>

### Overloading
   ```typescript
   // overload signature(=overload definition)(=overload declaration)
   function func(a: number): void
   function func(a: number, b: number, c: number): void
   
   // implementation signature
   function func(a: number, b?: number, c?: number) {
     if (typeof b === 'number' && typeof c === 'number') {
       console.log(a + b + c)
     } else {
       console.log(a * 20)
     }
   }
   
   func() // error - Expected 1-3 arguments, but got 0.
   func(1)
   func(1, 2) // error - No overload expects 2 arguments, but overloads do exist that expect either 1 or 3 arguments.
   func(1, 2, 3)
   ```
   <br>

### Custom type guard
   ```typescript
   // if we cannot use discriminated union, we can use custom type guard
   type Dog = {
     name: string
     isBark: boolean
   }
   
   type Cat = {
     name: string
     isScratch: boolean
   }
   
   type Animal = Dog | Cat
   
   function isDog(animal: Animal): animal is Dog {
     return (animal as Dog).isBark !== undefined
   }
   
   function isCat(animal: Animal): animal is Cat {
     return (animal as Cat).isScratch !== undefined
   }
   
   function warning(animal: Animal) {
     if (isDog(animal)) {
       console.log(`The type is Dog, isBark=${animal.isBark}`)
     } else if ('isScratch' in animal) {
       console.log(`The type is Cat, isScratch=${animal.isScratch}`)
     }
   }
   ```
<br>
   
## :label: Interface
- Naming a Type
   - An interface provides a way to name a type in typescript, similar to a type alias. 
   - This makes the code more readable and reusable by giving a descriptive name to a particular shape of data.
      ```typescript
      interface Person {
        name: string
        age: number
        // Function type expression
        expressionFunc: () => void
        // If you want to use overloading you have to use call signature(Don't use function type expression)
        // Call signature
        // overloading
        callSignatureFunc(): void
        callSignatureFunc(a: number, b: number): void
        // rest parameter
        restFunc(...rest: number[]): void
      }
      ```
<br>
   
- Defining the structure of objects
   - Interfaces are particularly useful for defining the structure of an object. 
   - They specify the expected properties and their types, ensuring that objects adhere to a specific format.
      ```typescript
      const user: Person = {
        name: 'Jisung',
        age: 30,
        expressionFunc: () => {
          console.log('Run expressionFunc() !')
        },
        callSignatureFunc: (a?, b?) => {
          if (a === undefined && b === undefined) {
            console.log('Run callSignatureFunc() !')
            return
          }
          console.log(`Run callSignatureFunc(${a}, ${b}) !`)
        },
        restFunc: (...rest) => {
          console.log(`Run restFunc([${rest}]) !`)
        }
      }
      
      console.log(user.name) // Expected output: Jisung
      
      user.expressionFunc() // Expected output: Run expressionFunc() !
      
      user.callSignatureFunc() // Expected output: Run callSignatureFunc() !
      user.callSignatureFunc(1, 2) // Expected output: Run callSignatureFunc(1, 2) !
      
      user.restFunc() // Expected output: Run restFunc([]) !
      user.restFunc(1, 2, 3) // Expected output: Run restFunc([1,2,3]) !
      user.restFunc(1, 2, 3, 4, 5) // Expected output: Run restFunc([1,2,3,4,5]) !
      ```
<br>
   
- Special Features
   - Inheritance
      - Interfaces support inheritance through the extends keyword, allowing one interface to inherit properties from another. 
      - This is useful for creating more specialized versions of an interface while keeping the code DRY (Don’t Repeat Yourself).
         ```typescript
         interface Employee extends Person {
           role: string
         }
         ```
   <br>

   - Merging
      - One of the unique features of interfaces is that they can be merged. 
      - If two interfaces with the same name are declared, TypeScript will automatically merge their properties, making it easier to extend functionality.
         ```typescript
         interface Person {
           gender: string  // added to the existing Person interface
         }
         ```
<br>
   
- Interfaces cannot use algebraic types.
   ```typescript
   interface Person {
     name: string
     age: number
   }
   
   const user1: Person = {
     name: 'Jisung',
     age: 30
   } | number // error - 'number' only refers to a type, but is being used as a value here.
   
   
   const user2: Person = {
     name: 'Jisung',
     age: 30
   } & number // error - 'number' only refers to a type, but is being used as a value here.
   
   
   // if you want to use algebraic types, you should use them as shown below
   const user3: Person | number = {
     name: 'Jisung',
     age: 30
   }
   ```
<br>
   
### Inheritance 
- extends keyword
   - In typescript, inheritance is a way to define relationships between objects, enhancing code reusability.
   - The extends keyword is used for the subclass (sub) to inherit the properties and methods of the superclass (super).
   - The subclass automatically inherits all properties and methods of the superclass but can also define additional properties.
      ```typescript
      interface Animal {
        name: string
        color: string
      }
      
      interface Dog extends Animal {
        isBark: boolean
      }
      
      const dog: Dog = {
        name: '',
        color: '',
        isBark: true
      }
      ```
<br>
   
- property type redefinition
   - If a subclass wants to redefine the type of a property inherited from a superclass, that type must be in a super-sub relationship with the superclass. In other words, the subclass type must include the superclass type to avoid errors.
   - In TypeScript, it is possible to refine the types of inherited properties, but they cannot be changed to completely different types. Violating this principle will result in type compatibility issues.
      ```typescript
      interface Animal {
        name: string
        color: string
      }
      
      interface Dog extends Animal {
        name: 'hello'
        isBark: boolean
      }
      ```
<br>
   
- multiple inheritance
   - In TypeScript, multiple inheritance refers to the capability of inheriting from multiple interfaces.
   - This allows a single interface to include properties and methods from several other interfaces.
   - Multiple inheritance is achieved using the extends keyword, and the interfaces being inherited are separated by commas.
      ```typescript
      interface Animal {
        name: string
        color: string
      }
      
      interface Dog extends Animal {
        isBark: boolean
      }
      
      interface Cat extends Animal {
        isScratch: boolean
      }
      
      interface DogCat extends Dog, Cat {}
      
      const dogCat: DogCat = {
        name: '',
        color: '',
        isBark: true,
        isScratch: true
      }
      ```
      <br>

### Interface declaration merging
- When an interface with the same name is declared multiple times, TypeScript merges them into a single interface.
   ```typescript
   interface Person {
     name: string
   }
   
   interface Person {
     age: number
   }
   
   const person: Person = {
     name: '',
     age: 20
   }
   ```
<br>
