# create-redux-toolkit-setters
 The `createSetters` function dynamically generates a set of "setter" functions based on the keys of an initial state object. These setter functions can be used in a state management library like Redux to update specific properties in the state.

```
/**
 * The `createSetters` function dynamically generates a set of "setter" functions
 * based on the keys of an initial state object. These setter functions can be
 * used in a state management library like Redux to update specific properties
 * in the state.
 *
 * @param {Object} initialState - An object representing the initial state,
 *                                where keys correspond to state properties.
 *
 * @returns {Object} - An object containing setter functions for each property in
 *                     the `initialState`. Each setter function has the form
 *                     `set<Key>()`, where `<Key>` is the capitalized name of
 *                     the property being set.
 *
 * The returned setter functions:
 *  - Take two arguments: `state` and `action`.
 *  - Update the corresponding key in the state with the value from `action.payload`.
 *
 * Example:
 *
 * Given an `initialState` of `{ name: '', age: 0 }`, this function will return:
 * {
 *   setName: (state, action) => (state.name = action.payload),
 *   setAge: (state, action) => (state.age = action.payload),
 * }
 *
 */
export const createSetters = initialState =>
  Object.keys(initialState).reduce((acc, key) => {
    const actionName = `set${key[0].toUpperCase()}${key.slice(1)}`;

    return {
      ...acc,
      [actionName]: (state, action) => {
        state[key] = action.payload;
      },
    };
  }, {});
```
