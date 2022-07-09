# Displaying Images

When building a mobile app, we often display images from many different sources: images from the web, images bundled with the app, photos from the user's camera, and more. Our images can vary in size from just a few pixels to tens of megabytes. Sometimes images will act as the background of a screen, and other times they'll be tappable thumbnails in a feed.

Because of these many different use cases, the `Image` component in React Native has to be extremely flexible. Today we'll look at some of the different ways we can use the `Image` component to display images.

## Bundled images

We use the source prop of the `Image` component to choose what image to display.

We can display images from the file system much like if we were using a JavaScript bundler for the web (e.g. webpack). We first import the image file by its path, and then pass the imported value as the source. Check it out in this example:

<iframe src="https://snack.expo.io/embedded/@dabbott/bundled-image?preview=true&platform=web" style="height: 53em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;"/>

In production, the React Native packager will include this image in our app bundle so that it loads directly from the device, even if the device isn't connected to the internet.

If we include multiple versions of the same image for phones with different screen resolutions, we should name them e.g. `myImage.png`, `myImage.png@2x`, and `myImage.png@3x`. The React Native packager will include them all in our app bundle, and the Image component will automatically choose the best version.

Note that if we don't set the width and height of the Image component (in this case we set them both to `200` in a style), it will automatically use the intrinsic dimensions of the image⁠ data. However, this only works for bundled images — the React Native packager measures the image at compile time and includes its dimensions in the metadata associated with the image.

## Images from the web

While we sometimes bundle a handful of images into our app, the majority of the images we display are typically hosted on the web. To display images from the web, we pass an object to the `source` prop, containing a `uri`.

Here's an example:

<iframe src="https://snack.expo.io/embedded/@dabbott/image-on-the-web?preview=true&platform=web" style="height: 53em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;"/>

In this case, the image data will be downloaded from the URI when the `Image` component is rendered for the first time.

Here, the image's intrinsic dimensions are unknown at compile-time, so we must control the `Image` component's size through styles. In the previous example we set a width and height, but we could also rely on other flexbox properties, like flex. Here's the same example, but now we stretch the image to fill the entire screen:

<iframe src="https://snack.expo.io/embedded/@dabbott/image-on-the-web-fullscreen?preview=true&platform=web" style="height: 53em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;"/>

If we know the image's intrinsic dimensions ahead-of-time (e.g. maybe the image was processed by our backend API already) we can include a width and height value in the object we pass to `source` to specify the image's intrinsic dimensions.

## Displaying content on top of an image

The `Image` component can't render any children, so if we want to render content on top of an image, we should instead use the `ImageBackground` component. This is a drop-in replacement for the `Image` component.

Here's the previous example, now using an `ImageBackground` and with a Text child:

<iframe src="https://snack.expo.io/embedded/@dabbott/image-with-content-on-top?preview=true&platform=web" style="height: 53em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;"/>

In the examples we've seen so far, the image has been scaled up or down automatically to match the layout of the Image and ImageBackground components that render them. Sometimes, however, we want a little more control over the scaling to make sure our images look great.

## Image scaling

Often we want to display images in a different aspect ratio than their intrinsic one. For example, we may present a grid of `Image` components as squares, when in reality some of the images are not perfect squares.

We can use the `resizeMode` style attribute to choose how to scale an image when its intrinsic aspect ratio is different from the aspect ratio of the `Image` component we render. The `resizeMode` is analogous to `background-size` or `object-fit` on the web.

The three common values for resizeMode are:

- **cover**: scale proportionally fill the `Image` component entirely
- **contain**: scale proportionally to fit within the `Image` component so that the entire image is visible
- **stretch**: scale each dimension independently to fill the `Image` component entirely

In the following example, we can see each of these options in action with a 200x600 image:

<iframe src="https://snack.expo.io/embedded/@dabbott/image-resizemode?preview=true&platform=web" style="height: 53em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;"/>

### Up next

So far we've only covered how to handle static content: views, text, and images. To make things more interactive, we'll need to handle user input. We'll learn how to do that tomorrow!
