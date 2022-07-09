# Persisting data

> Async Storage is a lightweight key-value database built specifically for React Native.

Many apps persist data on the device's filesystem for later use. Persisting data locally helps provide a great offline experience and handle cases where the user quits the app but wants to resume their progress later.

Apps persist data of all shapes and sizes - user input, API response JSON, images and videos, and more. Because of the variety of kinds of data we might want to persist, there are also a variety of ways we can do it:

- Binary data, like images and videos, are typically stored as files
- Very large data sets might be stored in a database, like SQLite or [realm](https://realm.io/docs/javascript/latest/)
- Smaller bits of data, like user input, authentication tokens, and API responses, are typically stored using [async-storage](https://github.com/react-native-community/async-storage)

We'll be looking at [`async-storage`](https://github.com/react-native-community/async-storage) today. This is React Native's equivalent of `localStorage` on the web.

## Async Storage

Async Storage is a lightweight key-value database built specifically for React Native. Keys and values are stored in the database as strings. While technically values can be any string, most values we store will be stringified JSON, and there are even a few built-in utility methods that assume values are JSON strings. There are no APIs for indexing or searching data.

The implementation of the database is allowed to be different on different platforms, e.g. it could be a single file, multiple files, or a SQLite database. For that reason, it's best not to assume any performance characteristics if you're planning to store and retreive a lot of data on multiple platforms -- you'll need to try it for your supported platforms and see what happens.

To install `async-storage`, run:

```bash
npm install --save @react-native-community/async-storage
```

> Before React Native 60, `async-storage` was bundled with React Native out-of-the-box, and imported with `import { AsyncStorage } from 'react-native'`. This is still how we'll import it in Expo Snack examples.

### Getting and setting items

As the name implies, all operations using `async-storage` are asynchronous. All of the APIs we call will return a `Promise`, so we'll usually call them with `await` (if you need a primer on `await`, check out yesterday's [article on network requests](./day-22-network-requests)). Most APIs can also fail (e.g. the device might be out of storage), so we should also handle errors.

Here's a slightly modified excerpt from the docs demonstrating how to store and retrieve data:

```js
storeData = async () => {
  try {
    await AsyncStorage.setItem("my_storage_key", "stored value");
  } catch (e) {
    // error saving
  }
};

readData = async () => {
  try {
    const value = await AsyncStorage.getItem("my_storage_key");

    if (value !== null) {
      // handle a previously stored value
    }
  } catch (e) {
    // error reading value
  }
};
```

### Example

Let's build on the example from yesterday's [article on network requests](./day-22-network-requests) by adding offline support for reading the lists of posts we fetch.

The main difference will be:

- After we fetch data, we'll store the JSON response using `AsyncStorage.setItem` so that it's there the next time the app launches
- When the component renders for the first time, as part of our `useEffect` call, we'll first try to read a previously stored item using `AsyncStorage.getItem`. If there's nothing stored, or if retrieving it fails, we fetch data as normal

<iframe src="https://snack.expo.io/embedded/@dabbott/persisting-data?preview=true&platform=web" style="height: 37em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;" />

[Download example](https://expo.io/--/api/v2/snack/download/@dabbott/persisting-data)

### Up next

We've covered a lot of material over the past few days: navigation, animation, gestures, network requests, persisting data, and more. Now it's time to practice putting it all together!
