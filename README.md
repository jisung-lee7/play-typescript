# play-typescript

My personal playground for typescript coding and learning.

## :pushpin: Summary
### Table of contents
- [TypeScript](#label-typescript)
- [Compiler options(tsconfig.json)](#label-compiler-options(tsconfig-json))

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
