The Road To Learn React

- [ES6](#ES6)
    - [Const Let,](#ConstLet,)
    - [Arrow Functions](#ArrowFunctions)
    - [Class](#Class)
    - [Destructuring assignment syntax](#Destructuringassignmentsyntax)
    - [… Spread Operator](#…SpreadOperator)
    - [Arrays](#Arrays)
    - [Higher Order Functions in JavaScript](#HigherOrderFunctionsinJavaScript)
    - [Object Initializer](#ObjectInitializer)
- [React](#React)
    - [Why I want to Learn React](#WhyIwanttoLearnReact)
    - [A first touch on React](#AfirsttouchonReact)
    - [Code Conventions](#CodeConventions)
    - [ReactDOM](#ReactDOM)
    - [Hot Module Reloading [HMR]](#HotModuleReloading[HMR])
    - [Immutability](#Immutability)
    - [Functional Components](#FunctionalComponents)
    - [Class Based Components](#ClassBasedComponents)
    - [Lifecycle Methods](#LifecycleMethods)
    - [JSX](#JSX)
    - [Rendering Elements](#RenderingElements)
    - [Props](#Props)
    - [State](#State)
    - [Event Handlers](#EventHandlers)
    - [Bindings](#Bindings)
    - [Passing arguments](#Passingarguments)
    - [Conditional Rendering](#ConditionalRendering)
    - [Lists & Keys](#Lists&Keys)
    - [Forms](#Forms)
    - [Lifting State Up](#LiftingStateUp)
    - [Composition VS Inheritance](#CompositionVSInheritance)
    - [Containment](#Containment)
-  [Think in React](#ThinkinReact)

# ES6 
## Const Let, 
Use const whenever possible and recreate an object instead of updating it (Pure Programming)
## Arrow Functions
-   Arrow functions can have 2 sorts of bodies:
    - Concise Block - is when there is a expression described in this case there is no return statment needed, an expression has an implicit return statement
    in our case a piece of JSX is returned which is an expression

        `(x) => x* 2` 
    - Code Block - Has multiple expressions and brackets this will need an explicit return statement

        `(x) => { 
        console.log(x)
        return x* 2
    }`

## Class
-   in ES6 a listener in a function on the class            
    - Destructuring assignment syntax - is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.
## … Spread Operator
Spread syntax allows an iterable such as an array expression or string to be expanded in places where zero or more arguments (for function calls) or elements (for array literals) are expected, or an object expression to be expanded in places where zero or more key-value pairs (for object literals) are expected.

## Arrays
- Array.concat →
- Array.slice() → 
    gives back a shalow copy of the array in a new array. You can define from where until where in the array you want a copy from. This is a good practice for developing with Immutability in mind.
- Array.concat() → 
    Use concat instead of push for immutability. Concat merges 2 arays and result into a new arraty which leaves the initial array intact
- Array.map() → 
    method creates a new array with the results of calling a provided function on every element in the calling array.
- Array.reduce() → 
    method executes a reducer function (that you provide) on each member of the array resulting in a single output value.
- Array.filter() → 
    method creates a new array with all elements that pass the test implemented by the provided function and returns true.
- Array.includes() → 
    method determines whether an array includes a certain value among its entries, returning true or false as appropriate.

## Higher-Order Functions in JavaScript
- One of the characteristics of JavaScript that makes it well-suited for functional programming is the fact that it can accept higher-order functions. 
- A higher-order function is a function that can take another function as an argument, or that returns a function. 
Example:
    ```
    this.state.list.filter( externalFunction(paramstoBePassedToFilter) )
    ```

    -   this function needs a function which returns a boolean true or false.
    -   If we want to filter a list of items in a search field we have a few options.
    -   You can write everything inside the render function and have access to everything
    -   You can write everything inside a class method and have access to everything
    -   Keeping components small and do as less as possible  we could create an external function or even use a function from a library we use. The problem arises that we would not have access to the state of the class because we are outside the component. We can solve this with:
    ``` 
    function externalFunction(paramstoBePassedToFilter) {
        return function (currentFilterItem) {
            return someBooleanCondition
        }
    }
    ```
    -   We have access to both the paramstoBePassedToFilter and currentFilterItem

## Object Initializer
When the propertie has the same name as the value you want to assign you only have to write it once 
```
const obj = { id, name: “tom”}
const obj = { id: id, name: “tom } 
```

Same goes for functions you can drop the : function like so:
```
getUsername: function(user) { }
getUsername(user) { }
```
Computed Properties let u use a dynamic name:
```
let key = ‘name’;
Const obj = { [key]: ‘tom’	
```

# React
## Why I want to Learn React

## A first touch on React
- a component takes in parameters called props, and returns a hiearchie of views to display via render()
- The render() returns a description of what you want to see on the screen render() returns a React Element
- passing props into components is how data flows in React apps, from parent to child
- think in description, I want on onClick so I write that, but don’t be bothered how React handles the event
- Make sure to return functions in a event (see Event Handlers)
- React components can have private state by assigning in the constructor this.state = 
- Components with a constructor should first call super(props) to have access to props in the constructor
- By calling this.setState() we create a request to update state, this will automaticaly triger the render() function to rerender including its child components
- Passing data to siblings is done via container components, where you declare a shared state in the container. The parent passes data via props which keeps the parent, children , syblings in sync.
- Because state is private we can’t just update the state of the parent. Therefor we need to assign a function on the parent which get passed via props to the children so they can call that function to update the parent state update parent state → rerender parent → rerender children → all in sync now

## Code Conventions
Use on[`Handler`] & on[`Event`]
- Always start component names with a capital,  React treats lowercase tags as DOM elements
- React events are named using camelCase 

## ReactDOM
- ReactDOM.Render(JSX, DOMNode) expects 2 arguments:
    - The first is the JSX it needs to render → example <App />
    - The second specifies the place in the DOM to render the JSX
- You can call `ReactDOM.Render()` multiple times in an application, for example when you are working with an old code base you could replace 2 parts in the app with React and render each Component seperate.
- A full React app wiil call RactDOM.Render() only one time  in the root 
- ReactDOM escapes values in JSX which prevent XSS, everything is converted to string.

## Hot Module Reloading [HMR]
A standard server wil refresh the page where HMR will refresh the UI without refreshing the page.

For example you are developing step 6 in a screenflow, with HMR you would only refresh step 6 where the server will refresh the page and you have to start over from step 1.

Add the following to your root index.js file:

```
If (module.hot) { module.hot.accept() }
```

## Immutability
In the end it has the same result, render an updated version of the screen with the new data from this.state & this.props.
- Benefits
    - Having the previous data in case of an undo
    - Beter determin when to rendens a new array

## Functional Components
- These are dumb components without state and only a render() function.
- Its’s a function which receives props and returns a React Element
- Use a functional component when when you don’t use state or lifecycle methods 
- Good practice is to use destructuring in the signature of your Function so you only have to pass the props object.
function user( { name, sex, id  } ) { }
- To enforce props as input and JSX as outmut make sure to write a closing tag of the root element you return as JSX

## Class Based Components
- Extend from React.Component which has extra features like state and class methods.
- setState
    - tells React to rerender itself including it’s children.
    - Primary method to update UI
    - Think more as a request , React decides when it’s the best time to update the UI, things can be batched.
    - The first argument is an updater Function to update the state. updaterFunction(state, props) => stateChange
    - Changes should be based on building a new object based on state and props
    - The constructor is the only place where you can use this.state = instead of setState()
- defaultProps
    - Used to set defaults for props when they are onmittend 
    ```
    .defaultProps = { color: “blue” };
    
    <Button id=”1” onClick={ (this.onChange) }  color=”red”/> 	→ will be red
    
    <Button id=”1” onClick={ (this.onChange) } /> 		→ will be blue

- displayName
    - Only used for debugging and is a string 

### Lifecycle Methods
#### render() → 
- When called it examines this.props & this.state
- Should be a pure function → don’t modify state and NO interaction with the DOM
- Interaction with the dom should be done in componentDidMount()
- Will not be invoked when shouldComponentUpdate() fails → returns false
#### constructor(props)  → 
- If you don’t use state or lifecycles don’t use a constructor (see Functional Components)
- Will be called before getMounted()
- Always call super(props) first to have access to the props in the constructor
- Only use to:
    - Initialize local state and default values
    - Binding eventHandlers to this
- Is the only place wher you can directly change state with this.state = instead of using setState()
- Avoid assigning props to state in the constructor, you will have both in the component so there is no benefit
#### componentDidMount() → 
- Initialization that needs DOM 
- Initialization of requests or subscriptions
- You May call setState() but it’s better to setup defaults in the constructor then. When doing this here it will retrigger a rerender but before the browser updates the screen. Even when render is called twice the user won’t notice it, but beware of  performance
#### componentDidUpdate() → 
- Invoked immidiatly after update but not when the component is initialy rendered
- Operate the DOM here after updates
- You can do requests and subscriptions but make sure to compare this.props with this.prevProps to avoid useless requests
- You can setState() her but it should be wrap it in a condition or you get an infinite loop
#### componentWillUnmount() → 
- Before component gets unmount and then destroyed
- Place to kill requests, subscriptions, timers → things created in componentDidMount() 
- Don’t call setState(), the component will not get rerendered and will be destroyed after unmount

## JSX
- JSX is descriptive en results in a React element which describes what to render.  
    - In the back this result in a function call to:
    React.createElement(‘div’, { className: ‘test’ } )
- You can add any JavaScript expression to JSX
- In JSX the returned element is specified in the Render Function
- The component = the declaration not ussage
- The instance is a representation of the componentand is build out of elements
- Split lines for readability and wrap them in parenthese () to avoid automatic semicolon insertion from editors.
- Don’t use Quotes around Currly Brackets “{}” 
Quotes =“string here” 
- Currly Braces ={JS expression goes here}
- Use camelCase properties like className,  tabIndex, …
- If a tag is empty you can self-close it, <App />,   `<span />`, …
- Keep in mind that you can use the .map() function as well in JSX
## Rendering Elements
- An element describes what you will see on the screen const 

`el = <h1> HELLO WORLD! </h1>;`

- React objects are plain JavaScript objects and cheap
- ReactDOM takes care for this to match it to the DOM
- React Elements are immutable

## Props
- Components are like JS functions, they accept input(props) and return a React element which describes what to appear on the screen
- Props are read-only
- props.children holds the elements that are nested inside the host
## State
- Create a constructor with arg props 
- Call super(props)
- set initial state and values with `this.state = {id: 3}`
- By calling `this.setState()` we create a request to update state, this will automaticaly triger the `render()` function to rerender including its child components
- Never use state and props here to calculate the new state. Instead you can pass a function to setState which takes the prevState & prevProps as arguments
- When calling setState(), React merges the provide object into the current state. You can use it multiple times in multiple places in a class. This results  in shalow copieng, where we only change the stateProp we passed to that particular setState() FN

## Event Handlers
- React events are named using camelCase 
- Event Handlers in JSX need a function as an argument not a function call. This will not work because the function will be called on render and when you click nothing happens.
````
    <button onClick={this.onChange()} />  // no go 
    <button onClick={this.onChange} />    // works fine
````
- Keep in mind that React uses Synthetic Events 
- You can not return false to prevent default behaviour, you have to call PreventDefault()
- No need to use addEventListener  just provide an Listener when the component initialy renders, in ES6 a listener in a function on the class but make sure to bind in the constructor (see Bindings)

### Bindings
- To be able to use the class methods in your instance and have access to this.state & this.props 
you have to bind the class methods in the constructor function. 
    - you could also bind in the render function but FB keeps it at the constructor.
    
    ```
    constructor(props) { 
        super(props);
        this.state = { list, searchTerm: '', };
        this.onSearchChange = this.onSearchChange.bind(this); 
    }
    ```

### Passing arguments
There is an exception when you need to pass arguments, you could sneek in the params by wrapping it in another function, this can be done with
- Arrow FN.
```
    <button onClick={ this.onChange(arg) } />           // no go 
    <button onClick={ ( ) => this.onChange(arg, e) } /> // works fine
```

- Prototypical binding
```
    <button onClick={ this.onChange(arg) } />            // no go 
    <button onClick={ this.onChange.bind(this, arg) } /> // works fine
```

## Conditional Rendering
### With logical && operator
```return { list.length > 0 && <h1> HELLO WORLD </h1> } ```

This will work because:
- True && expression → evaluetes to expression
- False && expression → evaluetes to false
Therefor if true the h2 element will be returned rendered

### Inline If-Else with conditional operator
``` <div>The user is <b>{ isLoggedIn ? ' ' : 'Not' }</b> logged in. </div> ```

### Prevent component rerender
- To prevent the rendering of a component return NULL instead of the render output
- Returning null has no impact on the LifeCycle methods
``` If ( !props.someProp ) { return nulll } ```

## Lists & Keys
- When rendering a list React needs a unique Key to determin each element in the list
- Key is a reserved word
- Key is not accessible via the component state → this.state.Key is not accessible 
- Key must be unique between siblings, does not have to be unique in the whole app 
- Make sure to use proper key’s, restructure your data even or use a lib like UUID
- To transform lists in React we use a .map() function, which results in multiple components.
```
    const nrs = [ 1, 2, 3 ];
    const listOfElements = nrs.map( (nr, index) => {
        <li key=”index”> { nr } </li>	
    } )
    <ul>{ listOfElements }</ul>   	// listOfElements will trigger the .map()
```


-   A better approach would be to create a basicList component which accepts an array and outputs a list of elements. Now this component can  be used everywhere to render a list of elements. 
- You could also skip the basicList component and just use the .map() function in JSX itself
Helps react to uniquely indentifie elements in a list
- A last help would be to use the index, this is also the default behaviour if the Key is onmitted, but is a bad practice and React will show a warning in the console
- Only makes sense in the context of an Array → dont put the key on the list Item but in the List itself
- A good rule of thumb is when using a .map() use a Key
- Key’s are never passed to the component but if you really need it in your component you can pass it as an extra prop

    - ```<Post key={ post.id } id={ post.id } /> ``` 
    → prop.key is not available but you have the same effect now and using the key as an id for your element

## Forms
- In plain HTML forms the Submit triggers a new page. To avoid this and handle the userdata ourselves we use a technieque called Controlled Components 
- Form
    - With controlled components we write our own eventHandler based on the component Event.
- TextArea
    - Defines text by its children, 
    - in React it has a Value propery. This gives the possibility to write it the same as a single line form by writing  our own handlers en get set the value propertie to our state.

### SelectTag
- Normaly you use the selected attribute on an <option> element. 
- React has a Value propertie on the select tag.

    - ``` this.setState({ value: ‘coconut’ });```

    will set the selected attribute on the coconut.
- You could also pass an arry to have multiple selected options
Handling multiple inputs
- When handling multiple controlled inputs you can add a name attribute to each element and let the handler function handle each elements value. You can use the Computed Propertie Names syntax
    - ```.setState( { [ name ] : value })```

### Controlled Input NULL value
- Specifieng the value propertie on a controlled component prevents the user to change it. If it’s still editable cthen check if you didn’t set to null or undefined.

## Lifting State Up
- Sharing state is accomplished by moving it up to the closest common ancestor. Props are read-only so the child can’t update the parent state. To solve this issue in React we can make the child controlled. This means that we add a changHandler in the parent which the child can call via this.props.handleChange and gets it’s other props as well.
- Step-By-Step
    - Replace the state.prop to props.prop → it will come from the parent
    - Instead of calling setState() in the child call the 
    
        `this.props.handleChangeFunction`

    - In the parent add the lifted state to the parent state in the constructor 
    - There should be a single truth for data in a React Application

## Composition VS Inheritance
### Containment
- Some components don’t know their children upfront. Recommended is to use the `props.children` to pass children directly. Like <slot> it will render the nested elements which are stored in `props.children`.
- You could also name them if you want more holes in your template.

### Inheritance
- Sometimes we think we need inheritance but we don’t, we can solve this with React & Composition.
- Example:
    - We could create a Dialog component which gets a message and title via props. Then we could create a WarningDialog or WelcomeDialog component and use the Dialog component in the render as a child and pass the props and do changes based on each Dialog Type
- Same goes for Class based components
- Don’t use Inheritance 
- To reuse non-UI functionality between components extract it into a JavaScript Module

# Think in React
Start with a `Mock` and a `JSON Structure`. 
- Break the UI into a Component Hierarchy
    - Draw some boxes in the mock to define components and name them
    - Use the “Single Responsibility Principle” a component should only do one thing otherwise break it into more components.
- Build a static version in React
    - Create Functional  components not Class based yet we are making a static version. Witch gets props as input and renders React elements
    - Don’t use state it’s not available in Functional Components
    - Use Composition and props and only write a render function
    - The root component adds the JSON data as a prop
- Identify the minimal but most complete representation of the UI State
    - First think of the minimal set of mutable state
    - To define if a component needs state ask these questions:
        - Is it passe in via a parent and props?
        - Does it remain unchanged over time?
        - Can you compute it based on the other state or props?
    - If you answer Yes to these questions you can create a functional component.

- Identify where your state should live
    - We defined the minimal state now
- Next we need to know which components mutate it
- For each State  in your App
    - Identify each component that renders something based on the state
    - Find a common ancestor component
    - Or the common ancestor or a component higher up the component hierarchy should own the state
    - If you can’t find a new component where it makes sense to hold the state then create a new component to just own that state and add it above the common ancestor component
- Add inverse Data Flow
    - Now everything is rendered via props
    - Now lift state up where needed 
    - Refactor to functional components if possible 

# Testing
For testing you have to digg around because all the docs refer to each other. We will need the following tools:
- test runner - *Jest* - [https://jestjs.io/docs/en/expect](https://jestjs.io/docs/en/expect)
- testing utility - *Enzyme* - [https://airbnb.io/enzyme/](https://airbnb.io/enzyme/)

To construct you will need to build it up as followed:
[jest](enzyme ).[jest] 
expect(wrapper).toBeTruthy();