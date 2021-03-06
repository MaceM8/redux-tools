# @redux-tools/reducers

A Redux store enhancer for asynchronous injection of reducers.

## API Reference

### `makeEnhancer`

Function which creates an enhancer to pass to `createStore()`.

#### Arguments

This function accepts no arguments.

#### Returns

(_Enhancer_): A Redux store enhancer which you can pass to `createStore()`.

#### Example

```js
import { createStore } from 'redux';
import { makeEnhancer as makeReducersEnhancer } from '@redux-tools/reducers';
import { identity } from 'ramda';

const store = createStore(identity, makeReducersEnhancer());
```

### `store.injectReducers`

This function will store passed reducers internally and replace the existing reducer with a fresh one.

#### Arguments

1. `reducers` (_Object_): Reducers to inject.
2. `options` (_Object_): Injection options. The following keys are supported:
   - [`namespace`] \(_string_): Namespace to inject the reducer under. If passed, the reducer will not handle actions from other namespaces and will store its state in `state.namespaces[namespace]` instead of in the root.
   - [`feature`] \(_string_): This string will be used instead of the default `namespaces` key to store the reducer state, allowing you to use @redux-tools for feature-based store structure (similar to Redux Form, e.g. `state.form.contact.values`).

### `store.ejectReducers`

Opposite to `store.injectReducers`. This function will remove the injected reducers. Make sure that you pass the correct namespace and epics (keys AND values), otherwise the reducers will not be removed.

#### Arguments

1. `reducers` (_Object_): Reducers to eject. Make sure that both the keys and values match the injected ones!
2. `options` (_Object_): Ejection options. The following keys are supported:
   - [`namespace`] \(_string_): Namespace the reducers were injected under.
   - [`feature`] \(_string_): This string will be used instead of the default `namespaces` key to store the reducer state, allowing you to use @redux-tools for feature-based store structure (similar to Redux Form, e.g. `state.form.contact.values`).
