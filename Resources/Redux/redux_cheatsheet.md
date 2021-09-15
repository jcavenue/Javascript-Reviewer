# Redux Cheat Sheet

**Redux** - simply a state management tool. Redux is an open-source JavaScript library for managing and centralizing application state. 

Link - [Redux](https://redux.js.org/introduction/getting-started)

---
### **Tips** : *Learn Redux without React for better understanding*

Redux API -
- compose
- combineReducers
- bindActionCreators
- applyMiddleware
- createStore

---

### **Compose Example**
*allows you to compose a set of functions and create one function that will pass a value through each of them*

- compose is a *functional helper*
```

	import { compose } from 'redux';

	const multiplyBy2 = num => num * 2;
	const divideBy2 = num => num / 2;
	const addBy2 = num => num + 2;

	// old way
	const calculate = num => addBy2(divideBy2(multiplyBy2(num)));

	// Redux compose
	const calculate = compose(addBy2, divideBy2, multiplyBy2);

	calculate(2);

	//OUTPUT = 4

```
---

