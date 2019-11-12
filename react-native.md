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
    + In general, you should initialize state in the constructor, and then call setState when you want to change it.
    + For example, let's say we want to make text that blinks all the time. The text itself gets set once when the blinking component gets created, so the text itself is a prop. The "whether the text is currently on or off" changes over time, so that should be kept in state.

- `stylesheets` 
    + use it to control the styles.
    + same as css but with `camelCasing`  

- `height and width`
    + fixed width and height can be set using height and width prop in style. It will remain same no matter the screen or other component dimensions.
    + use `flex:1` to make a component to fill all available space, shared evenly amongst other components with the same parent. The larger the flex given, the higher the ratio of space a component will take compared to its siblings.
    + ⚠️ A component can only expand to fill available space if its parent has dimensions greater than 0. If a parent does not have either a fixed width and height or flex, the parent will have dimensions of 0 and the flex children will not be visible. ⚠️ 
    
- `layouts`
    + ❗️[details](https://medium.com/wix-engineering/the-full-react-native-layout-cheat-sheet-a4147802405c)❗️

- `text input`
    ```python
    <TextInput
        style={{height: 40}}
        placeholder="Type here to translate!"
        onChangeText={(text) => this.setState({text})}
        value={this.state.text}
    />  
    ```
- `buttons`
- `scrolling`
- `lists to display data`
    +  two types of list flatlist and section list
    +  `flatlist` The FlatList component displays a scrolling list of changing, but similarly structured, data. FlatList works well for long lists of data, where the number of items might change over time. Unlike the more generic ScrollView, the FlatList only renders elements that are currently showing on the screen, not all the elements at once. The FlatList component requires two props: data and renderItem. data is the source of information for the list. renderItem takes one item from the source and returns a formatted component to render.
    + `section lists` If you want to render a set of data broken into logical sections, maybe with section headers, similar to UITableViews on iOS, then a SectionList is the way to go.
- `making http call` 🌏
    + use `fetch`
    + more [info](https://developer.mozilla.org/en-US/docs/Web/API/Request)
    + a simple `get` request  fetch('https://mywebsite.com/mydata.json');
    ```python 
        fetch('https://mywebsite.com/endpoint/', {
          method: 'POST',
          headers: {
            Accept: 'application/json',
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            firstParam: 'yourValue',
            secondParam: 'yourOtherValue',
          }),
        });
    ```
        
        








