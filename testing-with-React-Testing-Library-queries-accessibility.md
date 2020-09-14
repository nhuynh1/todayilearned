# Testing with React Testing Library queries helps make apps more accessible

Date: Sep 14, 2020
Tags: React, Testing

Unlike Enzyme where finding an element is typically done using css queries for say the class, id, or element type, using React Testing Library's built in querying methods limits the ways elements can be found. `getByLabelText()` is particularly helpful to ensure form elements are properly labeled.

```jsx
// Example of finding an input element with Enzyme
// We won't know from this test if the input has a proper label for accessibility
const firstNameInput = wrapper.find('input.firstName');
```

```jsx
// Example of finding an input element with React Testing Library
// If the input isn't labeled then this will throw an error indicating there's no element with that label
// With getByLabelText, regex can also be used to provide looser search
const firstNameInput = screen.getByLabelText(/first name/i);
```

**References**

- [Testing Library Queries](https://testing-library.com/docs/dom-testing-library/api-queries)
- [Testing Library: Which query should I use?](https://testing-library.com/docs/guide-which-query)
- [Enzyme vs. react-testing-library: A mindset shift](https://blog.logrocket.com/enzyme-vs-react-testing-library-a-mindset-shift/)