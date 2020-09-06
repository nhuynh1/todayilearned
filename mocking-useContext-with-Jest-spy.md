# Mocking useContext with Jest spy

Date: Sep 6, 2020
Tags: React, Testing

## Create custom hook that uses useContext; use the custom hook in component

In order to mock useContext first create a custom hook that uses useContext with the context being used

```jsx
// AppContext.js

import React, { useContext } from 'react';

const AppContext = React.createContext();

export const useAppContext = () => useContext(AppContext); // the custom hook
export default AppContext
```

Setup the Provider according to [React documentation](https://reactjs.org/docs/context.html#contextprovider)

```jsx
// for example, something like this

<AppContext.Provider value={name: 'Nancy'}>
	<MyComponent />
</AppContext.Provider>
```

```jsx
// MyComponent

import React from 'react';
import { useAppContext } from './AppContext';

const MyComponent = () => {
	const { name } = useAppContext();
	return (
		<h1>Hello {name}</h1>
	)
}

export default MyComponent;
```

## Mock the custom hook

Now use Jest to mock the custom hook. What is  happening here is that we are spying on `AppContext.useAppContext` and giving it our mock function, which in this case is a function that returns the testing values we give it

```jsx
import React from "react";
import { shallow } from 'enzyme';
import * as AppContext from './AppContext'; // note we're importing with a * to import all the exports

import MyComponent from './MyComponent';

test('MyComponent renders properly with name', () => {
	const contextValues = {name: 'Annie'};
	jest.spyOn(AppContext, 'useAppContext')
			.mockImplementation(() => contextValues);
	const wrapper = shallow(<MyComponent />);
	expect(wrapper.find('h1').text()).toBe('Hello Annie');
});
```

Since we can pass in testing values to the mock `useAppContext`, we can assert if the `<h1>` is rendering the name correctly

**References**

- [Jest Mock functions](https://jestjs.io/docs/en/jest-object#mock-functions)
- [Testing ‘useContext’ React hook with Enzyme shallow](https://medium.com/7shifts-engineering-blog/testing-usecontext-react-hook-with-enzyme-shallow-da062140fc83)