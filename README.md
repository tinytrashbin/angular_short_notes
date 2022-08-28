# Learning Angular by Examples

### 1). Creating a new project

Start by git-cloning [this repo](https://github.com/tinytrashbin/angular_examples).

Note: Remove `.git` file after cloning, and do `git init`.

In the root folder, run `npm install` and then run `npm start` to start the server.

Try editing HTML content in `src/app/example1/example1.component.html` and see if the change shows up.

-----------------------------------

### 2). Creating a new state variable in a component:

- Component class members are state variables as well.


For example1, we can make it like this in **`example1.component.ts`** file:

```ts

export class Example1Component implements OnInit {
  counter: number = 1
  constructor() { }
  ngOnInit(): void {
  }
}
```

`counter` is the state variable of type `number`, with default value = 1.

Note: since we are using typescript, we need to specify the type of variables.

We can use this variable in HTML part of this component:

**File: `example1.component.html`**

```HTML
<p>example1 counter value = {{counter}} </p>

```

Similar to AngularJS-1, we can use variables or expressions inside `{{...}}` in HTML part.

For example: `<p>There are total of {{3 + 4}} people.</p>`

In React, we use `{...}`, like this: `<p>There are total of {3 + 4} people.</p>`.

-----------------------------------

### 3). Inline Style

|  .  | .
| -------- | -----------
| React Syntax | `style={dict_expression}`
| React Example | `style={{color: "red", fontSize: "14px"}}`
| React Example | `style={{color: (is_red ? "red" : "blue"), fontSize: "14px"}}`
| AngularJS-1 Syntax |  `ng-style="dict_expression"`
| AngularJS-1 Example1 |  `ng-style="{'color': 'red', 'font-size': '14px'}"`
| AngularJS-1 Example2 |  `style="color: red; font-size: 14px;"`
| Angular-14 Syntax |  `[ngStyle]="dict_expression"`
| Angular-14 Example1 |  `[ngStyle]="{'color': 'red', 'font-size': '14px'}"`
| Angular-14 Example2 |  `style="color: red; font-size: 14px;"`
| Angular-14 Example3 |  `[ngStyle]="{'color': (is_red ? 'red': 'blue'), 'font-size': '14px'}"`
| Angular-14 Example4 |  `[ngStyle]="{'color': color_variable, 'font-size': '14px'}"`


Example:

```HTML
<p [ngStyle]="{'color': 'red'}" ></p>
```

-----------------------------------

### 4). OnClick

React Syntax:

1). Function without arguments: 

```JSX
<button onClick={func1_name} >Button1</button>
```

2). Function with arguments:

```JSX
<button onClick={() => func2_name(x, y)} >Button2</button>
```

AngularJS-1 Syntax:

```HTML
<button ng-click="func1_name()" >Button1</button>

<button ng-click="func2_name(x, y)" >Button2</button>
```

Angular-14 Syntax:

```HTML
<button (click)="func1_name()" >Button1</button>

<button (click)="func2_name(x, y)" >Button2</button>
```

**AngularJS-1**

```HTML
<!DOCTYPE html>
<html>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
<body ng-app="myApp" ng-controller="myCtrl" >
  <div>
    <div><button ng-click="func1_name()" >Click1</button> </div>
    <div><button ng-click="func2_name(4, 5)" >Click2</button> </div>
  </div>
<script>
  var app = angular.module('myApp', []);
  app.controller('myCtrl', function($scope) {
    $scope.func1_name = function() {
      alert("Abc")
    }

    $scope.func2_name = function(x, y) {
      alert("Abc " + x + "," + y)
    }
  });
</script>
</body>
</html>
```

**[Angular-14] File: example1.component.html**

```HTML
  <div>
    <div><button (click)="func1_name()" >Click1</button> </div>
    <div><button (click)="func2_name(4, 5)" >Click2</button> </div>
  </div>
```

**[Angular-14] File: example1.component.ts**

```ts
export class Example1Component implements OnInit {
  constructor() { }
  ngOnInit(): void {
  }
  func1_name(): void {
    alert("Abc")
  }

  func2_name(x: number, y: number): void {
    alert("Abc " + x + "," + y)
  }
}
```

