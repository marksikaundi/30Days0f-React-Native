# Styles

> React Native styles are based on CSS, with a few key differences.

We use styles to make our apps look great. Styles let us configure the visual properties of our components, like background color, as well as their layout, i.e. their position and size on the screen.

React Native styles are based on CSS: most of the style property names and values are the same between React for the web and React Native. This is convenient, since we'll be able to reuse a lot of our existing knowledge from building web apps.

However, there are some important differences between CSS and React Native styles. The biggest difference is that there are no CSS files! There's no special language or syntax to learn; all of our styles are defined using JavaScript.

There are two common ways to define component styles:

- Inline styles
- StyleSheets

We’ll start by exploring both of these approaches.

## Inline styles

Most of the built-in React Native components (View, Text, Image, etc) accept a `style` object as a prop. Styling this way is similar to React for the web: keys are camel-cased CSS property names and values are typically CSS values. For example, we can configure the backgroundColor of a View by passing `{ backgroundColor: "#0088FF" }` as the style prop.

In the following example, we set the backgroundColor, width, and height of a View using an _inline_ style object:

<iframe src="https://snack.expo.io/embedded/@dabbott/styled-view?preview=true&platform=web" style="height: 26em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;" />

[Download example](https://expo.io/--/api/v2/snack/download/@dabbott/styled-view)

> Any example snippet can be downloaded as a full React Native project on your computer! We'll include a "Download example" link below each snippet from here on out. After unzipping the file, run `npm install` and `expo start` to run the project locally. This is totally optional.

Inline styles are useful for prototyping, since they're co-located with our rendering code. We also _need_ to use inline styles when defining dynamic styles, e.g. styles based on props, since we don't know the values of our props until the render function is called.

However, inline styles can quickly grow from a couple lines into quite a lot of code, which clutters our render method, making our code harder to follow. Wouldn't it be convenient if we could move them somewhere else? That's where StyleSheets come in.

## StyleSheets

The `StyleSheet` API gives us a consistent way to define our styles outside of our component definition. Additionally, `StyleSheet` includes important performance optimizations that aren't possible with inline styles. For these reasons, we should generally use the `StyleSheet` API wherever possible, rather than inline styles.

Here's the same example as above using StyleSheets:

<iframe src="https://snack.expo.io/embedded/@dabbott/stylesheet-view?preview=true&platform=web" style="height: 26em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;" />

[Download example](https://expo.io/--/api/v2/snack/download/@dabbott/stylesheet-view)

We call `StyleSheet.create` with a top-level object containing nested style objects. `StyleSheet` will then optimize our styles and return them to us. The keys of the top-level object are arbitrary, but will determine the names of our optimized styles. We can then refer to them by name in our render method, e.g. styles.myStyle.

A React Native StyleSheet is analogous to a CSS stylesheet containing classnames - we define them separately from our component code, and can reuse the same definition wherever we want that style.

Sometimes we may want to apply multiple styles to a component at the same time (similar to "cascading" in CSS styles), and fortunately, React Native provides an easy way to do that.

## Applying multiple styles

Suppose we want to render two `Text` components. One should use a "standard" text style, while the other should extend our "standard" text style with an additional "fancy" style.

On the web, we would probably pass two classnames to our "fancy" text component: one for the standard style and one for the fancy style. React Native lets us pass an array of styles to a component to accomplish the same thing. When we pass an array of styles as a style prop, their keys are merged into a single object, with the last object in the array taking precedence.

Here's our example with two `Text` components:

<iframe src="https://snack.expo.io/embedded/@dabbott/multiple-styles?preview=true&platform=web" style="height: 38em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;" />

[Download example](https://expo.io/--/api/v2/snack/download/@dabbott/multiple-styles)

Here we can see that the fancy text uses the size of the "standard" text, but adds two additional style properties. Note that the color of the "fancy" style overrides the color of the "standard" style, since we pass it last in the array. Also note that we can mix-and-match inline style objects and StyleSheet styles in this array.

This approach helps us manage the complexity of complicated components by reusing portions of our styles in multiple places.

Tomorrow we'll take styling a step further to define responsive layouts for our components.
