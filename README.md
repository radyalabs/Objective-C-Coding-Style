Radya Labs Objective-C Coding Style
=======================================

Radya Labs Objective-C Coding Style

## Introduction
Here are some of the documents from Apple that informed the style guide:

* [The Objective-C Programming Language](http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/ObjectiveC/Introduction/introObjectiveC.html)
* [Cocoa Fundamentals Guide](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CocoaFundamentals/Introduction/Introduction.html)
* [Coding Guidelines for Cocoa](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)
* [iOS App Programming Guide](http://developer.apple.com/library/ios/#documentation/iphone/conceptual/iphoneosprogrammingguide/Introduction/Introduction.html)

## Dot & Bracket Notation Syntax
Dot notation should be used for accessing properties only.
Bracket notation is used for mutating properties and other instances.

**Dot notation**
```objc
CGFloat heightOfView = self.view.frame.size.height;
Person *person = self.company.person;
```

**Bracket notation**
```objc
[self.view setBackgroundColor:[UIColor redColor]];
[self.person setFirstName:@"Johnny"];
```

## Variables
Variables names must be named as clear and descriptively as possible.

Single letter variables name should be avoided except in `for()` loops.

Asterisks indicating pointers belong with the variable, e.g., `NSString *text` not `NSString* text` or `NSString * text`, except in the case of constants.

Property definitions should be used in place of naked instance variables whenever possible. Direct instance variable access should be avoided except in initializer methods (`init`, `initWithCoder:`, etc…), `dealloc` methods and within custom setters and getters. For more information on using Accessor Methods in Initializer Methods and dealloc, see [here](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/mmPractical.html#//apple_ref/doc/uid/TP40004447-SW6).

**For example:**
```objc
@interface Person : NSObject

@property (strong, nonatomic) NSString *firstName;
@property (strong, nonatomic) NSString *lastName;

@end
```

**Not**
```objc
@interface Person : NSObject {
	NSString *firstName;
	NSString *lastName;
}
```

## CGFloat and NSInteger
Always use `CGFloat` instead of `float` or `double` 

and `NSInteger` instead of `int`

## Constants
Constants should be declared as `static` constants and not `#define` unless explicitly being used as a macro

Always use 'k' before the constants name.

**For example:**
```objc
static const NSString *kCompanyName = @"Radya Labs";
static const CGFloat kHeaderHeight = 44.0f;
```

**Not:**
```objc
#define COMPANY_NAME @"Radya Labs"
#define HEADER_HEIGHT 44
```

## Braces {...}
Put open brace `{` in line with method invocations.
Give new line before close brace `{`

**For example:**
```objc
- (void)fetchDataFromURL:(NSURL *)url {
  ...
}
```

**Not:**
```objc
- (void)fetchDataFromURL:(NSURL *)url
{
  ...
}
```

## Booleans
Since `nil` resolves to `NO` it is unnecessary to compare it in conditions. Never compare something directly to `YES`, because `YES` is defined to 1 and a `BOOL` can be up to 8 bits.

This allows for more consistency across files and greater visual clarity.

**For example:**
```objc
if (!someObject) {
}
```

**Not:**
```objc
if (someObject == nil) {
}
```

-----
**For a `BOOL`, here are two examples:**
```objc
if (isAwesome)
if (![someObject boolValue])
```

**Not:**
```objc
if ([someObject boolValue] == NO)
if (isAwesome == YES) // Never do this.
```
-----
If the name of a `BOOL` property is expressed as an adjective, the property can omit the “is” prefix but specifies the conventional name for the get accessor, for example:

```objc
@property (assign, getter=isEditable) BOOL editable;
```

## pragma mark
`#pragma mark` directives show up in XCode in the menus for direct access to methods. They have no impact on the program at all.
`#pragma mark` should be used to organize the code.

**For example:**
```objc
@implementation ViewController

#pragma mark - Designated initializer
- (id)init {
  ...
}

#pragma mark - UIViewController

- (void)viewDidLoad {
  ...
}

- (void)viewDidAppear:(BOOL)animated {
  ...
}

#pragma mark - IBAction
- (IBAction)cancel:(id)sender {
  ...
}

#pragma mark - UITableViewDataSource
- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {
  ...
}

#pragma mark - UITableViewDelegate
- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath {
  ...
}
```

## NSUserDefaults and NSNotificationCenter key/post naming
Use prefix `UserDef.` for `NSUserDefaults` key.

Use prefix `Notif.` for `NSNotificationCenter` name.

**For example:**
```objc
[[NSUserDefaults standardUserDefaults] setObject:@"RadyaLabs" forKey:@"UserDef.COMPANY_NAME"];
[[NSNotificationCenter defaultCenter] postNotificationName:@"Notif.STOP_PLAYING_MOVIE" object:nil];
``` 