# Layout with Flexbox

> If you're familiar with CSS properties like flex-direction, then you already know how to create layouts in React Native!

Layouts in React Native are based on CSS — if you're familiar with properties like flex-direction and justify-content, then you already know how to create layouts in React Native (and if you're not, that's fine too!). Today we'll review the most important style properties.

We'll first cover how to set the dimensions of an individual component.

> Note that I also wrote part of the official React Native documentation on this topic, and there will be many similarities between this lesson and the documentation site.

## Fixed dimensions

For a component to render on the screen, it needs both a width and height greater than 0. These can be set explicitly using the width and height style properties.

In the following example, we create 3 Views with different dimensions:

<iframe src="https://snack.expo.io/embedded/@dabbott/width-and-height?preview=true&platform=web" style="height: 26em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;" />

Setting dimensions this way is common for components that should always render at exactly the same size, regardless of screen dimensions.

## Flex dimensions

We can use the flex style property to define a component that expands or shrinks to fill the available screen space. We do this frequently, since mobile devices have a wide range of screen sizes, and we want our app to look good on all of them.

In this example, we create 3 Views that fill the height of the screen, regardless how big or small the screen is:

<iframe src="https://snack.expo.io/embedded/@dabbott/width-and-height?preview=true&platform=web" style="height: 26em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;" />

When using flex, we pass a number value. The larger the value, the higher the ratio of space a component will take compared to its siblings. A component with no siblings will fill its parent fully as long as the value is greater than 0.
A flex value of 0 indicates that the component should not expand beyond its "intrinsic dimensions". In the following example, we render one Text component with a flex value of 0, and another with a flex value of 1.

<iframe src="https://snack.expo.io/embedded/@dabbott/flex-dimensions?preview=true&platform=web" style="height: 26em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;" />

The intrinsic height of the text component is just large enough to fit the text itself. Note that flex defaults to 0 (use intrinsic dimensions), and that many components have an intrinsic width and height of 0 (such as View). If a component has a width or height of 0, nothing will render on the screen. This is a common source of confusion for beginners.

## Laying out children

So far we've covered how a component can specify its own dimensions. Most layout properties, however, are controlled by a component's parent.

We normally use a combination of flexDirection, justifyContent, and alignItems on a parent component to determine the layout of its children.

### flexDirection

We use flexDirection to choose either a vertical or horizontal layout of children components. The two values we commonly use are:

- **row**: Align children from left to right.
- **column**: (default) Align children from top to bottom.

<iframe src="https://snack.expo.io/embedded/@dabbott/flex-direction?preview=true&platform=web" style="height: 43em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;" />

The option we choose here determines the main axis of the layout. Our choice here will affect the meaning of the other layout properties.

> There are two other options for `flexDirection`, `row-reverse` and `column-reverse`, which will reverse the order of the children. These are rarely used; instead of adjusting the layout, reverse the order of the children in the component's render method.

### justifyContent

We use justifyContent to determine the distribution of children align the primary axis. Here are the options for values we can use:

- **flex-start**: (default) Distribute children at the start of the main axis.
- **center**: Distribute children in the center of the main axis.
- **flex-end**: Distribute children at the end of the main axis.
- **space-between**: Distribute children evenly along the main axis, with remaining space between the children.
- **space-around**: Distribute children evenly along the main axis, with remaining space between the children, and also at the beginning and end of the main axis.

<iframe src="https://snack.expo.io/embedded/@dabbott/justify-content?preview=true&platform=web" style="height: 36em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;" />

[Download example](https://expo.io/--/api/v2/snack/download/@dabbott/justify-content)

### alignItems

We use alignItems to determine the alignment of children along the cross axis. The cross axis is the axis that runs perpendicular to the main axis, e.g. if our flex-direction is column then our main axis is vertical and our cross axis is horizontal. Here are the options for values we can use:

- **stretch**: (default) Stretch children to fill the parent.
- **flex-start**: Align children at the start of cross axis.
- **flex-end**: Align children at the end of cross axis.
- **center**: Align children at the center of cross axis.
- **baseline**: Align children along a common baseline. Individual children can be set to be the reference baseline for their parents.

<iframe src="https://snack.expo.io/embedded/@dabbott/align-items?preview=true&platform=web" style="height: 44em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;" />

[Download example](https://expo.io/--/api/v2/snack/download/@dabbott/align-items)

> Note that _stretch_ will not stretch a child if its `width` is set explitly (or height in the case of a `flexDirection: row` parent).

## Differences from CSS

The most important difference between flexbox in CSS and React Native are the default values.

Here are the defaults for CSS:

```css
flex-direction: row;
align-items: flex-start;
position: static;
```

And React Native:

```css
flex-direction: column;
align-items: stretch;
position: relative;
```

Defaulting to a column layout on mobile is reasonable, since phones are by far the most common mobile device, and most of the time they're used in a vertical layout.

There are a few other differences, such as flex only supporting a single number value in React Native, but the framework will generally warn you if you try to do something that isn't supported.
