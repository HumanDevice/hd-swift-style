# Human Device Swift Style Guide

## Table of Contents
* [Application architecture](#application-architecture)
* [XCode settings](#xcode-settings)
* [Naming](#naming)
* [Initialization of variables](#initialization-of-variables)
* [Code organization](#code-organization)
* [Use of `self`](#use-of-self)
* [`If` statements](#if-statements)
* [Closure Expressions](#closure-expressions)

##Application architecture
Every iOS application has the same base structure:
```
- Project
-- AppDelegate
-- Other global classes
-- Model
-- DAO
-- API
-- ViewController
-- Utils
-- Controls
```

![system architecture](https://s31.postimg.org/6nvwu929n/Screen_Shot_2016_07_04_at_11_29_31.png)

##XCode settings
Default tab spacing is 2 spaces.

##Naming
Class, enumerations, protocols and constants used in multiple classes are named using UpperCamelCase.

Functions, variables and constants used in parent class only are named using lowerCamelCase.

##Initialization of variables
When writing API and Model classes, make `Optional` as many variables as possible. When writing UIViewControllers, avoid optional variables, and go for instant declaration:

**Bad**
```swift
var images: [UIImage]?
var determinedRowHeight: Int?
var constantRowheight: Int = 74
```

**Good**
```swift
let constantRowHeight = 74
var images = [UIImage]()
var determinedRowHeight = 0
```

##Code organization
For UIViewControllers, code organization goes as follows:
* protocols and enums
* class declaration
  * class constants
  * IBOutlets
  * private class variables
  * UIViewController lifecycle methods
  * IBActions
  * public functions
  * static functions
* protocol implementation methods (in `extension`s)
* class extensions, `==` implementations, etc.
Private supporting functions come below functions they support (lifecycle, public methods, etc).

For **Model**, **API** and **Utils** classes `static` and `public` functions come first, and supporting private functions are below them.

##Use of `self`
Use `self` keyword only when it's necessary (ex. closuers or `init` methods).

##`If` statements
Don't use `()` while writing `if` statements, unless it makes code more readable. Put `else` in `if` closing line.

**Example**
```swift
if yomama.weight > 200 {
  yomama.fat()
} else {
  me.needsBetterJoke()
}
```
When it's appropriate, make use if `if let`.

**Bad**
```swift
if object.name != nil {
  otherObject.existingName = object.name!
}
```

**Good**
```swift
if let name = object.name {
  otherObject.existingName = name
}
```

##Closure Expressions
Use trailing closure syntax only if there's a single closure expression parameter at the end of the argument list. Start closure code in the new line.

**Example**
```swift
ImageAPI.downloadPictureForStore(superStore) {
  image in
  imageView.image = image
}
```
