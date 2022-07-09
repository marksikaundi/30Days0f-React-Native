# Platform-specific Code

> Once we know how to run platform-specific code, we'll be equipped to make an app that feels great on every platform.

Most of the time, we can share exactly the same code between iOS and Android. However, sometimes we may want to do something platform-specific. Examples include: icons, spacing and font sizes, and touch interaction feedback.

React Native provides us 3 main ways of doing this:

- Use `Platform.OS` or `Platform.select` to run different code _at runtime_
- Use the file extension `.ios.js`, `.android.js`, or `web.js` to _compile_ different code into your app bundle
- Write native code and _bridge it_ into JavaScript

## `Platform.OS` and `Platform.select`

This approach is probably what you'll use most frequently. It's best for small differences between platforms, such as style or text differences.

For example, suppose we wanted a text label to be _uppercase_ on Android. We could use `Platform.OS` to do something special on Android like this:

```js
import { Platfrom, Text } from "react-native";

export default ({ title }) => (
  <Text>{Platform.OS === "android" ? title.toUpperCase() : title}</Text>
);
```

We commonly use `Platform.OS` like a switch statement: for each platform, we specify something different we want to happen. React Native conveniently includes a utility function, `Platform.select`, that makes this pattern a little easier for us to use. `Platform.select` relies on `Platform.OS` under the hood.

Here's an example where we choose different text styles based on the current platform:

```js
import { Platform, StyleSheet } from 'react-native'

const styles = StyleSheet.create({
  text: {
    textAlign: 'center',
    margin: 8,
    ...Platform.select({
      ios: {
        color: '#007AFF',
        fontSize: 18,
      },
      android: {
        color: 'white',
        fontWeight: '500',
      },
    }),
  },
  }
})
```

> This example was taken from React Native's `Button` implementation.

Here, `Platform.select` returns an object that is then spread into the text style object. In this case, we can use platform-specific `color`, `fontSize`, and `fontWeight` attributes, while still sharing the same `textAlign` and `margin` attributes across platforms.

Using `Platform.OS` and `Platform.select` lets us share the exact same _files_ between each platform, even if each platform evaluates a few branches of the code slightly different. The main disadvantage is, we're still bundling every platform's branch of the code into the app bundle (e.g. including iOS-specific code on Android), which can increase the app bundle size. Of course, this size difference is negligible for small stylistic changes, but what if we want a bigger change, like running an entirely separate component on iOS and Android?

## `.ios.js`, `.android.js`, `.web.js`

We can use different file extensions to tell the React Native packager which files to include in the build for each specific platform.

Suppose we want to use a different button component on iOS and Android. In that case, we might create a `Button.ios.js` and `Button.android.js` file. To use it, we'd import it as if the extension were `.js` as usual (`import Button from './Button.js'`) and the packager would automatically choose the correct version based on the current platform.

This approach is useful when we want to make large changes, since each platform's app bundle will only include the code it needs to run, resulting in a smaller bundle size. However, the main disadvantage is that we now have 2 files that may duplicate some code or have to stay in sync, e.g. a component would probably need to handle the same props on iOS and Android, so both files should be updated at the same time.

> We can also use `.native.js` to target both iOS and Android, while ignoring web. We may separately need to configure our web packager to ignore these files though, if we're not using Expo's default packager configuration.

## Native code

We can also run platform-specific code by including it in the native portion of the codebase. Some things are simply faster and easier to do natively, so it's occasionally worth considering this option.

This has the same tradeoffs as writing any other native code, which we'll cover more another day.

### Up next

Now that we know how to run platform-specific code, we're better equipped to make an app that feels great on every platform. One key aspect of this is _navigation_. Tomorrow, we'll begin using the library `react-navigation` to navigate between multiple screens in an app.
