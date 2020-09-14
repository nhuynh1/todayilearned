# Use waitFor when testing Formik forms

Date: Sep 14, 2020
Tags: React, Testing

**Problem:** Methods called by Formik onSubmit appear not to be called when testing with Jest

```jsx
// Truncated code
test('setValues is called when submitting', () => {
	const setValues = jest.fn();
	render(<MyForm />);
	fireEvent.click(screen.getByTestId("submit-button"));
	expect(setValues).toHaveBeenCalledWith(shippingValues);
})
```

With the above test Jest tells us that setValues has been called 0 times, even though when manually testing I can see that it has been called after clicking on the submit button

**Solution:** Use `waitFor()` in React Testing Library

```jsx
// Truncated code
test('setValues is called when submitting', async () => {
	const setValues = jest.fn();
	render(<MyForm />);
	fireEvent.click(screen.getByTestId("submit-button"));
	await waitFor(() => {
		expect(setValues).toHaveBeenCalledWith(shippingValues);
	});
})
```

**Note:** `waitFor()` is an async utility, hence the use of `async` and `await`. Should also be able to use `then` and the `done()` function from Jest, since `waitFor()` returns a Promise

**References**

- [Testing Library - Async Utilities](https://testing-library.com/docs/dom-testing-library/api-async)