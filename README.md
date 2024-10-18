# play-typescript

My personal playground for typescript coding and learning.

## :pushpin: Summary
### Table of contents
- [TypeScript](#label-typescript)
- [Compiler options(tsconfig.json)](#label-compiler-options(tsconfig-json))
- [Types](#label-types)
- [Index signature](#label-index-signature)
- [Enum](#label-enum)

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
