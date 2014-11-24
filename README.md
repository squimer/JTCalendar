A fork from JTCalendar
==========

![Version](https://img.shields.io/cocoapods/v/JTCalendar.svg)
![License](https://img.shields.io/cocoapods/l/JTCalendar.svg)
![Platform](https://img.shields.io/cocoapods/p/JTCalendar.svg)

JTCalendar is a calendar control for iOS easily customizable.

## What's new?

- monthDidChange method added to delegate.
- Swift examples.

## Installation

With [CocoaPods](http://cocoapods.org/), add this line to your Podfile.

    pod 'JTCalendar', '~> 1.1'


## Screenshots

![Month](./Screens/month.png "Month View")

## Usage

### Swift Warning

If you're using swift, you'll need a bridging header file (You can create one following this [tutorial](https://developer.apple.com/library/ios/documentation/swift/conceptual/buildingcocoaapps/MixandMatch.html)).

Once you have a YouAppName-Bridging-Header.h file, add the following lines:

```objective-c
#import "JTCalendar.h"
#import "JTCalendarMenuView.h"
#import "JTCalendarContentView.h"
```

And you ready to go.

### Basic usage

You have to create two views in your UIViewController.

The first view is `JTCalendarMenuView`, it represents the months.

The second view is `JTCalendarContentView`, the calendar itself.

Your UIViewController must implement `JTCalendarDataSource`

#### Objective-C
```objective-c
#import <UIKit/UIKit.h>

#import "JTCalendar.h"

@interface ViewController : UIViewController<JTCalendarDataSource>

@property (weak, nonatomic) IBOutlet JTCalendarMenuView *calendarMenuView;
@property (weak, nonatomic) IBOutlet JTCalendarContentView *calendarContentView;

@property (strong, nonatomic) JTCalendar *calendar;

@end
```

`JTCalendar` is used to coordinate `calendarMenuView` and `calendarContentView`.

```objective-c
@implementation ViewController

- (void)viewDidLoad
{
    [super viewDidLoad];
        
    self.calendar = [JTCalendar new];
    
    [self.calendar setMenuMonthsView:self.calendarMenuView];
    [self.calendar setContentView:self.calendarContentView];
    [self.calendar setDataSource:self];
}

- (void)viewDidAppear:(BOOL)animated
{
    [super viewDidAppear:animated];
    
    [self.calendar reloadData]; // Must be call in viewDidAppear
}

- (BOOL)calendarHaveEvent:(JTCalendar *)calendar date:(NSDate *)date
{
    return NO;
}

- (void)calendarDidDateSelected:(JTCalendar *)calendar date:(NSDate *)date
{
    NSLog(@"%@", date);
}

- (void)calendarDidChangeMonth:(JTCalendar *)calendar date:(NSDate *)date
{
    NSLog(@"Date: %@", date);
}

@end

```

#### Swift

`JTCalendar` is used to coordinate `calendarMenuView` and `calendarContentView`.

```swift
import UIKit

class ViewController: UIViewController, JTCalendarDataSource {
    
    @IBOutlet weak var calendarMenuView: JTCalendarMenuView!
    @IBOutlet weak var calendarContentView: JTCalendarContentView!
    
    var calendar: JTCalendar!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        self.calendar = JTCalendar()
        
        self.calendar.menuMonthsView = calendarMenuView
        self.calendar.contentView = calendarContentView
        self.calendar.dataSource = self
    }

    
    override func viewDidAppear(animated: Bool) {
        super.viewDidAppear(animated)
        
        self.calendar.reloadData()
    }
    
    func calendarHaveEvent(calendar: JTCalendar!, date: NSDate!) -> Bool {
        return true
    }
    
    func calendarDidDateSelected(calendar: JTCalendar!, date: NSDate!) {
        println(date)
    }
    
    func calendarDidChangeMonth(calendar: JTCalendar!, date: NSDate!) {
        println(date)
    }
    
}
```

### Customize the design

You have a lot of options available for personnalize the design.
Check the `JTCalendarAppearance.h` file for see all options.

##### Objective-c:
```objective-c
self.calendar.calendarAppearance.calendar.firstWeekday = 2; // Monday
self.calendar.calendarAppearance.ratioContentMenu = 1.;
self.calendar.calendarAppearance.menuMonthTextColor = [UIColor whiteColor];
self.calendar.calendarAppearance.dayCircleColorSelected = [UIColor blueColor];
self.calendar.calendarAppearance.dayTextColorSelected = [UIColor whiteColor];
[self.calendar reloadAppearance];
```

##### Swift:
```swift
self.calendar.calendarAppearance.calendar().firstWeekday = 2
self.calendar.calendarAppearance.ratioContentMenu = 1
self.calendar.calendarAppearance.menuMonthTextColor = UIColor.whiteColor()
self.calendar.calendarAppearance.dayCircleColorSelected = UIColor.blueColor()
self.calendar.calendarAppearance.dayTextColorSelected = UIColor.whiteColor()
self.calendar.reloadAppearance()
```

#### Recommendation

You may want to open your calendar on a specific date.

##### Objective-c:
```objective-c
[self.calendar setCurrentDate:myDate];
```

##### Swift:
```swift
self.calendar.currentDate = myDate
```



## Original Author

- [Jonathan Tribouharet](https://github.com/jonathantribouharet) ([@johntribouharet](https://twitter.com/johntribouharet))

## License

JTCalendar is released under the MIT license. See the LICENSE file for more info.
