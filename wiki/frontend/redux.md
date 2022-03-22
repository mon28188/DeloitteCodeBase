# State management - LWC & Redux

---

### What is state management?
State management refers to the management of the state of one or more user interface controls such as text fields, 
OK buttons, radio buttons, and so on in a graphical user interface.

#### Example
We have 2 pages, `page A` and `page B`

On page A we have 2 inputFields - `input1`, `input2`

On page B we have 1 inputField - `input3`

The initial state will look as following

initialState = {
    `input1`: ' ',
    `input2`: ' ',
    `input3`: ' '
}

As we fill in the values, the state will be updated with these values, and the values should be present in 
both of the pages. So after we fill in `input1` and `input2` on `page A` and we navigate to `page B`, we can access 
the values that we first introduced in `page A`.

### What is Redux?
Redux is an open-source JavaScript library for managing application state.

Redux is a pattern and library for managing and updating application state, using events called "actions".
It serves as a centralized store for state that needs to be used across your entire application, with rules ensuring
that the state can only be updated predictable.

In order to implement Redux on LWC we create a LWC base component that will help us in doing so `pnlUiRedux`

More information regarding Redux can be found on [Redux](https://redux.js.org/).

### How to use Redux Store?
The center of every Redux application is the store. A "store" is a container that holds your application's global state.

To be able to use the Redux Store for state management we need the following base components 
`pnlUiProvider`, `pnlUiConnectedRouter`, `c-pnl-ui-route` and `pnlUiHistory`.

#### Example
Example of how to implement the Redux Store can be found in the LWC base components 
[LWC Base Components](/wiki/frontend/lwcbase.md)

---

[Home](/wiki/Home.md) - [Frontend](/wiki/frontend/frontend.md) - State management - LWC & Redux