# TypeScript-DOCS

## Why TypeScript?
![1](https://user-images.githubusercontent.com/77200870/188300785-de1534d0-2dc0-49bd-9a46-fe82d71df3bf.PNG)

<br/>

## Course Overview
![2](https://user-images.githubusercontent.com/77200870/188300772-45d15b0d-a7ea-4a8d-9c01-e09f52e07cc4.PNG)

<br/>

## 0x00 - TypeScript Types
### The problem 🚧
```js
const message = "Hello World!";

message();
```
> This won't produce any error during development, only when we run the above code we will get a `TypeError` because the JavaScript runtime figures the type of the value and lists the behaviors and capabilities it has.

### The solution ✔️
> TypeScript solves this thanks to its `static type-checker`

<br/>

### The problem 🚧 : Non-exception Failures
> So far we’ve been discussing certain things like runtime errors - cases where the JavaScript runtime tells us that it thinks something is nonsensical. Those cases come up because the ECMAScript specification has explicit instructions on how the language should behave when it runs into something unexpected.
For example, the specification says that trying to call something that isn’t callable should throw an error. Maybe that sounds like “obvious behavior”, but you could imagine that accessing a property that doesn’t exist on an object should throw an error too. Instead, JavaScript gives us different behavior and returns the value undefined

```js
const user = {
  name: "Daniel",
  age: 26,
};
user.location; // returns undefined
```

### The solution ✔️
> Using the TS static type-checker

![ts1](https://user-images.githubusercontent.com/77200870/188301352-0307ae22-285c-478b-9ef4-0978d9d331e8.PNG)

<br/>

### The problem 🚧 : Legitimate Bugs
#### [1] Typos
![ts2](https://user-images.githubusercontent.com/77200870/188301427-db416fae-bf55-4393-bf98-2d660d7799c4.PNG)
#### [2] uncalled functions
![ts3](https://user-images.githubusercontent.com/77200870/188301465-58e28f16-7f72-4134-8b73-3d4d93e67372.PNG)
#### [3] Basic Logic Errors
![ts5](https://user-images.githubusercontent.com/77200870/188301488-b41113fb-25a4-473c-af0d-50789de889f4.PNG)

--------------------------------------------------------------
### Types for Tooling 🔨
> TypeScript core type-checker can provide error messages and code completion as you type in the editor, that's what people refer to as `tooling in TypeScript`
But tooling in TypeScript goes beyond completions and errors as you type. An editor that supports TypeScript can deliver “quick fixes” to automatically fix errors, refactorings to easily re-organize code, and useful navigation features for jumping to definitions of a variable, or finding all references to a given variable. All of this is built on top of the type-checker and is fully cross-platform.

![ts6](https://user-images.githubusercontent.com/77200870/188301702-fc8f33b6-7730-48ff-86f7-07a46cb74cac.PNG)

<br/>

### Everday Types
> With TypeScript we can add `type annotations` on variables and function paramaters
```ts
function greet(person: string, date: Date) {
  console.log(`Hello ${person}, today is ${date.toDateString()}!`);
}
```
<p>Date() in JavaScript returns a string</p>

![ts7](https://user-images.githubusercontent.com/77200870/188301828-5d469bf9-3976-4aaa-8788-be70afac998d.PNG)

> Keep in mind, we don’t always have to write explicit type annotations. In many cases, TypeScript can even just infer (or “figure out”) the types for us even if we omit them (Type Inference).

![ts8](https://user-images.githubusercontent.com/77200870/188301879-92b91205-e624-4c4e-bceb-25a1b5f771fe.PNG)

>Even though we didn’t tell TypeScript that `msg` had the type `string` it was able to figure that out. That’s a feature, and it’s best not to add annotations when the type system would end up inferring the same type anyway.

#### All TypeScript Basic Types
![4](https://user-images.githubusercontent.com/77200870/188302167-8b05dade-c874-40a5-916f-27dc6b61fcbd.PNG)

**[01] number, string, boolean, Date :**

```ts 
let age: number = 19;
```

<br/>

**[02] object:** 

```js
const student: {
  name: string;
  age: number;
} = {
  name: 'Jakob',
  age: 19,
}
```

> The type part of each property is optional, if it's not specified it's assumed to be of type `any`

> We can set a property to be optional by using ? : `obj: { first: string; last?: string }`

<p>In JavaScript, if you access a property that doesn’t exist, you’ll get the value `undefined` rather than a runtime error. Because of this, when you read from an optional property, you’ll have to check for `undefined` before using it.</p>

![ts7](https://user-images.githubusercontent.com/77200870/188303248-50369664-19a9-4736-b26e-c1dd14ae8d76.PNG)

<br/>

**[03] Arrays:** 

```js
let cars: string[] = ['BMW', 'MARCEDES'] // string-only array
let names: any[] = ['Jakob', 19, 100] // mixed-type array
```

<br/>

**[04] Tuples:**

<p>Fixed length arrays</p>

```js
const role: [number, string]
```

<br/>

**[05] Enums:**

<p>Automatically enumerated global constant identifiers</p>

```ts
enum Role {ADMIN, READ_ONLY, PUBLISHER}
```

**Notes**
- Enum values are automatically assigned values starting from 0
- We can overide this by explicitly setting the first value : `enum Role {ADMIN = 5, READ_ONLY, PUBLISHER}`
- We can set values for all the enums : `enum Role {ADMIN = 5, READ_ONLY = 1000, PUBLISHER= 152}`
- To access them we use the syntax : `Role.ADMIN`, this returns `5`

<br/>

**[05] Enums:**

```ts
let addValues: Function;
```
<br/>

### Downleveling
<p>When we compile the previous example to plain JavaScript we go from</p>

![ts9](https://user-images.githubusercontent.com/77200870/188301981-d0c754d1-c3f8-4a29-a0b7-c6e19ff30d6d.PNG)

To

![ts1](https://user-images.githubusercontent.com/77200870/188301998-515594bc-fb65-474f-836e-652fd69e0f8b.PNG)

>Template strings are a feature from a version of ECMAScript called ECMAScript 2015 (a.k.a. ECMAScript 6, ES2015, ES6, etc. - don’t ask). TypeScript has the ability to rewrite code from newer versions of ECMAScript to older ones such as ECMAScript 3 or ECMAScript 5 (a.k.a. ES3 and ES5). This process of moving from a newer or “higher” version of ECMAScript down to an older or “lower” one is sometimes called downleveling.
By default TypeScript targets ES3, an extremely old version of ECMAScript. We could have chosen something a little bit more recent by using the target option. Running with `--target es2015` changes TypeScript to target ECMAScript 2015, meaning code should be able to run wherever ECMAScript 2015 is supported. So running `tsc --target es2015 hello.ts` gives us the same output above for all es6 features


<br/>

### Functions 📘
#### Parameter Type Annotations

<p>When you declare a function, you can add type annotations after each parameter to declare what types of parameters the function accepts. Parameter type annotations go after the parameter name:</p>

![ts](https://user-images.githubusercontent.com/77200870/188305088-a282e66d-52f0-4e57-871b-6b1a5399c9ae.PNG)

<p>When a parameter has a type annotation, arguments to that function will be checked</p>

![ts1](https://user-images.githubusercontent.com/77200870/188305120-7c7ec750-f18a-49c5-9174-23549a09186e.PNG)

>Even if you don’t have type annotations on your parameters, TypeScript will still check that you passed the right number of arguments.

#### Return Type Annotations

<p>You can also add return type annotations. Return type annotations appear after the parameter list:</p>

![ts5](https://user-images.githubusercontent.com/77200870/188305151-82e1c43d-02d0-4c9c-a828-80f4e82a915a.PNG)

**Note** 🚧
>Much like variable type annotations, you usually don’t need a return type annotation because TypeScript will infer the function’s return type based on its return statements. The type annotation in the above example doesn’t change anything. Some codebases will explicitly specify a return type for documentation purposes, to prevent accidental changes, or just for personal preference.

<br/>

### Union Types

<p>TypeScript’s type system allows you to build new types out of existing ones using a large variety of operators. Now that we know how to write a few types, it’s time to start combining them in interesting ways.</p>

#### Defining a Union Type

<p>The first way to combine types you might see is a union type. A union type is a type formed from two or more other types, representing values that may be any one of those types. We refer to each of these types as the union’s members.
Let’s write a function that can operate on strings or numbers:</p>

![ts2](https://user-images.githubusercontent.com/77200870/188302845-31421fe3-f18b-4482-8c63-9295099890c6.PNG)

#### Working with Union Types
> TypeScript will only allow an operation if it is valid for every member of the union. For example, if you have the union string | number, you can’t use methods that are only available on string

![ts3](https://user-images.githubusercontent.com/77200870/188302912-815d6e0f-c8a7-493f-b119-8dfd847821c9.PNG)

<p>The solution is to narrow the union with code, the same as you would in JavaScript without type annotations. Narrowing occurs when TypeScript can deduce a more specific type for a value based on the structure of the code.
For example, TypeScript knows that only a string value will have a typeof value "string":</p>

![ts4](https://user-images.githubusercontent.com/77200870/188302940-0a50e18b-84ba-45fb-8f6f-62a521aba5f0.PNG)

<p>Another example is to use a function like Array.isArray:</p>

![ts5](https://user-images.githubusercontent.com/77200870/188302970-b10d19a2-073b-438d-80a3-7dd3390d7b32.PNG)

>Notice that in the else branch, we don’t need to do anything special - if x wasn’t a string[], then it must have been a string.

<p>Sometimes you’ll have a union where all the members have something in common. For example, both arrays and strings have a slice method. If every member in a union has a property in common, you can use that property without narrowing:</p>

![ts6](https://user-images.githubusercontent.com/77200870/188303024-a4991a52-632e-4423-b7d5-ce035356d2cb.PNG)

<br/>

### Literal Types

![ts8](https://user-images.githubusercontent.com/77200870/188303475-55407fa6-356b-413f-baac-d2294fbcd269.PNG)

<p>By themselves, literal types aren’t very valuable:</p>

![ts9](https://user-images.githubusercontent.com/77200870/188303494-6781b6d0-cea5-4b82-af33-89cda7b842f6.PNG)

<p>It’s not much use to have a variable that can only have one value!</p>

<p>But by combining literals into unions, you can express a much more useful concept - for example, functions that only accept a certain set of known values:</p>

![ts](https://user-images.githubusercontent.com/77200870/188303594-8a132a83-0fd3-4cd9-9bd7-c17036953e84.PNG)

<p>Numeric literal types work the same way:</p>

![ts1](https://user-images.githubusercontent.com/77200870/188303598-54b2d213-f6c2-4cef-a73d-204cbb32e6eb.PNG)

<p>Of course, you can combine these with non-literal types:</p>

![ts2](https://user-images.githubusercontent.com/77200870/188303627-f06c011b-8105-496b-8cab-46cf33d79caf.PNG)

<br/>

### Type Aliases
<p>We’ve been using object types and union types by writing them directly in type annotations. This is convenient, but it’s common to want to use the same type more than once and refer to it by a single name.</p>

```ts
type ID = number | string;

type ReturnType = "as-text" | "as-number"
```

<p>And for objects</p>

![ts3](https://user-images.githubusercontent.com/77200870/188304193-73b58446-149a-4a0e-a923-94fcd8aa154b.PNG)

<br/>

### Functions as Types
<p>The simplest way to describe a function is with a function type expression. These types are syntactically similar to arrow functions:</p>

![ts8](https://user-images.githubusercontent.com/77200870/188306772-b4472a27-f0bf-4100-81f5-0181a08a9d19.PNG)

>The syntax `(a: string) => void` means “a function with one parameter, named a, of type string, that doesn’t have a return value”. Just like with function declarations, if a parameter type isn’t specified, it’s implicitly `any`.

> Note that the parameter name is required. The function type (string) => void means “a function with a parameter named string of type any“!

<p>Of course, we can use a type alias to name a function type:</p>

![ts7](https://user-images.githubusercontent.com/77200870/188306694-69a61d2f-64a3-484c-aaa4-7ab921399f0a.PNG)

<br/>

### **Other Types to Know About**
#### unknown
<p>The unknown type represents any value. This is similar to the any type, but is safer because it’s not legal to do anything with an unknown value:</p>

![ts9](https://user-images.githubusercontent.com/77200870/188307405-c9bcd1e3-743f-4339-bd12-f96b91efca1d.PNG)

```ts
let userInput: unkown;
let userName: string;

userInput = 5;
userInput = 'Max'

if (typeof userInput === 'string') {
  userName = userInput;
}
```

<br/>

#### never
<p>Some functions never return a value:</p>

![ts22](https://user-images.githubusercontent.com/77200870/188307743-d8283964-2565-4a36-b059-c499a81a7ba4.PNG)

---------------------------------------------------------------------
## 0x01 - TypeScript Compiler ⚙️
### Compile the entire project at once
> tsc --init

> tsc

<br/>

### Run The Scripts In Watch Mode
> tsc --watch / tsc -w

<br/>

### Adding and excluding files
> In `tsconfig.json`, after `compilerOptions` object, we describe `exclude` or `include` arrays

> `include` and `exclude` can have files or folders, but `files` which actually behaves like `include` only has files

<br/>

### Compilation Options

**target** : target ECMASCRIPT version to compile to

**rootDir** : the folder that contains the `.ts` files

**outDir** : the folder that will contain the compiled `.js` files

**sourceMap** : generate `.js.map` files for browser debugging

**noEmitOnError** : don't compile `.ts` files to `.js` if they contains errors

**strict**

**noImplicitAny** : in function parameters make sure you specify the type of the parameters

**strictNullChecks** :
```ts
const btn = document.querySelector('button')

if (btn) // btn !== undefined && btn !== null {
  btn.addEventListener...
}
```

**noUnusedLocals**

**noUnusedParameters**

**noImplicitReturns**

------------------------------------------------------------
## Next-Generation JavaScript & TypeScript

<p>Because the TypeScript compiler can compile our code down to any JavaScipt version, we still can take advantage of the new features of JavaScript</p>

[> ECMAScript6 compatibility table](https://kangax.github.io/compat-table/es6/)

<br/>

- `let` and `const` are only available in their scope or any lower scope, `var` is only scoped in functions or the global scope
- **Default function parameters:** default arguments must come at last
```js
const add = (num1: number, num2: number = 5) => {...}
```
- **The spread operator:** we can push to constant arrays, because arrays are object refrences, and when pushing we don't change the addres
[> Reference vs Primitive Values](https://academind.com/tutorials/reference-vs-primitive-values)
```js
const hobbies = ['sports', 'cooking']
const activeHobbies = ['hiking']

activeHobbies.push(...hobbies)
```
- **Rest parameters:**
```js
const add = (...numbers: number[]) => {
  return numbers.reduce((acc, curr) => acc + curr, 0)
}

// using tuples: only accept three arguments
const add = (...numbers: [number, number, number]) => {
  return numbers.reduce((acc, curr) => acc + curr, 0)
}
```
- **Destructuring:**
```js
// array destructuring
const [hobby1, hobby2, ...remainingHobbies] = hobbies
```

---------------------------------------------------------------------------
## Classes & Objects 💡
### Fields

<p>A field declaration creates a public writeable property on a class</p>

![3](https://user-images.githubusercontent.com/77200870/188533741-972ae799-9272-45dd-b372-29c0dd6797b6.PNG)

**Note:** <p>As with other locations, the type annotation is optional, but will be an implicit any if not specified.</p>

<p>Fields can also have initializers; these will run automatically when the class is instantiated</p>

![4](https://user-images.githubusercontent.com/77200870/188533893-83d3c884-d506-407f-9244-c54d4001f197.PNG)

Just like with `const`, `let`, and `var`, the initializer of a class property will be used to infer its type

![5](https://user-images.githubusercontent.com/77200870/188534006-1c7f3d4a-8b38-4b13-88ee-a4a9ad568c1e.PNG)

<br/>

### --strictPropertyInitialization

<p>The strictPropertyInitialization setting in `tsconfig` controls whether class fields need to be initialized in the constructor.</p>

![6](https://user-images.githubusercontent.com/77200870/188534141-2465220e-e6a4-43db-a307-f83be439353a.PNG)

<p>If you intend to definitely initialize a field through means other than the constructor (for example, maybe an external library is filling in part of your class for you), you can use the definite assignment assertion operator, </p>`!`

![7](https://user-images.githubusercontent.com/77200870/188534289-2647909f-d984-4fc0-8a15-cd0e72ca5124.PNG)

<br/>

### readonly

<p>Fields may be prefixed with the readonly modifier. This prevents assignments to the field outside of the constructor.</p>

![8](https://user-images.githubusercontent.com/77200870/188534541-a32f7e57-422f-42de-b4b0-edcc999b2580.PNG)

In constructor

```ts
constructor(public readonly name: string, private code: number) {}
```

<br/>

### Constructors

<p>Class constructors are very similar to functions. You can add parameters with type annotations, default values, and overloads</p>

![9](https://user-images.githubusercontent.com/77200870/188534703-b7af9af4-f3ea-402d-9afe-6099f2dd35ce.PNG)

<p>With overloads</p>

![10](https://user-images.githubusercontent.com/77200870/188534961-8acfe55c-5791-492d-a746-870c9dc13eab.PNG)

**Short-hand inisialization**
<p>With this syntax we don't have to declare the fields then assign their initial values in the constructor, instead we do it in one go</p>

```ts
class Department {
    constructor(public name: string, private code: number) {}

    describe(this: Department) {
        console.log("Department name: " + this.name)
        console.log("Department code: " + this.code)
    }
}

const cs = new Department('computer science', 15263)
```

<p>There are just a few differences between class constructor signatures and function signatures</p>

- Constructors can’t have type parameters - these belong on the outer class declaration, which we’ll learn about later
- Constructors can’t have return type annotations - the class instance type is always what’s returned

#### Super Calls

Just as in JavaScript, if you have a base class, you’ll need to call `super()`; in your constructor body before using any `this.` members

![11](https://user-images.githubusercontent.com/77200870/188535201-4f30b644-d797-4888-8341-2d517bf6096c.PNG)

Forgetting to call `super` is an easy mistake to make in JavaScript, but TypeScript will tell you when it’s necessary.

<br/>

### Methods

<p>A function property on a class is called a method. Methods can use all the same type annotations as functions and constructors</p>

![12](https://user-images.githubusercontent.com/77200870/188535385-681990c4-7f89-472d-bfd0-eeb3e7708da1.PNG)

Other than the standard type annotations, TypeScript doesn’t add anything else new to methods.

Note that inside a method body, it is still mandatory to access fields and other methods via `this.`. An unqualified name in a method body will always refer to something in the enclosing scope

![13](https://user-images.githubusercontent.com/77200870/188535527-7aa29afd-6d80-4c31-905a-2f71c04807fb.PNG)

<p>And to be more precise about that the this keyword refers to, we can pass it as an argument to the method(it won't affect the other arguments)</p>

```ts
describe(this: Department) {
    console.log("Department: " + this.name)
}
```

> **Note:** this keyword always refers to the object it's being called on</p>

<br/>

### Access Modifiers

- private (soft privacy)

```ts
private employees: string[] = [];
```

**Note**
> Because `private` members aren’t visible to `derived `classes, a `derived` class can’t increase its visibility:

![Screenshot from 2022-09-09 16-38-15](https://user-images.githubusercontent.com/77200870/189388467-d667c367-a667-48aa-af8e-0eeb35e710f0.png)

#### Cross-instance private access
> Different OOP languages disagree about whether different instances of the same class may access each others’ private members. While languages like Java, C#, C++, Swift, and PHP allow this, Ruby does not.
>
> TypeScript does allow cross-instance private access

![Screenshot from 2022-09-09 16-39-48](https://user-images.githubusercontent.com/77200870/189388758-467afa8b-603e-4ba6-ac4f-4245f7582c02.png)

<br/>

- public

```ts
public name: string;
// same as
name: string;
```

<br/>

- protected

#### Cross-hierarchy protected access

  <p>We can access `base` class's protected fields and methods in the `derived` class.</p>

  **But,** <p>we cannot access them directly on an instance of the `derived` class.</p>
  
Different OOP languages disagree about whether it’s legal to access a protected member through a base class reference:

![Screenshot from 2022-09-09 16-29-53](https://user-images.githubusercontent.com/77200870/189386933-09448293-e3ca-438b-95c0-93179078cf7b.png)

#### Exposure of protected members

If a field is `protected` in the `base` class we cannot make it `private` in the `derived` class, but we can make it `public`

![Screenshot from 2022-09-09 16-35-29](https://user-images.githubusercontent.com/77200870/189387979-49054815-293c-41b0-a00d-98899ddef41e.png)

<br/>

### Inheritance

#### Extending classes

Classes may `extend` from a base class. A derived class has all the properties and methods of its base class, and also define additional members.

![14](https://user-images.githubusercontent.com/77200870/188539906-4365c313-69ee-4c6c-8162-672971ade27f.PNG)

Redefining the constructor of the derived class

```ts
class Department {
    constructor(public readonly name: string, private code: number) {}

    describe(this: Department) {
        console.log("Department name: " + this.name)
        console.log("Department code: " + this.code)
    }
}

class ITDepartment extends Department {
    admins: string[]

    constructor(name: string, admins: string[]) {
        super(name, 123) // a must
        this.admins = admins
    }
}

const cs = new Department('computer science', 15263)

const csIT = new ITDepartment('cyber security', ['Max'])
```

<br/>

#### Overriding Methods

A derived class can also override a base class field or property. You can use the `super`. syntax to access base class methods.

> TypeScript enforces that a derived class is always a subtype of its base class.

![1](https://user-images.githubusercontent.com/77200870/188596789-78a3f59d-f517-4b80-8a99-5d86033e63ec.PNG)

> Remember that it’s very common (and always legal!) to refer to a derived class instance through a base class reference

![2](https://user-images.githubusercontent.com/77200870/188598397-742b543a-2613-4789-9915-8031cbe00217.PNG)

**Note**
> It’s important that a derived class follow its base class contract.

What if `Derived` didn’t follow `Base`’s contract?

![3](https://user-images.githubusercontent.com/77200870/188598190-3e85656c-47b8-4be0-8605-08ce5f937914.PNG)

If we compiled this code despite the error, this sample would then crash

![4](https://user-images.githubusercontent.com/77200870/188598589-c90f85f3-882d-4ae1-a37c-6ff3443cb272.PNG)


### Protected

When a `derived` class extends a `base` class, all `private` fields in the base class won't be accessable in the `derived` class, to get over this behavior, we use `protected` instead of `private` in the base class 

```ts
class Department {
    protected employees: string[];

    constructor(public name: string, employees: string[]) {
        this.employees = employees
    }

    addEmployee(emp: string) {
        this.employees.push(emp)
    }

    displayEmployees() {
        this.employees.map((emp) => {
            console.log(emp)
        })
    }
}

class ITDepartment extends Department {
    private techs: string[]

    constructor(techs: string[]) {
        super('IT', [])
        this.techs = techs
    }

    displayEmployees() {
        this.employees.map((emp) => {
            console.log(`Employee name: `, emp)
        })
    }

    displayTechs() {
        this.techs.map((tech) => {
            console.log(`Technology name: `, tech)
        })
    }
}

const it = new ITDepartment(['NextJS', 'Express'])

it.displayTechs()

it.addEmployee('Jakob')
it.addEmployee('Houdini')
it.addEmployee('Robert')

it.displayEmployees()
```

### Getters And Setters

#### Getters
Declaration
```js
get mostRecentTech() {
    return this.lastTech
}
```
Access
```js
console.log(obj.mostRecentTech)
```

<br/>

#### Setters
Declaration
```js
set mostRecentReport(value: string) {
    this.addTech(value)
}
```
Access
```js
obj.mostRecentReport = 'TypeScript'
```

<br/>

### Static Members

Classes may have `static` members. These members aren’t associated with a particular instance of the class. They can be accessed through the class constructor object itself

![Screenshot from 2022-09-09 18-28-35](https://user-images.githubusercontent.com/77200870/189409981-daac8a15-ca3f-480c-9f4e-0aeebe335dbe.png)

> Static members can also use the same public, protected, and private visibility modifiers:

![Screenshot from 2022-09-09 18-29-23](https://user-images.githubusercontent.com/77200870/189410104-e7b5ae64-e0af-4577-a1aa-7146389afd59.png)

Static members are also inherited

![Screenshot from 2022-09-09 18-30-06](https://user-images.githubusercontent.com/77200870/189410225-84bef361-a4d3-4fd1-8f7d-5d4bea6ed611.png)

#### Special Static Names

It’s generally not safe/possible to overwrite properties from the Function prototype. Because classes are themselves functions that can be invoked with `new`, certain `static` names can’t be used. Function properties like `name`, `length`, and `call` aren’t valid to define as `static` members

![Screenshot from 2022-09-09 18-31-28](https://user-images.githubusercontent.com/77200870/189410706-b39ff844-1bc2-436c-91e4-748e0d1e09e1.png)

#### Why No Static Classes?

we don’t need a “static class” syntax in TypeScript because a regular object (or even top-level function) will do the job just as well

![Screenshot from 2022-09-09 18-34-54](https://user-images.githubusercontent.com/77200870/189410986-e555a1a4-6c21-4477-913e-eed97048d6e6.png)

#### static Blocks in Classes

Static blocks allow you to write a sequence of statements with their own scope that can access private fields within the containing class. This means that we can write initialization code with all the capabilities of writing statements, no leakage of variables, and full access to our class’s internals.

![Screenshot from 2022-09-09 18-35-34](https://user-images.githubusercontent.com/77200870/189411123-66bb870e-cedb-4b7f-b316-3eb0c0d3f63e.png)





