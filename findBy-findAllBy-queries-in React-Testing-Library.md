# `findBy*`, `findAllBy*` queries in React Testing Library

Date: Sep 15, 2020
Tags: React, Testing

The `findBy*` queries are simple combinations of `getBy*` queries and `waitFor()`. `findBy*` queries returns a promise that resolves when an element is found; the promise is rejected if no element is found or if more than one element is found. `findBy*` has a default timeout of 1000ms.

if we expect multiple elements to be found use `findAllBy*` queries, which works similarly but returns a promise that resolves to an array of elements instead

The built-in timeout comes in handy when testing async operations and components, i.e. Formik form submissions are async

```jsx
test('ShippingForm cannot be submitted empty', async () => {
    // <ShippingForm /> is a Formik form component
		render(<ShippingForm />);

    const submit = screen.getByTestId("submit-shipping-button");
    fireEvent.click(submit);
		
		// Formik form submits are async, so use findBy* and findAllBy* queries
    const shippingForm = await screen.findByTestId("shipping-form");
    expect(shippingForm).toBeInTheDocument();

    const requiredTexts = await screen.findAllByText(/required/i);
    expect(requiredTexts.length).toBeGreaterThan(0);
})
```

**References**

- [Testing Formik with react-testing-library](https://scottsauber.com/2019/05/25/testing-formik-with-react-testing-library/)
- [Testing Library - Queries](https://testing-library.com/docs/dom-testing-library/api-queries#findby)