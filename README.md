#Butter#

Butter is a framework for OS X that seeks to provide a set of commonly used controls which are full replacements for their cell-based AppKit counterparts. This framework is still a work in progress, but it is **usable in production apps.**

This framework seeks to provide the following:

- Image-based customization of controls for various states
- Block-based action handlers
- Complete independence of cell-based controls
- Customizable properties that would otherwise be hard to change

#Controls#

##BTRControl##
`BTRControl` is a subclass of `BTRView` that provides a base for all controls. It offers state-based customization with block-based (or alternatively target/action-based) control event handling. `BTRControl` is designed for subclassing.

##BTRButton##
`BTRButton` is a subclass of `BTRControl`, and is an extremely customizable. Here's an example:

```objc
BTRButton *button = [[BTRButton alloc] initWithFrame:rect];
[button setTitle:@"Hey!" forControlState:BTRControlStateNormal];
[button setBackgroundImage:image1 forControlState:BTRControlStateNormal];
[button setBackgroundImage:image2 forControlState:BTRControlStateHighlighted];
[button addBlock:^{ NSLog(@"hi!"); } forControlEvents:BTRControlEventClick];
button.animatesContents = YES; // animate the transition back from click
```

##BTRActivityIndicator##
`BTRActvityIndicator` is a subclass of `BTRView` that provides a comprehensive API for creating any type of circular indeterminate activity indicator. Nearly all features of the indicator can be modified, and if more customization is desired a custom layer can be set to completely modify the appearance of the spinner. Short example:

```objc
BTRActivityIndicator *indicator = [[BTRActivityIndicator alloc] initWithFrame:rect];
indicator.progressShapeColor = newColor;
indicator.progressAnimationDuration = 4.f; // make it slow
indicator.progressShapeCount = 20; // give it more gears
[indicator startAnimating];
```

##BTRImageView##
`BTRImageView` is a subclass of `BTRView`, and it provides a fast and lightweight alternative to `NSImageView`. The view is layer-hosted, meaning the sublayer that contains the image itself can safely have a  transform applied. This opens up many possibilities for complex animations. `BTRImageView` can also handle animated images, such as GIFs.

```objc
BTRImageView *imageView = [[BTRImageView alloc] initWithImage:someGIF];
imageView.contentMode = BTRViewContentModeScaleAspectFit;
imageView.transform = some3DTransform;
imageView.animatesMultipleFrames = YES; // animate the GIF
```

`BTRImageView` is also capable of displaying stretchable images when combined with `BTRImage`.

##BTRImage##
`BTRImage` is a `NSImage` subclass that provides support for stretchable images.

```objc
NSEdgeInsets insets = NSEdgeInsetsMake(0, 5, 0, 5);
BTRImage *image = [BTRImage resizableImageNamed:@"epic" withCapInsets:insets];
self.imageView.image = image; // BTRImageView only
```
Note that `BTRImage` will not attempt to use the stretched images when manually drawing, or for any other purpose than setting it as the image of a `BTRImageView`.

There is also a convenience category for creating `BTRImage`s out of `NSImage`s, located in `NSImage+BTRImageAdditions.h`.

##BTRTextField##
`BTRTextField` is a subclass of `NSTextField`. It takes all the pain out of customizing normal text fields. Background images for states, text shadow, placeholder text customization, custom text drawing frames, control event handlers, and more.

```objc
BTRTextField *textField = [[BTRTextField alloc] initWithFrame:rect];
[textField setBackgroundImage:image forControlState:BTRControlStateNormal];
textField.textShadow = someNSShadow;
```

##BTRSecureTextField##
The secure variant of `BTRTextField`.

##BTRLabel##
`BTRLabel` is a subclass of `BTRTextField` that provides a common setup for labels, with no bezel, background drawing, editing, or selection.

```objc
BTRLabel *label = [[BTRLabel alloc] initWithFrame:rect];
```
License
---
Butter is licensed under the MIT License. See the [License](https://github.com/ButterKit/Butter/blob/master/LICENSE.md).