------------------

### 5). Conditionals / ng-if

React Syntax: `{condition && <div>....</div>}`

AngularJS-1 Syntax: `<div ng-if="condition" >....</div>`

Angular-14 Syntax: `<div *ngIf="condition" >....</div>`


**AngularJS-1**

```HTML
<!DOCTYPE html>
<html>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
<body ng-app="myApp" ng-controller="myCtrl" >

<div >
  <ul ng-if="show_fruits">
    <li>Apples</li>
  </ul>
</div>

<script>
  var app = angular.module('myApp', []);
  app.controller('myCtrl', function($scope) {
    $scope.show_fruits = false
  });
</script>
</body>
</html>
```

**[Angular-14] File: example1.component.html**

```HTML
<div >
  <ul *ngIf="show_fruits">
    <li>Apples</li>
  </ul>
</div>
```

**[Angular-14] File: example1.component.ts**

```ts
export class Example1Component implements OnInit {
  show_fruits: boolean = false
  constructor() { }
  ngOnInit(): void {
  }
}
```

-----------------------------------


### 6). Map / ng-repeat / `*ngFor`

React Syntax: `{list.map((x) => <div>...{x}...</div>)}`

React Syntax (with key): `{list.map((x) => <div key={some_unique_id} >...{x}...</div>)}`

AngularJS-1 Syntax: `<div ng-repeat="x in list" >...{{x}} .</div>`

Angular-14 Syntax: `<div *ngFor="let x of list" >...{{x}} .</div>`

**AngularJS-1**

```HTML
<!DOCTYPE html>
<html>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
<body ng-app="myApp" ng-controller="myCtrl" >
  <div ng-repeat="fruit in fruits" >
    I like <b>{{fruit}}</b>
  </div>
<script>
  var app = angular.module('myApp', []);
  app.controller('myCtrl', function($scope) {
    $scope.fruits = ["Apple", "Banana", "Orange"]
  });
</script>
</body>
</html>
```


**[Angular-14] File: example1.component.html**

```HTML
<div *ngFor="let fruit of fruits" >
  I like <b>{{fruit}}</b>
</div>
```

**[Angular-14] File: example1.component.ts**

```ts
export class Example1Component implements OnInit {
  fruits: string[] = ["Apple", "Banana", "Orange"]
  constructor() { }
  ngOnInit(): void {
  }
}
```

-----------------------------------


### 7). Changing state on click


**[Angular-14] File: example1.component.html**

```HTML

<p>counter = {{counter}}</p>

<button (click)="incr()" >Increase</button>
```

**[Angular-14] File: example1.component.ts**

```ts
export class Example1Component implements OnInit {
  counter: number = 1
  constructor() { }
  ngOnInit(): void {
  }
  incr(): void {
    this.counter += 1
  }
}
```

Note: state variables (class members) are accessed with `this.` , For example `this.counter` in `incr` function.

-----------------------------------

### 8). ng-Model / double-binding with input

AngularJS-1 Syntax: `ng-model="name" `

Angular-14 Syntax: `[(ngModel)]="name" `


**[Angular-14] File: example1.component.html**

```HTML
<input [(ngModel)]="name" />
<br> name = {{name}} <br>
<button (click)="reset()" >Reset</button>
```

**[Angular-14] File: example1.component.ts**

```ts
export class Example1Component implements OnInit {
  name: string = "Initial Value"
  constructor() { }
  ngOnInit(): void {
  }
  reset(): void {
    this.name = "Original value"
  }
}
```

-----------------------------------

### 9). API call:

API Call Syntax:

```ts
this.http.get<any>('https://fakestoreapi.com/products').subscribe(backend_output => {
  console.log(backend_output)
})
```

#### How to execute something when a component loads:

Put inside `ngOnInit`


#### How to call an API when a component loads:

```ts
export class Example1Component implements OnInit {
  products: any[] = []
  constructor(private http: HttpClient) { }
  ngOnInit(): void {
    this.http.get<any>('https://fakestoreapi.com/products').subscribe(backend_output => {
      this.products = data
    })
  }
}
```

