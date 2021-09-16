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

### **compose Example**
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
### **createStore Example**
*it is an object store that return 4 functions*
```

	{
		dispatch: ƒ dispatch(),
		subscribe: ƒ subscribe(),
		getState: ƒ getState(), 
		replaceReducer: ƒ replaceReducer()
	}

```
Sample snippet

```

import {
	createStore,
 	compose,
	applyMiddleware,
	bindActionCreators
} from "redux";


const initialState = { value: 0 };

const INCREMENT = 'INCREMENT';
const ADD = 'ADD';

const increment = () => ({ type: INCREMENT })
const add = (amount) => ({ type: ADD, payload: amount });

const reducer = (state = initialState, action) => {
  if(action.type === INCREMENT){
    return { value: state.value + 1};
  }

  if(action.type === ADD){
    return { value: state.value + action.payload}
  }

  return state
}

// Four Functions
const store = createStore(reducer);
const subscriber = () => console.log('SUBSCRIBE', store.getState());

store.subscribe(subscriber); // calling this function everytime the state changes

store.dispatch(increment());
store.dispatch(add(100));

console.log(store.getState());

```
---
### **bindActionCreators example**
*it binds the action to the creators*

```
	const action = bindActionCreators({increment, add}, store.dispatch);

	action.add(500);
	action.increment();
```
---
### **combineReducers Example**
*use to combine reducers if the state is deeply nested or you want to code splitting and do task*

```
	import {
  createStore,
  compose,
  applyMiddleware,
  bindActionCreators,
  combineReducers
} from "redux";

const initialState = {
  users: [
    {id: 1, name: 'Jc'},
    {id: 2, name: 'Lara'}
  ],
  tasks: [
    {title: 'Do cleaning'},
    {title: 'Do some stuff'}
  ]
};

const ADD_USER = 'ADD_USER';
const ADD_TASK = 'ADD_TASK';

const addUser = (name) => ({type: ADD_USER, payload: name});
const addTask = (title) => ({type: ADD_TASK, payload: title});

const userReducers = (users = initialState.users, action) => {
  if(action.type === ADD_USER){
    return [ ...users, action.payload];
  }
  return users;
}

const tasksReducers = (tasks = initialState.tasks, action) => {
  if(action.type === ADD_TASK){
    return [ ...tasks, action.payload];
  }

  return tasks;
}


const reducers = combineReducers({users: userReducers, tasks: tasksReducers})

const store = createStore(reducers);
const subscriber = () => console.log('SUBSCRIBE', store.getState());
store.subscribe(subscriber);

const action = bindActionCreators({addTask, addUser}, store.dispatch);

action.addTask({title: 'do cleaning'})
```
---

