# React types

```TS
# ReactNode 

type ReactText = string | number;
type ReactChild = ReactElement | ReactText;

interface ReactNodeArray extends Array<ReactNode> {}
type ReactFragment = {} | ReactNodeArray;

type ReactNode = ReactChild | ReactFragment | ReactPortal | boolean | null | undefined;
```

```TS
# ReactElements

declare global {
  namespace JSX {
    interface Element extends React.ReactElement<any, any> { }
  }
}
```
# By Sample
```TS
<p> // <- ReactElement = JSX.Element
   <Custom> // <- ReactElement = JSX.Element
     {true && "test"} // <- ReactNode
  </Custom>
 </p>
```

```TS
//React Components, Elements, and Instances
//https://reactjs.org/blog/2015/12/18/react-components-elements-and-instances.html
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';

class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    console.log('This is a component instance:', this);
  }

  render() {
    const another_element = <div>Hello, World!</div>;
    console.log('This is also an element:', another_element);
    return another_element;
  }
}

console.log('This is a component:', MyComponent)

const element = <MyComponent/>;

console.log('This is an element:', element);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```


