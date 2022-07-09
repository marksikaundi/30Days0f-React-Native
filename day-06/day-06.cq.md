# Text Components

> The Text component is one of the most common React Native components — we use it whenever we need to display text in our app.

Unlike with React on the web, we can't just put text content directly inside any component. For example, this code _won't run_:

```js
<View>My text</View>
```

Instead, we need to wrap all of our text within a **`Text`** component:

```js
<View>
  <Text>My text</Text>
</View>
```

## Common styles

We've previously covered how we can use the style prop to style components in general. Here we'll cover some of the common ways we can style Text components specifically.

Text components can use all of the same style properties as View components, plus an additional set of `Text`-specific properties. Here are a few of the most common `Text`-specific properties:

- **fontFamily**: The name of the font family, e.g. "Helvetica".
- **fontSize**: The size to draw the font, in pixels.
- **fontWeight**: This thickness of the font. One of: 'normal', 'bold', '100', '200', '300', '400', '500', '600', '700', '800', '900'.
- **lineHeight**: The height of each line of text that includes the space above and below the text itself.
- **textAlign**: The alignment of the text drawn within the `Text` component. One of: 'auto', 'left', 'right', 'center', 'justify'.
- **color**: The text color.

In the following example, we'll set each of these properties, along with a few we've already used to style our View components:

<iframe src="https://snack.expo.io/embedded/@dabbott/styled-text?preview=true&platform=web" style="height: 47em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;" />

[Download example](https://expo.io/--/api/v2/snack/download/@dabbott/styled-text)

By default, `Text` components automatically grow horizontally to fit the text content drawn within. If the `Text` component can't grow horizontally within its parent anymore, it will then wrap the text content to the next line and grow vertically. However, we can override this behavior by specifying the dimensions of the component ourselves.

In this example, we set the width of the `Text` to 200 explicitly, which affects where it wraps to the next line:

<iframe src="https://snack.expo.io/embedded/@dabbott/styled-text-with-fixed-width?preview=true&platform=web" style="height: 48em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;" />

[Download example](https://expo.io/--/api/v2/snack/download/@dabbott/styled-text-with-fixed-width)

Note that textAlign affects the alignment of the text content drawn within the `Text` component, but not the component itself. If we want to align the `Text` component in the horizontal center of the screen, we would set the alignItems style property on the parent View.

## Inline text

`Text` components are similar to "block" elements on the web — if we use multiple `Text` elements within the same parent, they will stack on top of each other:

<iframe src="https://snack.expo.io/embedded/@dabbott/stacked-text-components?preview=true&platform=web" style="height: 53em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;" />

[Download example](https://expo.io/--/api/v2/snack/download/@dabbott/stacked-text-components)

However, we sometimes want `Text` components to act like "inline" elements so that we can render multiple styles of text content within a single paragraph. `Text` components can be nested to accomplish this. In this example, we'll style a specific range of text within the larger paragraph:

<iframe src="https://snack.expo.io/embedded/@dabbott/nested-styled-text?preview=true&platform=web" style="height: 53em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;" />

[Download example](https://expo.io/--/api/v2/snack/download/@dabbott/nested-styled-text)

Styles applied to a `Text` component also apply to every Text component descendant within it. In the previous example, the nested text inherits styles.text, but then overrides the fontWeight by applying styles.boldText (the innermost style has the highest precedence).

### Up next

Now, text is great and all, but if we want our app to look even better, we'll need to throw in some images. Tomorrow we'll learn how to do that using the `Image` component.
