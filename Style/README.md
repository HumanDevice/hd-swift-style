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
* [Color constants](#color-constants)

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
Use `self` keyword only when it's necessary (ex. closures or `init` methods).

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
When it's appropriate, make use of `if let` and `where`.

**Bad**
```swift
if object.name != nil {
  otherObject.existingName = object.name!
}
```

**Terrible**
```swift
if object.name != nil {
  if object.name! != "potato" {
   otherObject.existingName = object.name!
  }
}
```

**Good**
```swift
if let name = object.name where name != "potato" {
  otherObject.existingName = name
}
```

In case of enumeration, use `switch` statements over `if` statements.

**Bad**
```swift
if manager.isReachable {
 NetworkReachabilityManager.NetworkReachabilityStatus.NotReachable
 if NetworkReachabilityManager.NetworkReachabilityStatus.Reachable(.EthernetOrWiFi) == status {
  print("WiFi")
 } else if NetworkReachabilityManager.NetworkReachabilityStatus.Reachable(.WWAN) == status {
  print("WWAN")
 }
} else {
 print("No connection")
}

```

**Good**
```swift
switch status {
 case NetworkReachabilityManager.NetworkReachabilityStatus.NotReachable:
  print("No connection")
 case NetworkReachabilityManager.NetworkReachabilityStatus.Unknown:
  print("Unknown")
 case NetworkReachabilityManager.NetworkReachabilityStatus.Reachable(.EthernetOrWiFi):
  print("WiFi")
 case NetworkReachabilityManager.NetworkReachabilityStatus.Reachable(.WWAN):
  print("WWAN")
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

##Color constants
Colors used in whole project are kept in `ColorConstants` class.

**Example**
```swift
class ColorConstants {
  static let Gray = UIColor.init(red: 230/255, green: 230/255, blue: 230/255, alpha: 1)
}
```
