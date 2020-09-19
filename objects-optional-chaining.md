# Objects optional chaining (?.)

Date: Sep 18, 2020
Tags: JavaScript

**Problem**

Accessing a nested object property where the reference is missing throws an error and breaks the code

```jsx
const people = [
	{
		name: "Larry",
		pet: {
			name: "Mittens"
		}
	},
	{
		name: "Moe"
	}
];

people.forEach(person => {
	console.log(person.name);
	console.log(person.pet.name); // throws error!
})
```

**Previous solution**

Check if the reference exists and then try to access the property

```jsx
people.forEach(person => {
	console.log(person.name);
	person.pet && console.log(person.pet.name); // check that pet exists first
})
```

**New solution**

Use optional chaining `(?.)`. Instead of  throwing an error, it returns undefined, and all it took was adding a question mark!

```jsx
people.forEach(person => {
	console.log(person.name);
	console.log(person.pet?.name); // optional chaining
})
```

I saw optional chaining used in a gatsby starter template and was seriously mindblown. 🤯

**Caveat**

This is pretty new so it hasn't reached cross-browser stability. Best to use this with babel support via [@babel/plugin-proposal-optional-chaining](https://babeljs.io/docs/en/babel-plugin-proposal-optional-chaining)

**Reference**

- [Optional chaining (?.)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)
