<!--docs:
title: ttons"<component name>"
layout: detail
section: components
excerpt: "iOS Buttons"
ide_version: "<cIDE name> <compatible IDE version and build number>"
material_package_version: "<compatible Material platform package version number>"
iconId:
path: /
api_doc_root:
-->

# Buttons

[Buttons](https://material.io/components/buttons/) allow users to take actions, and make choices, with a single tap.

There are four types of buttons:

1. [Text button](#text-button)
2. [Outlined button](#outlined-button)
3. [Contained button](#contained-button)
4. [Toggle button](#toggle-button) (*not fully supported in iOS*)

![Example of the four button types](assets/buttons_types.png)


## Using buttons


### Install `MDCButton`

<details><summary><b>Expand for installation instructions for <code>MDCButtons</code></b></summary>

<br>

`MDCButton` is used to implement all four Material Buttons. In order to use `MCDButton`, do the following:

1. Install with Cocoapods
    Add the following line to your `Podfile`:

    ```
    pod MaterialComponents/Buttons
    ```
    
    Run the installer:
    
    ```
    pod install
    ```

1. Import the Buttons and initialize them `MDCButtons` using `alloc`/`init`.

<!--<div class="material-code-render" markdown="1">-->
#### Swift
```swift
import MaterialComponents.MaterialButtons
import MaterialComponents.MaterialButtons_Theming

let button = MDCButton()
```
#### Objective-C
```objc
#import "MaterialButtons.h"
#import <MaterialComponents/MaterialButtons+Theming.h>

MDCButton *button = [[MDCButton alloc] init];
```

</details>


### Making Buttons accessible

To help ensure your buttons are accessible to as many users as possible, please
be sure to review the following recommendations:

#### Set `-accessibilityLabel`

Set an appropriate
[`accessibilityLabel`](https://developer.apple.com/documentation/uikit/uiaccessibilityelement/1619577-accessibilitylabel)
value if your button does not have a title. This is often the case with Floating
Action Button instances which typically only have an icon.

##### Objective-C

```objc
button.accessibilityLabel = @"Create";
```

##### Swift

```swift
button.accessibilityLabel = "Create"
```

#### Minimum touch size

Make sure that your buttons have a minimum touch area. The Material spec
for buttons calls for buttons that have a [visual height of
36](https://material.io/design/components/buttons.html#specs)
and that [touch areas should be at least 44 points high and 44
wide](https://material.io/design/layout/spacing-methods.html#touch-click-targets).

#### Set the touch size

To keep a button's visual sizes small with larger touchable areas, set the
`hitAreaInsets` to a negative value. Be careful to maintain sufficient distance
between the button touch targets. This will allow your button to have [a large
enough touch
target](https://material.io/design/layout/spacing-methods.html#touch-click-targets)
while maintaining the desired visual appearance. For more see the [Touch and click
targets](https://material.io/design/layout/spacing-methods.html#touch-click-targets)
in the spec.

##### Objective-C

```objc
CGFloat verticalInset = MIN(0, -(48 - CGRectGetHeight(button.bounds)) / 2);
CGFloat horizontalInset = MIN(0, -(48 - CGRectGetWidth(button.bounds)) / 2);
button.hitAreaInsets = UIEdgeInsetsMake(verticalInset, horizontalInset, verticalInset, horizontalInset);
```

##### Swift

```swift
let buttonVerticalInset =
min(0, -(kMinimumAccessibleButtonSize.height - button.bounds.height) / 2);
let buttonHorizontalInset =
min(0, -(kMinimumAccessibleButtonSize.width - button.bounds.width) / 2);
button.hitAreaInsets =
UIEdgeInsetsMake(buttonVerticalInset, buttonHorizontalInset,
buttonVerticalInset, buttonHorizontalInset);
```

#### Set the minimum visual size of the button

Set your buttons to have a minimum size. [Material Buttons
guidelines](https://material.io/design/components/buttons.html#specs)
typically recommend [a minimum height of 36 points and a minimum width of 64
points](https://material.io/design/components/buttons.html#specs).

##### Objective-C

```objc
button.minimumSize = CGSizeMake(64, 36);
```

##### Swift

```swift
button.minimumSize = CGSize(width: 64, height: 48)
```

#### Exceptions

However there are
[some](https://material.io/design/components/buttons.html#toggle-button) clear
[exceptions](https://material.io/design/components/app-bars-bottom.html#specs)
for these rules. Please adjust your buttons sizes accordingly.

#### Using `accessibilityHint`

Apple rarely recommends using the `accessibilityHint` because the label should
already be clear enough to indicate what will happen. Before you consider
setting an `-accessibilityHint` consider if you need it or if the rest of your
UI could be adjusted to make it more contextually clear.

A well-crafted, thoughtful user interface can remove the need for
`accessibilityHint` in most situations. Examples for a selection dialog to
choose one or more days of the week for a repeating calendar event:

- (Good) The dialog includes a header above the list of days reading, "Event
repeats weekly on the following day(s)." The list items do not need
`accessibilityHint` values.
- (Bad) The dialog has no header above the list of days. Each list item
(representing a day of the week) has the `accessibilityHint` value, "Toggles
this day."


## Text button

[Text buttons](https://material.io/components/buttons/#text-button) are typically used for less-pronounced actions, including those located in dialogs and cards. In cards, text buttons help maintain an emphasis on card content.

### Text button example

Text buttons are implemented by [MDCButton](https://material.io/develop/ios/components/buttons/api-docs/Classes/MDCButton.html). To use a text button use the text button theming method on the MDCButton theming extension. For more information on theming extensions see the [Theming section](#theming). 

MDCButton API and source Code:

* MDCButton (a subclass of [UIButton](https://developer.apple.com/documentation/uikit/uibutton))
    * [Class description](https://material.io/develop/ios/components/buttons/api-docs/Classes/MDCButton.html)
    * [GitHub source](https://github.com/material-components/material-components-ios/blob/develop/components/Buttons/src/MDCButton.h)

<!--<div class="material-code-render" markdown="1">-->
#### Swift
```swift
button.applyTextTheme(withScheme: containerScheme)
```

#### Objective-C

```objc
[self.button applyTextThemeWithScheme:self.containerScheme];
```
<!--</div>-->

<details>
<summary><b>Adding an icon to a text button</b></summary>
<br>

To add an icon to an MDCButton styled as a text button use the familiar UIButton methods for setting an image.

!["iOS text button with purple text 'Text button' and '+' icon over a white background."](assets/text-button-icon.svg)

<!--<div class="material-code-render" markdown="1">-->
```swift
button.setImage(image, for: .normal)
```

```objc
[button setImage:image forState: UIControlStateNormal];
```
<!--</div>-->

</details>

### Anatomy and key properties

A text button has a text label, a transparent container and an optional icon.

![Text button anatomy diagram](assets/text_button_anatomy.png)

1. Text label
1. Container
1. Icon

_**Note** A container in iOS refers to a set of components with an applied Material Theme. A container with respect to anatomy refers to the visible bounds of a component._

<details>
<summary><b>Text label</b> and <b>Icon</b> attributes</summary>
<br>

|  | Attribute | Related method(s) | Default value |
| --- | --- | --- | --- |
| **Text label** | <a href="https://developer.apple.com/documentation/uikit/uibutton/1623992-titlelabel"><code>titleLabel</code></a> |  | |
| |  | <a href="https://material.io/develop/ios/components/buttons/api-docs/Classes/MDCButton.html#/c:objc(cs)MDCButton(py)uppercaseTitle"><code>uppercaseTitle</code></a> | YES |
| |  | <a href="https://developer.apple.com/documentation/uikit/uibutton/1623993-settitlecolor"><code>setTitleColor:forState:</code></a> | System default |
| |  | <a href="https://developer.apple.com/documentation/uikit/uibutton/1624018-settitle"><code>setTitle:forState:</code></a> | Black |
| **Color** |  |  | |
| **Typography** |  |  |  |
| **Icon** | | | |
| **Size** | | | |
| **Gravity** (position relative to text label) | | | |
| **Padding** (space between icon and text label) | | | |


</details>

<details>
<summary><b>Container</b> attributes</summary>
<br>

|  | Attribute | Related method(s) | Default value |
| --- | --- | --- | --- |
| **Color** |  |  | |
| **Stroke color** | |  | |
| **Stroke width** |  |  |  |
| **Shape** |  | | |
| **Elevation** | | | |
| **Ripple color** | | | | 
</details>

## Text button
<!-- Extracted from docs/text-button.md -->

<img src="docs/assets/text.gif" alt="An animation showing a Material Design text button." width="128">

[Text buttons](https://material.io/components/buttons/#text-button) are typically used for less-pronounced actions, including those located in dialogs and cards. In cards, text buttons help maintain an emphasis on card content.

### Text button example

Text buttons are implemented by [MDCButton](https://material.io/develop/ios/components/buttons/api-docs/Classes/MDCButton.html). To use a text button use the text button theming method on the MDCButton theming extension. For more information on theming extensions see the [Theming section](#theming). 

<!--<div class="material-code-render" markdown="1">-->
#### Swift
```swift
button.applyTextTheme(withScheme: containerScheme)
```

#### Objective-C

```objc
[self.button applyTextThemeWithScheme:self.containerScheme];
```
<!--</div>-->

## Text button

[Text buttons](https://material.io/components/buttons/#text-button) are typically used for less-pronounced actions, including those located in dialogs and cards. In cards, text buttons help maintain an emphasis on card content.


### Text button example

Source Code APIs:

* MDCButton  (a subclass of [UIButton](https://developer.apple.com/documentation/uikit/uibutton))
    * [Class description](https://material.io/develop/ios/components/buttons/api-docs/Classes/MDCButton.html)
    * [GitHub source](https://github.com/material-components/material-components-ios/blob/develop/components/Buttons/src/MDCButton.h)
* [Themes class description](https://material.io/develop/ios/components/theming/) <!-- This is slated to be deprected, though the examples from https://material.io/develop/ios/components/buttons/api-docs/Classes/MDCButton.html appear to use this class -->

The following example shows a text button with a text label that uses Material Theming as its `ContainerScheme`.

For more information on Material Theming for iOS, go to the [iOS Material Theming page](../theming).

!["iOS Text button with purple text 'Text' over a white background."](assets/text-button.svg)
<!--<div class="material-code-render" markdown="1">-->
**Swift**

```swift
let button = MDCButton()
button.applyTextTheme(withScheme: MyMaterialTheme)
```

**Objective-C**

```ObjC
MDCButton *button = [[MDCButton alloc] init];
[button applyTextThemeWithScheme:MyMaterialTheme];
```
<!--</div>-->

<details>
<summary><b>Adding an icon to a text button</b></summary>
<br>

The following example shows a text button with an icon.

!["iOS text button with purple text 'Text button' and '+' icon over a white background."](assets/text-button-icon.svg)

<!--<div class="material-code-render" markdown="1">-->
```swift

```


```objc

```
<!--</div>-->

</details>

### Anatomy and key properties

A text button has a text label, a transparent container and an optional icon.

![Text button anatomy diagram](assets/text_button_anatomy.png)

1. Text label
1. Container
1. Icon


_**Note** A container in iOS refers to a set of components with an applied Material Theme. A container with respect to anatomy refers to the visible bounds of a component._

<details>
<summary><b>Text label</b> and <b>Icon</b> attributes</summary>
<br>

|  | Attribute | Related method(s) | Default value |
| --- | --- | --- | --- |
| **Text label** | <a href="https://developer.apple.com/documentation/uikit/uibutton/1623992-titlelabel"><code>titleLabel</code></a> |  | |
| |  | <a href="https://material.io/develop/ios/components/buttons/api-docs/Classes/MDCButton.html#/c:objc(cs)MDCButton(py)uppercaseTitle"><code>uppercaseTitle</code></a> | YES |
| |  | <a href="https://developer.apple.com/documentation/uikit/uibutton/1623993-settitlecolor"><code>setTitleColor:forState:</code></a> | System default |
| |  | <a href="https://developer.apple.com/documentation/uikit/uibutton/1624018-settitle"><code>setTitle:forState:</code></a> | Black |
| **Color** |  |  | |
| **Typography** |  |  |  |
| **Icon** | | | |
| **Size** | | | |
| **Gravity** (position relative to text label) | | | |
| **Padding** (space between icon and text label) | | | |


</details>

<details>
<summary><b>Container</b> attributes</summary>
<br>

|  | Attribute | Related method(s) | Default value |
| --- | --- | --- | --- |
| **Color** |  |  | |
| **Stroke color** | |  | |
| **Stroke width** |  |  |  |
| **Shape** |  | | |
| **Elevation** | | | |
| **Ripple color** | | | | 
</details>



## Outlined button

[Outlined buttons](https://material.io/components/buttons/#outlined-button) are medium-emphasis buttons. They contain actions that are important, but aren’t the primary action in an app.

### Outlined button example without container schemes

You can apply a theme to the button using `Themes`.

Source Code APIs:

* MDCButton  (a subclass of [UIButton](https://developer.apple.com/documentation/uikit/uibutton))
    * [Class description](https://material.io/develop/ios/components/buttons/api-docs/Classes/MDCButton.html)
    * [GitHub source](https://github.com/material-components/material-components-ios/blob/develop/components/Buttons/src/MDCButton.h)
* [Themes class description](https://material.io/develop/ios/components/theming/)  <!-- This is slated to be deprected, though the examples from https://material.io/develop/ios/components/buttons/api-docs/Classes/MDCButton.html appear to use this class -->

The following example shows an outlined button with a text label and stroked container that uses Material Theming as its `ContainerScheme`.

For more information on Material Theming for iOS, go to the [iOS Material Theming page](../theming).
    

!["Outlined button with purple text surrounded by a gray outline"](assets/outlined-button.svg)

<!--<div class="material-code-render" markdown="1">-->
**Swift**
```swift
let button = MDCButton()
button.applyOutlinedTheme(withScheme: MyMaterialTheme)
```
**Objective-C**
```objc
MDCButton *button = [[MDCButton alloc] init];

[self.button applyOutlinedThemeWithScheme:self.MyMaterialTheme];
```
<!--</div>-->

<details>
<summary><b>Adding an icon to an outlined button</b></summary>
<br>

The following example shows an outlined button with an icon.

!["iOS outlined button with purple text 'Outlined' and '+' icon over a white background."](assets/outlined-button-icon.svg)

<!--<div class="material-code-render" markdown="1">-->
```swift

```


```objc

```
<!--</div>-->

</details>


### Outlined button example with container schemes

You can apply a theme to the button that applies to all elements in a container using `MDCContainerScheme`.

Source Code APIs:

* MDCButton  (a subclass of [UIButton](https://developer.apple.com/documentation/uikit/uibutton))
    * [Class description](https://material.io/develop/ios/components/buttons/api-docs/Classes/MDCButton.html)
    * [GitHub source](https://github.com/material-components/material-components-ios/blob/develop/components/Buttons/src/MDCButton.h)
* [Themes class description](https://material.io/develop/ios/components/theming/)  <!-- This is slated to be deprected, though the examples from https://material.io/develop/ios/components/buttons/api-docs/Classes/MDCButton.html appear to use this class -->
* [MDCContainerScheme class description](https://github.com/material-components/material-components-ios/tree/stable/components/schemes/Container)

!["Outlined button example in Android with purple text surrounded by a gray outline"](assets/outlined-button.svg)

<!--<div class="material-code-render" markdown="1">-->
**Swift**
```swift
let button = MDCButton()
button.applyTextTheme(withScheme: MyMaterialTheme)
```
**Objective-C**
```objc
MDCButton *button = [[MDCButton alloc] init];
[self.button applyTextThemeWithScheme:self.MyMaterialTheme];
```
<!--</div>-->

<details>
<summary><b>Adding an icon to a contained button</b></summary>
<br>

The following example shows a contained button with an icon.

!["iOS contained button with purple text 'Contained' and '+' icon over a white background."](assets/contained-button-icon.svg)

<!--<div class="material-code-render" markdown="1">-->
```swift

```


```objc

```
<!--</div>-->

</details>


### Anatomy and key properties

An outline button has text, a container, and an optional icon.

![Outlined button anatomy diagram](assets/outlined_button_anatomy.png)

1. Text label
1. Container
1. Icon

_**Note** A container in iOS refers to a set of components with an applied Material Theme. A container with respect to anatomy refers to the visible bounds of a component._

<details>
<summary><b>Text label</b> and <b>Icon</b> attributes</summary>
<br>

|  | Attribute | Related method(s) | Default value |
| --- | --- | --- | --- |
| **Text label** | | | |
| **Color** |  | | |
| **Typography** | | | |
| **Icon** | | | |
| **Size** | | | |
| **Gravity** (position relative to text label) | | | |
| **Padding** (space between icon and text label) | | | |


</details>

<details>
<summary><b>Container</b> attributes</summary>
<br>

|  | Attribute | Related method(s) | Default value |
| --- | --- | --- | --- |
| **Color** | | | |
| **Stroke color** | | | |
| **Stroke width** || | |
| **Shape** | | | |
| **Elevation** | | | |
| **Ripple color** | | | |

</details>


## Contained button

[Contained buttons](https://material.io/components/buttons/#contained-button) are high-emphasis, distinguished by their use of elevation and fill. They contain actions that are primary to your app.

### Contained button example

Source Code APIs:

* MDCButton  (a subclass of [UIButton](https://developer.apple.com/documentation/uikit/uibutton))
    * [Class description](https://material.io/develop/ios/components/buttons/api-docs/Classes/MDCButton.html)
    * [GitHub source](https://github.com/material-components/material-components-ios/blob/develop/components/Buttons/src/MDCButton.h)
* [Themes class description](https://material.io/develop/ios/components/theming/)  <!-- This is slated to be deprected, though the examples from https://material.io/develop/ios/components/buttons/api-docs/Classes/MDCButton.html appear to use this class -->

The following example shows a contained button with a text label and a filled container that uses Material Theming as its `ContainerScheme`.

For more information on Material Theming for iOS, go to the [iOS Material Theming page](../theming).
.

!["Contained button example with white text 'Text' on a purple background."](assets/contained-button.svg)

<!--<div class="material-code-render" markdown="1">-->
**Swift**
```swift
let button = MDCButton()
button.applyContainedTheme(withScheme: MyMaterialTheme)
```
**Objective-C**
```objc
MDCButton *button = [[MDCButton alloc] init];
[self.button applyContainedThemeWithScheme:self.MyMaterialTheme];
```

<!--</div>-->


### Anatomy and key attributes

A contained button has text, a container, and an optional icon.


_**Note** A container in iOS refers to a set of components with an applied Material Theme. A container with respect to anatomy refers to the visible bounds of a component._

![Contained button anatomy diagram](assets/contained_button_anatomy.png)

1. Text label
1. Container
1. Icon

<details>
<summary><b>Text label</b> and <b>Icon</b> attributes</summary>
<br>

|  | Attribute | Related method(s) | Default value |
| --- | --- | --- | --- |
| **Text label** | | | |
| **Color** |  | | |
| **Typography** | | | |
| **Color** || | |
| **Size** | | | |
| **Gravity** (position relative to text label) | | | |
| **Padding** (space between icon and text label) | | | |


</details>

<details>
<summary><b>Container</b> attributes</summary>
<br>

|  | Attribute | Related method(s) | Default value |
| --- | --- | --- | --- |
| **Color** | | | |
| **Stroke color** | | | |
| **Stroke width** || | |
| **Shape** | | | |
| **Elevation** | | | |
| **Ripple color** | | | |

</details>



## Toggle button

[Toggle buttons](https://material.io/components/buttons/#toggle-button) can be used to select from a group of choices.

There are two types of toggle buttons:

* [Toggle button](#toggle-button) (*not supported in iOS*)
* [Icon](#icon)

### Toggle button

The toggle button allows you to select from a group of buttons that can be set to [selective action](https://material.io/components/buttons/#toggle-button) where only one button in a group can be selected at one time.

**NOTE** The Material toggle bar is not supported in iOS. 

### Icon

Icons can be used as toggle buttons when they allow selection, or deselection, of a single choice, such as marking an item as a favorite.

* [MDCCardCollectionCell](https://material.io/develop/ios/components/cards/api-docs/Classes/MDCCardCollectionCell.html)
* [UICollectionViewController]()
* [Themes class description](https://material.io/develop/ios/components/theming/)  <!-- This is slated to be deprected, though the examples from https://material.io/develop/ios/components/buttons/api-docs/Classes/MDCButton.html appear to use this class -->

The iOS icon toggle button is only available for use with the iOS [card](../Cards) component. Go to the card article for an [example](../Cards/#card-example-with-icon-buttons).

## Theming

<!-- Extracted from docs/theming.md -->

You can theme an MDCButton to match a
[Material Design button style](https://material.io/design/components/buttons.html) using theming
extensions. [Learn more about theming extensions](../../docs/theming.md).

### How to theme an MDCButton

To make use of the theming methods shown in the examples above do the following:

1. Install the theming extensions with Cocoapods
    Add the following line to your `Podfile`:

    ```
    pod MaterialComponents/Buttons+Theming
    ```
    
    Run the installer:
    
    ```
    pod install
    ```

1. Import the Buttons theming target

<!--<div class="material-code-render" markdown="1">-->
#### Swift
```swift
import MaterialComponents.MaterialButtons
import MaterialComponents.MaterialButtons_Theming

let button = MDCButton()
```
#### Objective-C
```objc
#import "MaterialButtons.h"
#import <MaterialComponents/MaterialButtons+Theming.h>

MDCButton *button = [[MDCButton alloc] init];
```

From there, use the theming methods from the examples to achieve your preferred button style.
