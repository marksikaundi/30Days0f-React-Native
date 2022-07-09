# First component

> Now that we'll all set up, let’s dive into how components work in React Native.

If you’re already familiar with React, then you already know how to write in React Native. This is because they both share a core concept - **using components to construct interfaces.**

If you’ve never used React for the web before, there’s no need to worry! Let’s dive into how components work in React Native.

## Component structure

When we create a new application with Expo, a single component is created by default in `App.js`.

<iframe src="https://snack.expo.io/embedded/@houssein/app.js?preview=true&platform=web" style="height: 26em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;"  />

Let’s step through each part of the file. All our imports are declared at the very beginning:

```js
import React from "react";
import { StyleSheet, Text, View } from "react-native";
```

Just like writing components in React for a web page, we need to import the `react` library in order to be able to create our components. In the second line however, a number of core APIs from React Native are also imported:

- `StyleSheet`: API used to set styles outside of the component function
- `Text`: Used to display text (analogous to the [<span>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/span) element in HTML)
- `View`: Used to define layouts and draw boxes with borders (analogous to the [<div>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div) element in HTML)

On the web, core elements such as `div` and `span` never need to be imported and are supported by every browser automatically. In React Native however, every component must be imported.

I> Every core React Native API will be explored in more detail later in the series.

There are two ways to define a component using React Native (and React):

- A **function component** that uses a JavaScript function
- A **class component** that uses an ES6 class

Underneath our imports we can see our component defined as a function:

```js
export default function App() {
  return (
    <View style={styles.container}>
      <Text>Open up App.js to start working on your app!</Text>
    </View>
  );
}
```

The function returns what we want to render within that part of our application. In this example, we have a single View component that wraps a Text component that displays a simple message.

This component can also be written using a class instead:

```js
export default class App extends React.Component {
  render() {
    return (
      <View style={styles.container}>
        <Text>Open up App.js to start working on your app!</Text>
      </View>
    );
  }
}
```

Defining a component using a class requires extending `React.Component`. Using `extends` allows us to declare a class as a subclass of another class. In this example, `App` is a subclass of `React.Component`.

React Native reads both of these components in the exact same way. However, using class components make it possible to define state or use lifecycle methods.

I> [Hooks](https://reactjs.org/docs/hooks-intro.html), a newer React feature, also makes it possible to use state and lifecycle operations within function components

The last piece of our component is our style definitions:

```js
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center"
  }
});
```

The StyleSheet API is used here to define a `container` style that sets background color and a few flexbox properties. Using `flex: 1` makes the `View` expand to fill the entire screen. The combination of `alignItems: center` and `justifyContent: center` ensure the text component is aligned in the vertical and horizontal center.

Ready to learn more about styling in React Native? We’ll be exploring this in more detail in tomorrow’s article!
