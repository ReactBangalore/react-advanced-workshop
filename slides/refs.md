### React Advanced Workshop

Kiran Abburi

[@kiran_abburi](https://twitter.com/kiran_abburi)

---

### Refs
* To imperatively modify a child outside of the typical dataflow
* Provides access to DOM nodes or React component instances

---

### Usecases
* Integrating with third party libraries like D3, jQuery
* Managing focus of inputs
* Triggering methods on components imperatively

---

### Refs
```js
class Form extends React.Component {
  componentDidMount() {
    this.inputRef.focus()
  }
  render() {
    return <input ref={ref => this.inputRef = ref} />
  }
}
```

---

### Refs
```js
class Form extends React.Component {
  constructor(props) {
    super(props)
    this.setInputRef = (ref) => this.inputRef = ref
  }
  componentDidMount() {
    this.inputRef.focus()
  }
  render() {
    return <input ref={this.setInputRef} />
  }
}
```

---

### Ref on react component
* CustomInput should be class component

```
class Form extends React.Component {
  render() {
    return <CustomInput ref={(ref) => this.inputRef = ref} />
  }
}
```

---

New Ref API in React 16.3
* React.createRef
* React.forwardRef

---

React.createRef
```
class Form extends React.Component {
  constructor(props) {
    super(props)
    this.inputRef = React.createRef()
  }
  componentDidMount() {
    this.inputRef.current.focus()
  }
  render() {
    return <input ref={this.inputRef} />
  }
}
```

---

React.forwardRef
```
function logProps(WrappedComponent) {
  class LogProps extends React.Component {
    componentDidUpdate(prevProps) {
      console.log('old props:', prevProps);
      console.log('new props:', this.props);
    }

    render() {
      return <WrappedComponent {...this.props} />;
    }
  }

  return LogProps;
}
export default logProps(FancyButton);
```

---

React.forwardRef
```
<FancyButton
  label="Click Me"
  handleClick={handleClick}
  ref={ref}
/>;
```

---

React.forwardRef
```
function logProps(WrappedComponent) {
  class LogProps extends React.Component {
    componentDidUpdate(prevProps) {
      console.log('old props:', prevProps);
      console.log('new props:', this.props);
    }

    render() {
      return <WrappedComponent {...this.props} />;
    }
  }
  function forwardRef(props, ref) {
    return <LogProps {...props} forwardedRef={ref} />;
  }
  return React.forwardRef(forwardRef);
}
export default logProps(FancyButton);
```
