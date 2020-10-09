# Typescript Basics

#### Online editor for testing
[TypeScript: TS Playground - An online editor for exploring TypeScript and JavaScript](https://www.typescriptlang.org/play)

### Basic Types
```ts
let isDone: boolean = false;
let decimal: number = 6;
let hex: number = 0xf00d;
let color: string = "blue";
let looselyTyped: any = 4; // To opt-out of type checking
let list: number[] = [1, 2, 3]; // Array types option 1
let list: Array<number> = [1, 2, 3]; // Array types option 2
let x: [string, number]; // Tuple: array with a fixed number of elements

function buildName(firstName: string, lastName: string): string {
  return firstName + " " + lastName;
} // buildName('ivan', 'ivanov')) 
// "ivan ivanov" - the result must be a string (params):string

// Enums allow us to declare a set of named constants
// a collection of related values that can be numeric or string values.
enum Color {
  Green = 7,
  Blue = 2,
  Red = 5,
}
let c: Color = Color.Green; // 7

// If a function does not return any value
// then you can specify void as return type.
function warnUser(): void {
  console.log("This is my warning message");
}

// Anonymous object
function greet(person: { name: string; age: number }) {
  return "Hello " + person.age;
}

// Named object - Interface
interface Person {
  readonly id: number // readonly property
  name: string
  age?: number // add '?' to make the property optional
}
function greet(person: Person) {
  return "Hello " + person.name;
}
```

### Extending Types
```ts
interface Person {
  name: string;
  age: number;
}

interface Student extends Person {
  grade: number;
}

const ivan: Student = {
  name: "Ivan",
  age: 18,
  grade: 4
};

console.log(ivan) //{ "name": "Ivan", "age": 18, "grade": 4 } 
```

### Generic type which declares a type parameters
```ts
// Instead of having:
interface NumberBox {
  contents: number;
}
interface StringBox {
  contents: string;
}
interface BooleanBox {
  contents: boolean;
}
// We can use
interface Box<T> {
  contents: T;
}

let box: Box<string> = { contents: "hello" };
let box2: Box<number> = { contents: 5 };

console.log(box.contents) // "hello" 
console.log(box2.contents) // 5
```

### Classes
```ts
class Greeter {
  greeting: string;

  constructor(message: string) {
    this.greeting = message;
  }

  greet() {
    return "Hello, " + this.greeting;
  }
}

let greeter = new Greeter("world");
```

### Inheritance 
```ts
class Animal {
  name: string;
  constructor(theName: string) {
    this.name = theName;
  }
  move(distanceInMeters: number = 0) {
    console.log(`${this.name} moved ${distanceInMeters}m.`);
  }
}

class Dog extends Animal {
  constructor(name: string) {
    super(name);
  }
  move(distanceInMeters = 5) {
    console.log("Running...");
    super.move(distanceInMeters);
  }
  bark() {
    console.log("Woof! Woof!");
  }
}

let rex: Dog = new Dog("Rex");

rex.move();
rex.bark()
```

### Some examples

```ts
let fullName: string = `Joe Black`;
let age: number = 37;
let sentence: string = `I am ${fullName}. I'll be ${age + 1} years old next month.`;
console.log(sentence) // "Hello, my name is Joe Black. I'll be 38 years old next month." 
```

```ts
let x: [string, number];
x = ["hello", 10]
console.log(x[0].substring(1)); 
console.log(x[1].substring(1)); //ERROR: Property 'substring' does not exist on type 'number'.
x[3] = "world"; //ERROR: Tuple type '[string, number]' of length '2' has no element at index '3'.
```

```ts
interface Person {
  name: string;
  age: number;
}

interface ReadonlyPerson {
  readonly name: string;
  readonly age: number;
}

let writablePerson: Person = {
  name: "Gosho",
  age: 18,
};

let readonlyPerson: ReadonlyPerson = writablePerson;

console.log(readonlyPerson.name); // Gosho
writablePerson.name = "Ivan"
console.log(readonlyPerson.name); // Ivan

console.log(readonlyPerson.age); // 18
writablePerson.age++;
console.log(readonlyPerson.age); // 19
```