#### How to call an API when a button is clicked:

**[Angular-14] File: example1.component.html**

```HTML
<button (click)="get_all_products()" >Show All Products</button>

<div *ngFor="let product of products" >
  product title = {{product.title}}
</div>
```

**[Angular-14] File: example1.component.ts**

```ts
export class Example1Component implements OnInit {
  products: any[] = []
  constructor(private http: HttpClient) { }
  ngOnInit(): void {
  }

  get_all_products(): void {
    this.http.get<any>('https://fakestoreapi.com/products').subscribe(backend_output => {
      this.products = backend_output
    })
  }
}
```

-----------------------------------

### 10). Subcomponents, passing values to subcomponents

**[Angular-14]**: How to use a subcomponent in HTML of another component:

```HTML
<app-sub-example></app-sub-example>
```

**[Angular-14]**: How to pass values to a subcomponent:

```HTML
<app-sub-example [name]="name" [email]="email" ></app-sub-example>
```

**In ReactJS**: How to pass values to a sub component.

```JSX
<AppSubExample name={name} email={email} />
```

**[Angular-14]**: How to use the values passed in subcomponent:

**File: sub-example.component.ts**

```ts
export class SubExampleComponent implements OnInit {
  @Input("name") name!: string
  @Input("email") email!: string

  constructor() { }
  ngOnInit(): void {
  }
}
```

**File: sub-example.component.html**

```HTML
<p>My name = {{name}}, and email = {{email}}</p>
```

**In ReactJS**: How to use the values passed in subcomponent:

```JSX
function AppSubExample({name, email}) {
  return (<p>My name = {name}, and email = {email}</p>);
}
```

-----------------------------------

### 11). Passing EventEmitter to subcomponents

EventEmitter is used by child components for changing state variables of parent component. In ReactJS we pass callback/function to the child component for this purpose.

For example, we pass `deleteUser` function (callback), which is defined in
the parent component but called in child component.

```JSX
// ReactJS
function AppSubExample({name, email, deleteUser}) {
  ...
}
```

In Angular-14:

**File: parent.component.html**

```HTML
<app-sub-example [name]="name" (deleteUser)="deleteUser($event)" ></app-sub-example>
```

**File: parent.component.ts**

```ts
  deleteUser(name: string): void {
    ...
  }
```

**File: child.component.html**

```HTML
<input [(ngModel)]="name" >
<br>
<button (click)="deleteUser.emit(name)" >Delete</button>
```

**File: child.component.ts**

```ts
import { Component, OnInit, Input, Output, EventEmitter} from '@angular/core';

...
export class SubExampleComponent implements OnInit {
  @Input("name") name!: string
  @Output("deleteUser") deleteUser = new EventEmitter<string>();

  constructor() { }
  ngOnInit(): void { }
}
```

Note: Event emitters should be initialized to `new EventEmitter<string>()`

**In ReactJS**


```JSX
function AppSubExample({deleteUser}) {
  return (
    <p>
      <button onClick={() => deleteUser("Abc")} ></button>
    </p>)
}

function MainFunc() {
  const deleteUser = function(name) {
    ...
  }
  return <p><AppSubExample deleteUser={deleteUser} /></p>
}
```

Differences:

|  React  | Angular-14
| -------- | -----------
| Callbacks are passed like other variables | Passed differently
| Syntax: `deleteUser={deleteUser}` | Syntax: `(deleteUser)="deleteUser($event)"`
| Callback functions can take any number of args | Can take only 1 argument.
| Used in subcomponents like other variables | Used in subcomponent with `@output` annotation
| Eg: `function AppSubExample({deleteUser})` | Eg: `@Output("deleteUser") deleteUser = new EventEmitter<string>()`
| Called directly as `deleteUser("Abc")` | Called `.emit` on it, eg: `deleteUser.emit("Abc")`

Note:

1. In ` = new EventEmitter<string>();` , the `string` is the data type of input param. It will be different for different callbacks.

2. Since event-emitter can take only 1 argument, we must call it with tuple or dictionary if we need to pass multiple parameters.

-----------------------------------

