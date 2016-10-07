# React ES5 to ES6

## Quick links

1. [require => import](#require)
1. [createClass => extends React.Component](#createClass)
1. [module.exports => export default](#module)
1. [name function()  =>  name()](#name)
1. [getDefaultProps and propTypes](#getDefaultProps)
1. [getInitialState](#getinitialstate)
1. [destructuring & spread attributes](#destructuring)
1. [use arrow functions](#use)
1. [“this” differences](#this)

### <a id="require"></a>require => import

ES5

  ```js
  //ES5
  var React = require("react");  
  var PropTypes = React.PropTypes;
  ```

ES6

  ```js
  import React, { Component, PropTypes } from 'react';
  ```

### <a id="createClass"></a>createClass => extends React.Component

ES5

  ```js
  var Mycomponent = React.createClass({
    render: function() {
      return (
        <div>ES5</div>
      );
    },
  });
  ```

ES6

  ```js
  class Mycomponent extends React.Component {
    render() {
      return (
        <div>ES6</div>
      );
    }
  }
  ```

### <a id="module"></a>module.exports => export default

ES5

  ```js
  var Mycomponent = React.createClass({
    render: function() {
      return (
        <div>ES5</div>
      );
    },
  });

  module.exports = Mycomponent;

  ```

ES6

  ```js
  export default class Mycomponent extends React.Component {
    render() {
      return (
        <div>ES6</div>
      );
    }
  }
  ```

### <a id="name"></a>name function()  =>  name()

ES5

  ```js
  var Mycomponent = React.createClass({
    componentWillMount: function(){

    },
    render: function() {
      return (
        <div>ES5</div>
      );
    },
  });

  module.exports = Mycomponent;

  ```

ES6

  ```js
  export default class Mycomponent extends React.Component {
    componentWillMount() {

    }
    render() {
      return (
        <div>ES6</div>
      );
    }
  }
  ```

### <a id="getDefaultProps"></a>getDefaultProps and propTypes

ES5

  ```js
  var Video = React.createClass({
      getDefaultProps: function() {
          return {
              autoPlay: false,
              maxLoops: 10,
          };
      },
      propTypes: {
          autoPlay: React.PropTypes.bool.isRequired,
          maxLoops: React.PropTypes.number.isRequired,
          posterFrameSrc: React.PropTypes.string.isRequired,
          videoSrc: React.PropTypes.string.isRequired,
      },
      render: function() {
          return (
              <View />
          );
      },
  });
  ```

ES6

  ```js
  class Video extends React.Component {
    render() {
        return (
            <View />
        );
    }
  }
  Video.defaultProps = {
      autoPlay: false,
      maxLoops: 10,
  };
  Video.propTypes = {
      autoPlay: React.PropTypes.bool.isRequired,
      maxLoops: React.PropTypes.number.isRequired,
      posterFrameSrc: React.PropTypes.string.isRequired,
      videoSrc: React.PropTypes.string.isRequired,
  };
  ```

ES future proposals:

  ```js
  class Video extends React.Component {
    static defaultProps = {
      autoPlay: false,
      maxLoops: 10,
    }
    static propTypes = {
      autoPlay: React.PropTypes.bool.isRequired,
      maxLoops: React.PropTypes.number.isRequired,
      posterFrameSrc: React.PropTypes.string.isRequired,
      videoSrc: React.PropTypes.string.isRequired,
    }
    state = {
      loopsRemaining: this.props.maxLoops,
    }
  }
  ```

### <a id="getInitialState"></a>getInitialState

ES5

  ```js
  var Header = React.createClass({
    getInitialState: function() {
      return {
        title: this.props.title
      };
    },
  });
  ```

ES6

  ```js
  export default class Header extends Component {
    constructor(props) {
      super(props);
      this.state = {
        title: props.title
      };
    }
  }
  ```

ES future proposals:
  
  ```js
  export default class Header extends Component {
    state = {
      title: this.props.title
    };
      
    // followed by constructor...
  }
  ```

### <a id="destructuring"></a>destructuring & spread attributes

```js
class AutoloadingPostsGrid extends React.Component {
  render() {
    var {
      className,
      ...otherProps,  // contains all properties of this.props except for className
    } = this.props;
    return (
      <div className={className}>
        <PostsGrid {...otherProps} />
        <button onClick={this.handleLoadMoreClick}>Load more</button>
      </div>
    );
  }
}

```

### <a id="use"></a>use arrow functions

Stateless component:

```js

function App() {
  return (
    <div>
      <MyComponent />
    </div>
  );
}

```

Using Arrow function:

```js
const App = () => (
  <div>
    <MyComponent />
  </div>
);
```

Using Arrow funtion with [Destructuring function arguments](https://github.com/getify/You-Dont-Know-JS/blob/master/es6%20&%20beyond/ch2.md#destructuring-parameters):

```js
const App = ({className, ...other}) => (
  <div className={classnames(className)} {...other}>
    <MyComponent />
  </div>
);
```

### <a id="this"></a>“this” differences

ES5

  ```js
  import React from 'react';

  const Contacts = React.createClass({
    handleClick() {
      console.log(this); // React Component instance
    },
    render() {
      return (
        <div onClick={this.handleClick}></div>
      );
    }
  });

  export default Contacts;
  ```

ES6

  ```js
  import React from 'react';

  class Contacts extends React.Component {
    constructor(props) {
      super(props);
    }
    handleClick() {
      console.log(this); // null
    }
    render() {
      return (
        <div onClick={this.handleClick}></div>
      );
    }
  }

  export default Contacts;
  ```

There are a few ways we could bind the right context, here’s how could do it:

  ```js
  import React from 'react';

  class Contacts extends React.Component {
    constructor(props) {
      super(props);
      this.handleClick = this.handleClick.bind(this);
    }
    handleClick() {
      console.log(this); // React Component instance
    }
    render() {
      return (
        <div onClick={this.handleClick}></div>
      );
    }
  }

  export default Contacts;
  ```


