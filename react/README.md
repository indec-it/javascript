# INDEC React/JSX Style Guide() {

*A mostly reasonable approach to React and JSX*

> **Note**: this guide is base on airbnb guide [Airbnb React Style Guide](https://github.com/airbnb/javascript/tree/master/react),
it reinforces the most important rules and overwrites some of them.

## Table of Contents

1. [Methods](#methods)
1. [Actions](#actions)
1. [Best Practices](#best-practices)
    * Fragment usage [3.1](#best-practices--fragment)
    * Deprecation of `will` componentse [3.2](#bestpractices--deprecations)
    * Use PureComponent when be possible [3.3](#bestpractices--pureComponent)
    * Avoid re-render with react.memo [3.4](#bestpractices--memo)

## Methods

<a name="method--placement"></a><a name="1.1"></a>
- [1.1](#method--placement) **Method placement**: if the method dosen't use `this`, it can be a global function at the compilation unit.


<a name="method--purefunction"></a><a name="1.2"></a>
- [1.2](#method--pure--function) **Method declaration in pure functions**: method declarations should outside pure functions.

> Why? Method's are created in every execution of the render.

```jsx
// very bad
const UserDetails = ({states, user}) => {
    const findState = (states, user) => find(states, state => state._id == user.state);
    return (
        <div>
            {findState(states, user).name}
        </div>
    );
};

// good
const findState = (states, user) => find(states, state => state._id == user.state);

const UserDetails = ({states, user}) => (
    <div>
        {findState(states, user).name}
    </div>
);

// good
const findState = (states, user) => find(states, state => state._id == user.state);

class UsersList extends Component {
    // ...

    render() {
        const {user, states} = this.state;
        return (
            <div>
                {findState(states, user).name}
            </div>
        );
    }
}
```

<a name="method--props"></a><a name="1.2"></a>
- [1.3](#method--props--naming) **Methods and props naming**: handlers of a component should be called `handler`+`event`.

```jsx
// good
handleSubmit() {
    // ...
}

handleChange(e) {
    // ...
}
```

<a name="method--child"></a><a name="1.2"></a>
- [1.4](#child--method--naming) **Child methods naming**: handlers got from props should be named `on`+`event`.

```jsx
// bad
Comments.propTypes = {
    submit: PropTypes.func.isRequired,
    setChange: PropTypes.func.isRequired
};

// good
Comments.propTypes = {
    onChange: PropTypes.func.isRequired,
    onSubmit: PropTypes.func.isRequired
}
```

<a name="render--method"></a><a name="1.2"></a>
- [1.5](#render--method) **Render method naming**: If react elements are returned the structure should be `render`+`rendered content`.

```jsx
// good
class UserList extends Component {
  renderContent() {
      return (
          ...
      );
  }

  render() {
      return (
          <div>
              {this.renderContent()}
          </div>
      );
  }
}
```

**[⬆ back to top](#table-of-contents)**

## Actions

<a name="action--naming"></a><a name="2.1"></a>
- [2.1](#action--naming) **Actions naming**: actions should be named (entity + verb infinitive + action past).

```jsx
ENTITY_VERB_ACTION(past tense)

const USERS_FETCH_REQUESTED = 'USERS_FETCH_REQUESTED';
const USERS_FETCH_SUCCEEDED = 'USERS_FETCH_SUCCEEDED';
```

**[⬆ back to top](#table-of-contents)**

## Best Practices

<a name="best-practices--fragment"></a><a name="3.1"></a>
- [3.1](#best-practices--fragment) **Fragment usage**: avoid useless `div` or `View` (react-native) as element container, use `Fragment` instead.

```jsx
// bad
render() {
    return (
        <div>
            Some text.
            <h2>A heading</h2>
            More text.
            <h2>Another heading</h2>
            Even more text.
        </div>
    );
}
```

```jsx
// good
render() {
    return (
        <Fragment>
            Some text.
            <h2>A heading</h2>
            More text.
            <h2>Another heading</h2>
            Even more text.
        </Fragment>
    );
}
```

More information about `Fragment`: https://reactjs.org/docs/fragments.html

 Disclaimer: `Fragment` cannot render styles, in that case you should use `div`, or `View` in `react-native`.

<a name="bestpractices--deprecations"></a><a name="3.2"></a>
- [3.2](#bestpractices--deprecations) **Deprecation of `will` components**:

`componentWillMount` and `componentWillUpdate` are deprecated, `componentDidMount` and `componentDidUpdate` should be used now.

Also `componentWillReceiveProps ` is replaced by a new function called `getDerivedStateFromProps`

<a name="bestpractices--pureComponent"></a><a name="3.3"></a>
- [3.3](#bestpractices--pureComponent) **Use PureComponent when be possible**:

You should use `PureComponent` over `Component` because `PureComponent` handles the `shouldComponentUpdate` method for you.

[documentation](https://reactjs.org/docs/react-api.html#reactpurecomponent)

<a name="bestpractices--memo"></a><a name="3.4"></a>
- [3.4](#bestpractices--memo) **Avoid re-render with react.memo**:
Sometimes we have a function component and its props no change but the component re-render anyway, with `react.memo` we can avoid this.

```jsx
// bad
const Example = ({title}) => <h2>{title}</h2>

export default Example;
```

```jsx
// good
const Example = ({title}) => <h2>{title}</h2>

export default react.memo(Example);
```

When using `react-redux`, `connect` acts like `react.memo`. In that case you don't need to wrap it in `React.memo()`

**[⬆ back to top](#table-of-contents)**

# }
