# Creating a JavaScript object with an anonymous constructor function

Date: Sep 16, 2020
Tags: JavaScript

**Problem**

Creating an object literal where one property value depends on another property value is not possible because the object has not yet been initialized

```jsx
const myName = {
	firstName: "bunny", 
	title: "dr.", 
	fullName: myObj.title + myObj.firstName
};
// Uncaught ReferenceError: Cannot access 'myName' before initialization
```

**Solution**

A quick and dirty solution (although I'm not sure this is the best) is to create an anonymous function constructor. Normally an object constructor function is reusable to create multiple objects, but in this case we only want one object, so we can just use an anonymous function

```jsx
const myName = new function() {
	this.firstName = "bunny";
	this.title = "dr.";
	this.fullname = `${this.title} ${this.firstName}`;
}(); // the () is to avoid linting warnings

console.log(myName);
// {firstName: "bunny", title: "dr.", fullname: "dr. bunny"}
```

**Alternatively**

Initialize the object and then add properties that rely on the initial properties

```jsx
const myName = {
	firstName: "bunny", 
	title: "dr."
};

myName.fullname = `${myName.title} ${myName.firstName}`;

console.log(myName);
//{firstName: "bunny", title: "dr.", fullname: "dr. bunny"}
```

Or use [getter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get) functions

```jsx
const myName = {
	firstName: "bunny", 
	title: "dr.",
	get fullName() {
		return `${this.title} ${this.firstName}`
	}
}

console.log(myName);
// {firstName: "bunny", title: "dr."}
// notice fullName is not a property

console.log(myName.fullName);
// dr. bunny
```

**References**

- [JavaScript Constructor Function](https://www.programiz.com/javascript/constructor-function)
- [Missing '()' invoking a constructor](http://linterrors.com/js/missing-invoking-a-constructor)
- [Self-references in object literals / initializers](https://stackoverflow.com/questions/4616202/self-references-in-object-literals-initializers?lq=1)