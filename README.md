


# DiskMonitor
![](https://img.shields.io/badge/version-1.0-brightgreen.svg)

DiskMonitor is SwiftPM Package for monitoring added/ejected/renamed disks written in Swift 5.1,  working using Apple's low level Disk Arbritration framework.

Build using Swift 5.1, XCode 11.3, supports macOS only.

# Usage

The framework provide its functionality through the `DiskMonitor` class. You should make an instance of this class using the 
```swift
///  Creates a new disk monitor with an optional delegate passed.
///
///  `DiskMonitor` is a simple class that acts as a wrapper around the `DiskArbritation` framework from Apple that notifies
///  about changes with disk drives.
///
///  - Parameter  delegate: The delegate object that you want notified in the case of new discoveries.
public init(withDelegate delegate: DiskMonitorDelegate? = nil)
```
initialiser. You can optionally pass delegate now or set the property later. Setting delegate is the way the framework communicates back when change occurs with the disks. The `delegate` object should conform to:

```swift
	///  Requirements for being a delegate to a `DiskMonitor`.
	public  protocol  DiskMonitorDelegate: AnyObject {

	///  Called when a raw disk appears.
	///
	///  - Parameters:
	///  - monitor: The monitor that found it.
	///  - diskAppeared: The raw `DADisk`.
	func rawDiskMonitor(_ monitor: DiskMonitor, diskAppeared disk: DADisk)

	///  Called when a raw disk disappears.
	///
	///  - Parameters:
	///  - monitor: The monitor that found it.
	///  - diskAppeared: The raw `DADisk`.
	func rawDiskMonitor(_ monitor: DiskMonitor, diskDisappeared disk: DADisk)
	
	///  Called when a raw disk was renamed.
	///
	///  - Parameters:
	///  - monitor: The monitor that found it.
	///  - diskAppeared: The raw `DADisk`.
	func rawDiskMonitor(_ monitor: DiskMonitor, diskRenamed disk: DADisk)
}
```

Alternatively you can receive updates in the form of `Notification` s in the `Notification Center.default` center.

```swift
// MARK: - Notifications

extension  Notification.Name {

	///  Posted by the `DiskMonitor` when a disk appears. The notification's object is the raw `DADisk`.
	public  static  let  rawDiskAppeared = Notification.Name("DiskMonitor.rawDiskAppeared")

	///  Posted by the `DiskMonitor` when a disk dissapears. The notification's object is the raw `DADisk`.
	public  static  let  rawDiskDisappeared = Notification.Name("DiskMonitor.rawDiskDisappeared")

	///  Posted by the `DiskMonitor` when a disk gets renamed. The notification's object is the raw `DADisk`.
	public  static  let  rawDiskRenamed = Notification.Name("DiskMonitor.rawDiskRenamed")
}
```

After you have chosen your callback method, you are ready to call:
```swift
///  Makes the disk monitor start monitor what disks are added/ejected/renamed.
///
///  It posts notifications for adding/ejecting/renaming 
/// `.rawDiskAppeared`/`.rawDiskDisappeared`/`.rawDiskRenamed`.
///
///  You can stop the monitoring process with `stopMonitoring()`.
public  func  startMonitoring()
```

and 
```swift
///  Stops the currently launched disk monitoring.
///
///  You can start it again with `startMonitoring()`.
public  func  stopMonitoring()
```

when you want to end the monitoring process.

# Installation

### Swift Package Manager

1. Go to your project settings
2. Tap on your Project name above listed targets
3. Open tab swift packages
4. Add DiskMonitor's repo as a package.

# Further Information

If you find `DiskMonitor` Package helpful, you might as well like [DiskUtil](https://github.com/stoqn4opm/DiskUtil).

# Licence

The framework is licensed under MIT licence. For more information see file `LICENCE`
