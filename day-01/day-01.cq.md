---
coverImageBackgroundPosition: "50% 70%;"
---

# What is React Native?

> React Native allows us to build a mobile application for iOS and Android in a single language and framework.

Welcome to 30 days of React Native! Each day in our 30-day journey will cover a different React Native topic. Many of the articles will build upon the previous day’s materials, and by the end of it we'll have covered all the concepts you need to build your own mobile app using React Native.

We expect readers to be familiar with fundamental React concepts like _components_ already. If you’re not, you can learn many of these with our more web-focused course [30 days of React](https://www.fullstackreact.com/30-days-of-react/). A basic understanding of web concepts like CSS is also expected.

You don't need to have any experience building mobile apps to understand any of the material covered. If you do have some mobile development experience and you're already familiar with a topic, feel free to skip ahead.

_So, what is React Native, anyway?_

## React Native

React is a JavaScript library for building user interfaces. _React Native_ is a framework for building _native_ Android and iOS apps using React.

One of the core concepts of React Native (and React) is to represent user interfaces in terms of different _components_. Here is an example of a component in React Native:

<iframe src="https://snack.expo.io/embedded/@dabbott/intro-component?preview=true&platform=web" style="height: 53em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;"/>

> Throughout this series, you'll see interactive code snippets like the one above. If you edit the code, the preview will update in realtime. You can even run the preview on an iOS or Android device! These code snippets are hosted using a free service called Expo Snack. This is similar to Codesandbox, Codepen, or JSFiddle for web code.

This component, `IntroComponent`, contains 3 smaller components within it: an `Image` component, a `Button`, and a `Text` label. The label updates when we press the button (go on, try it). It takes fairly little code to do a lot with React Native! We'll explore how each of these components work later this week.

The term _"native"_ in React Native means that the user interface of our app is constructed with the underlying platform's built-in UI elements. On the web, interfaces are constructed with HTML elements — HTML elements are considered _native_ to the web platform since they're provided by the web browser. Similarly, Apple and Google provide a built-in set of UI components for their mobile operating systems. React Native helps us construct interfaces with this, using JavaScript and React.

## Why React Native?

Many developers write native mobile applications using platform-supported languages, such as Swift/Objective-C for iOS and Java/Kotlin for Android. Instead of writing in different languages to build for both platforms, React Native allows you to build parts of your application (or all of it) in a single language (JavaScript) and framework (React). This minimizes the burden of familiarizing yourself with all the different languages, toolchains and development environments needed to support both iOS and Android. In other words, you can re-use any prior React and JavaScript knowledge from building web apps when building native mobile apps.

In addition to making it easy to share code between iOS and Android, React Native also allows developers to build components or functionality specific to one platform. We can write native components and APIs and define a “bridge” to the JavaScript interface. This flexibility means we can use React Native both for brand new projects and existing native applications.

## How is React Native different from hybrid app platforms?

Hybrid app platforms, like [Ionic](https://ionicframework.com/) and [Phonegap](https://phonegap.com/), also make it possible to build mobile applications using web technologies. Ionic, for example, already lets us create UI building blocks in the form of components (optionally even using React). However, these tools are different from React Native because they rely on WebViews in order to deliver the user interface. A WebView is a webpage embedded in a native app. The result is that the user interface often doesn’t feel like a typical native experience. Very minimal native code is actually used even though certain device APIs, like the camera roll, can still be accessed. On the other hand, React Native is a set of JavaScript bindings for native UI APIs. In other words, the UI in a React Native app is fully native.

Tomorrow, we'll demonstrate how fast it is to bootstrap React Native applications by setting up our very first project.
