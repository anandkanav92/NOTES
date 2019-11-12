`react-native` (tut 📙 [source](https://egghead.io/lessons/react-native-create-a-react-native-app-and-run-it-on-the-ios-simulator-and-android-emulator))
---

- `<View><Text>Hello world!</Text></View>`.
    + This is JSX - a syntax for embedding XML within JavaScript. Many frameworks use a specialized templating language which lets you embed code inside markup language. In React, this is reversed. JSX lets you write your markup language inside code. It looks like HTML on the web, except instead of web things like <div> or <span>, you use React components. In this case, <Text> is a built-in component that displays some text and View is like the <div> or <span>.

- `props aka properties`.
    + it lets you define properties for your own custom components. Similar to member variables of a class. See the working example below.
```python
import React, { Component } from 'react';
import { Text, View } from 'react-native';

class Greeting extends Component {
  render() {
    return (
      <View style={{alignItems: 'center'}}>
        <Text>Hello {this.props.name}!</Text>
      </View>
    );
  }
}

export default class LotsOfGreetings extends Component {
  render() {
    return (
      <View style={{alignItems: 'center', top: 50}}>
        <Greeting name='Rexxar' />
        <Greeting name='Jaina' />
        <Greeting name='Valeera' />
      </View>
    );
  }
}
```
- `state`
    + There are two types of data that control a component: props and state. props are set by the parent and they are fixed throughout the lifetime of a component. For data that is going to change, we have to use state.

    In general, you should initialize state in the constructor, and then call setState when you want to change it.

    For example, let's say we want to make text that blinks all the time. The text itself gets set once when the blinking component gets created, so the text itself is a prop. The "whether the text is currently on or off" changes over time, so that should be kept in state.








