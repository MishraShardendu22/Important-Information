## To use Redux Toolkit to manage a global context with an array and a variable, follow these steps:

### 1. Set Up Redux Toolkit

First, ensure you have Redux Toolkit installed in your project:

```bash
npm install @reduxjs/toolkit react-redux
```

### 2. Create a Slice

Create a slice to manage your state. This includes your array and variable.

```javascript
import { createSlice } from '@reduxjs/toolkit';

const initialState = {
  myArray: [],
  myVariable: '',
};

const mySlice = createSlice({
  name: 'mySlice',
  initialState,
  reducers: {
    setArray(state, action) {
      state.myArray = action.payload;
    },
    addToArray(state, action) {
      state.myArray.push(action.payload);
    },
    setVariable(state, action) {
      state.myVariable = action.payload;
    },
  },
});

export const { setArray, addToArray, setVariable } = mySlice.actions;

export default mySlice.reducer;
```

### 3. Configure Store

Set up your Redux store and integrate the slice.

```javascript
import { configureStore } from '@reduxjs/toolkit';
import myReducer from './mySlice';

const store = configureStore({
  reducer: {
    mySlice: myReducer,
  },
});

export default store;
```

### 4. Provide the Store

Wrap your main application component with the `Provider` from `react-redux`.

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux';
import store from './store';
import App from './App';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

### 5. Use Redux State in Components

Now you can use the global state in your components.

```javascript
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { addToArray, setVariable } from './mySlice';

const MyComponent = () => {
  const myArray = useSelector((state) => state.mySlice.myArray);
  const myVariable = useSelector((state) => state.mySlice.myVariable);
  const dispatch = useDispatch();

  const handleAddItem = () => {
    dispatch(addToArray('New Item'));
  };

  const handleSetVariable = () => {
    dispatch(setVariable('New Value'));
  };

  return (
    <div>
      <h1>My Variable: {myVariable}</h1>
      <button onClick={handleSetVariable}>Set Variable</button>
      <ul>
        {myArray.map((item, index) => (
          <li key={index}>{item}</li>
        ))}
      </ul>
      <button onClick={handleAddItem}>Add Item</button>
    </div>
  );
};

export default MyComponent;
```

### Summary

1. **Create a slice** with initial state and reducers for managing the array and variable.
2. **Configure the store** and add the slice reducer.
3. **Wrap your app** with the Redux `Provider`.
4. **Use `useSelector` and `useDispatch`** in components to read from and update the global state.

This setup allows you to manage a global array and a variable in your React application efficiently with Redux Toolkit.
