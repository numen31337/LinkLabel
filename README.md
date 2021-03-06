# LinkLabel
UILabel with custom hyperlink styling, optional interaction delegate, minimal setup

![](http://i.imgur.com/fjHOieW.png)


## What’s up
Creating a UILabel with attributed text, links appear blue and underlined, and in most cases you don’t want them to be. It’s pretty awkward and a time-kill to try and make them simply be styled the way you desire.

LinkLabel makes this all easy. *Without any extra code*, links appear the same colour as the rest of your text, but underlined. It’s what the default *should* be.

If you want to add custom styling, that’s super simple, too. Same as you would specify attributes for your attributedText, any attributes you want to be different about your links, you add to LinkLabel’s `linkTextAttributes`, and `highlightedLinkTextAttributes`.

## Install with CocoaPods

```
pod 'LinkLabel'
```

## Install Manually
1. Drag contents of `Source` folder into your Xcode project.
2. Add `#import "UIKit/UIGestureRecognizerSubclass.h"` to Bridging Header file.

## Usage
Create a label using `LinkLabel`, instead of UILabel.

```swift
let myLabel = LinkLabel()
```

Setup attributed text, including `NSLinkAttributeName`, as normal.

```swift
let text = "This is some text, which includes a link."
let fullRange = NSMakeRange(0, (text as NSString).length)
let linkRange = (text as NSString).rangeOfString("includes a link")

let attributedString = NSMutableAttributedString(string: text)
attributedString.addAttribute(.font, value: UIFont.systemFont(ofSize: 15), range: fullRange)
attributedString.addAttribute(.foregroundColor, value: UIColor.black, range: fullRange)
attributedString.addAttribute(.link, value: URL(string: "https://google.com")!, range: linkRange)
```

If you wish to customise the link appearance:

```swift
let linkTextAttributes: [NSAttributedStringKey: AnyObject] = [
    .underlineStyle: NSNumber(value: NSUnderlineStyle.styleSingle.rawValue as Int),
    .foregroundColor: UIColor.green
]

let highlightedLinkTextAttributes: [NSAttributedStringKey: AnyObject] = [
    .underlineStyle: NSNumber(value: NSUnderlineStyle.styleSingle.rawValue as Int),
    .foregroundColor: UIColor.red
]

label.linkTextAttributes = linkTextAttributes
label.highlightedLinkTextAttributes = highlightedLinkTextAttributes
```

To make it easier to respond to link taps, I’ve added in an interaction delegate. Adopt `LinkLabelInteractionDelegate`, and then implement the delegate function:

```swift
label.interactionDelegate = self
```

```swift
//MARK: LinkLabelInteractionDelegate

func linkLabelDidSelectLink(linkLabel linkLabel: LinkLabel, url: NSURL) {
  print("did select link: \(url)")
}
```

## Credit

Created by [Andrew Hart](http://twitter.com/AndrewProjDent), for TwIM.

[ProjectDent.com](http://ProjectDent.com)

[@ProjectDent](http://twitter.com/ProjectDent)
