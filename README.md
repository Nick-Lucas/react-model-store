# react-model-store

### About

This package provides react bindings for [model-store.js](https://github.com/Nick-Lucas/model-store.js)

For more information about the motivations of this project, check out the main repo.

### API

This package is intended to feel familiar to redux users, and the API reflects this.

For a full example, check out the `examples/` folder, but the basic API is very simple

```js

// Create a model, as documented in the main repo
const model = createModel({
  counter: createDomain({ count: 0 }, store => ({
    increment: () => {
      const { count } = store.getState()
      return { count: count + 1 }
    },
    decrement: () => {
      const { count } = store.getState()
      return { count: count - 1 }
    },
  }))
})


// Import the Provider component and render 
// it with the model
import { Provider } from "react-model-store"

ReactDOM.render(
  <Provider model={model}>
    <App />
  </Provider>, 
  document.getElementById('root')
)

// Connect any component to the store which you 
// want state or functions injected into
import { connect } from "react-model-store"

class App extends React.Component { /* ... */ }

export default connect(
  state => ({
    count: state.counter.count
  }), 
  funcs => ({
    increment: funcs.counter.increment,
    decrement: funcs.counter.decrement
  })
)(App)
```

### Development

React bindings for model-store.js

For development, checkout [model-store](https://github.com/Nick-Lucas/model-store.js) and run `yarn link` or `npm link`

In this repo run `yarn link model-store` or `npm link model-store`
