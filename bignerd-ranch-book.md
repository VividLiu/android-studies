# Big Nerd Ranch

## Shortcuts

| shortcut or menu option | description |
|--------|--------|
| Alt+Enter (Option+Enter)| manually import a class|
| Shift+Shift | search everywhere |
| Ctrl+Shift+F | Find Path  |
| Ctrl+N | search class |
| Ctrl+Shift+N | search file |
| Right-Click (after constructor) | generate getter and setter |
| Android View -> res -> Right-Click layout folder | New Layout Resource file |
| package view -> Right-Click (package name) -> New Java class   | create new java class  |
| Settings -> System -> About Emulator (or Phone) -> Build Number (Tap 7 times) | enable developer settings |
| Tools -> SDK Manager -> Android SDK | download sdk or documentation |
| File > Project Structure > select app on left panel > click dependency on right top menu | Add a dependency to project |
| Tools > Android > Sync Project with Gradle Files | Sync Project with Gradle |

## Useful Links

| shortcut | description |
|--------|--------|
| forums.bignerdranch.com | debugging and general android help |

## Useful Java utilities

| utility | description |
|--------|--------|
| UUID | mechanism to create a universally unique ID value |

## Ch 3: Activity Lifecyle

Activity Lifecyle:

- every instance has lifecyle
  - four states:
    - resumed
    - paused
    - stopped
    - nonexistent
- transition methods:
  - notifies the activity of change
  - Nonexistent -> onCreate -> Stopped
  - Stopped -> onStart -> Pauseda
  - Paused -> onResume -> Resumed

  - Resumed ->  onPause -> Paused
  - Paused ->  onStopped -> Stopped
  - Stopped -> onDestroy -> NonExistent

  - Nonexistent -> Stopped -> Paused -> Resumed

- transition methods:
  - notifies the activity of change

  - Nonexistent -> onCreate -> Stopped
  - Stopped -> onStart -> Pauseda
  - Paused -> onResume -> Resumed

  - Resumed ->  onPause -> Paused
  - Paused ->  onStopped -> Stopped
  - Stopped -> onDestroy -> NonExistent

  - Nonexistent -> Stopped -> Paused -> Resumed

- Entire Lifetime (instance in memory):
  - Stopped
  - Paused
  - Resumed

- Visible Lifetime (view partially or fully visibly):
  - Paused (partially visible, could be fully visible also)
  - Resumed

- Foreground Lifetime:
  - User interacting with this activity
  - Resumed

- one activity in resumed state at any time

- onCreate(Bundle):
  - OS calls method after activity created but before on screen
  - typically activity overrides onCreate(Bundle)
    - inflate widgets (by calling setContentView(int))
    - get references to inflated widgets
    - set listeners on widgets to handle user interaction
    - connecting external models:w
  - never call onCreate(Bundle) or any other Activity; override
    method

- Logging Activity Lifecyle
  - **android.util.Log**: sends log messages
  - Log.d(String tag, String msg): sends debug messages

- override methods:
  - @Override: tells compiler overriding method
    - check if really overriding the method
  - super.onStart(): The call to superclass is required
    - should be the first line
- Logcat:
  - SDK window that displays the log
  - loglevels (Log.x):
    - e: error
    - w: warning
    - i: info
    - d: debug
    - v: verbose

- Back Button:
  - onPause -> onStop -> onDestroy

- Home Button:
  - onPause -> onStop:
    - activity hangs out in stopped state in memory
    - use recents button to go back to stopped activity
      - without recent button press and hold the home
- stopped Activity:
  - can be destroyed at the discretion of the OS
- partially visible:
  - new activity with transparent background or smaller screen
    size is launched on top of your activity
  - fully visible scenario occurs in multi-window mode in Android
    6.0 and higher.
- rotate activity:
  - destroys and starts a new activity
- fixed vs runtime device configuaration:
  - fixed: screen density
  - runtime:
    - screen orientation, keyboard availability, language, multi-window
    - resources that better match might be available
- landscape:
  - create new resource
  - Available Qualifier -> Orientation -> Landscape
  - configuration qualifiers res subdirectory
    - "-land" for landscape
  - landscape and normal must have same layout names

- FrameLayout:
  - no arrangement of children in particular manner
  - use android:layout_gravity of children

- saving data:
  - onSaveInstanceState(Bundle outState):
    - called before onStop
    - used to save state in bundle object
    - Bundle: structure that maps string keys to limited value types

- retrieving data:
  - override onCreate(Bundle savedInstanceState)
  - call super.onCreate(savedInstanceState)
  - data is implicitly passed to onCreateBundle

- Activity LifeCycle Revisited:
  - activity can be destroyed if user navigates away AND Android needs to reclaim memory
  - Only activities that have onStop() called can be destroyed
  - onSaveInstanceState: can be used to save bundle object
    - stored by OS in activity's activity record
  - Stashed: when activity is stopped but Activity Record still exists.
    - activity record destroyed:
      - on reboot
      - back button
  - Permanent Data:
    - override onStop

  - Enable developer options:
    - Settings -> System -> About Emulator (or Phone) -> Build Number (Tap 7 times)
  - Stopped
    - Paused
    - Resumed

- Visible Lifetime (view partially or fully visibly):
  - Paused (partially visible, could be fully visible also)
  - Resumed

- Foreground Lifetime:
  - User interacting with this activity
  - Resumed

- one activity in resumed state at any time

- onCreate(Bundle):
  - OS calls method after activity created but before on screen
  - typically activity overrides onCreate(Bundle)
    - inflate widgets (by calling setContentView(int))
    - get references to inflated widgets
    - set listeners on widgets to handle user interaction
    - connecting external models:w
- never call onCreate(Bundle) or any other Activity; override method

- Logging Activity Lifecyle
  - android.util.Log: sends log messages
  - Log.d(String tag, String msg): sends debug messages

- override methods:
  - @Override: tells compiler overriding method
    - check if really overriding the method
  - super.onStart(): The call to superclass is required
    - should be the first line
- Logcat:
  - SDK window that displays the log
  - loglevels (Log.x):
    - e: error
    - w: warning
    - i: info
    - d: debug
    - v: verbose

- Back Button:
  - onPause -> onStop -> onDestroy

- Home Button:
  - onPause -> onStop:
    - activity hangs out in stopped state in memory
    - use recents button to go back to stopped activity
      - without recent button press and hold the home
- stopped Activity:
  - can be destroyed at the discretion of the OS
- partially visible:
  - new activity with transparent background or smaller screen
    size is launched on top of your activity
  - fully visible scenario occurs in multi-window mode in Android
    6.0 and higher.
- rotate activity:
  - destroys and starts a new activity
  - fixed vs runtime device configuaration:
    - fixed: screen density
    - runtime:
      - screen orientation, keyboard availability, language, multi-window
            - resources that better match might be available
- landscape:
  - create new resource
  - Available Qualifier -> Orientation -> Landscape
  - configuration qualifiers res subdirectory
    - "-land" for landscape
  - landscape and normal must have same layout names

- FrameLayout:
  - no arrangement of children in particular manner
  - use android:layout_gravity of children

- saving data:
  - onSaveInstanceState(Bundle outState):
    - called before onStop
    - used to save state in bundle object
    - Bundle: structure that maps string keys to limited value types

- retrieving data:
  - override onCreate(Bundle savedInstanceState)
  - call super.onCreate(savedInstanceState)
  - data is implicitly passed to onCreateBundle
- Activity LifeCycle Revisited:
  - activity can be destroyed if user navigates away AND Android needs to reclaim memory
  - Only activities that have onStop() called can be destroyed
  - onSaveInstanceState: can be used to save bundle object
    - stored by OS in activity's activity record
  - Stashed: when activity is stopped but Activity Record still exists.
    - activity record destroyed:
      - on reboot
      - back button
  - Permanent Data:
    - override onStop

## Ch 4: Debugging Android Apps

Pass exception to log:

- Log.d(TAG, "message", new Exception())
- use breakpoints
- stop debuggin your app
- stop program
  - disconnect debugger
  - exception breakpoint
    - Run -> View Breakpoints (enable type of breakpoint)
- android lint:
  - compatibility problems
- R-class issues:
  - recheck validity of XML in your resource file. Layout files not always validated
  - clean project (Build -> Clean)
  - Sync your projet with Gradle
  - Run Android Lint
  - check forums.bignerdranch.com

## Ch 5: Your Second Activity

- create activity:
  - touch three files:
    - java class (activity class)
    - xml layout
    - application manifest
  - tools:text (layout xml tag):
    - only shows up for preview but never for runtime
  - AndroidManifest.xml:
    - always named the same
    - lives in app/manifests
    - Android Name Attribute:
      - .CheatActivity: dot in front
      - tells os class is in the package specified by package attribute
  - launcher activity
    - defined in manifest.xml usine the intent-filer
      - android.intent.action.MAIN
      - android.intent.category.LAUNCHER
  - starting an Activity:
    - ask OS to create activity instance and call onCreate method
    - define new activities in the manifest
    - simplest way (parent to child):
      - use startActivity(Intent intent)
      - call sent to OS
    - Activity -> (StartActivity) -> ActivityManager -> xyz
      - intent parameter used to identify xyz (activity)

    - Intent:
      - object component uses to communicate with OS
        - components: [ services, broadcast receivers, content providers]

      - constructors:
        - vary depending on purpose
        - start activity:
          - public Intent(Context PackageContext, Class' cls)
            - PackageContext: which package cls is in
            - cls: what activity class to be started
      - explicit:
        - start activities within your application

      - implicit:
        - start activities in another application

      - passing data between activities:
        - intent extras:
          - putExtra():
            - two arguments:
              - key:
                - globally unique
                - prepend app name
              - value
            - returns intent
          - getExtra():
            - getIntent().get\<type\>Extra(String, default_value)
            - getIntent: retrieves Intent that started activity

      - get from child:
        - startActivityForResult():
          - signature: startActivityForResult(Intent, int requestCode)
            - requestCode:
              - used to distinguish among child activities
                - user defined int
        - results to parent:
        - setResult(int resultCode)
          - setResult(int resultCode, Intent data)
            - resultCode:
              - Activity:
                - RESULT_CANCELED
                - RESULT_OK
                - RESULT_FIRST_USER:
                  - used as offset to define custom return types
        - sending back intent:
        - create intent
          - set data: putExtra
          - use setResult
        - handling result:
          - onActivityResult(int requestCode, int resultCode, intent)
            - create static method on child to extract intent returned to parent
    - Android QuizActivity:
      - launch activity started (QuizActivity)
      - Cheat button -> Instance of CheatActivity
        - if back button QuizActivity on top of stack
    - ActivityManager:
      - back stack
        - maintains activities for all applications
        - use of OS and device as a whole
      - Checks activity existence
        - ActivityNotFoundException: app crash if not found
    - savedInstanceState:
      - data lost during rotation
      - save data to restore info
      - need to check to whether savedInstanceState is null (otherwise crash)
      - created on when onSaveInstanceState called
      - has various get and put methods for various types
      - onSaveInstanceState: special method that gets called by OS
        - pass in bundle called (savedInstanceState)
        - savedInstanceState has get and set methods
        - remember to check if savedInstanceState is null

## Ch 6: Android SDK Versions and Compatibility

- build version and target version:
  - set in the build.gradle file
  - target sdk and minimum sdk versions in gradle sets those in the manifest.xml
    - Sync with Gradle to reflect the changes in build.gradle
    - sdk version same as api level
  - minSdkVersion:
    - lowest sdk version that android would allow for your app installation
    - sdkVersion and API Level used interchangeably
  - Target SDK Version:
    - informs android about what API level the app is designed for
    - typically the latest version
    - might lower if a new SDK would change app appearance
    - developer.android.com/reference/android/os/Build.VERSION_CODES.html
    - is advertized to the OS
  - Compile SDK Version (build target):
    - not placed in manifest.xml
    - private between you and compiler
    - controls classes and methods used for the build
    - best to use latest revision of the APIs
  - Code from later APIs in older SDK:
    - lint displays the API compatibility automatically
    - older device will crash if using API that is not found on device
    - add code to check for API versions:
      - Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP
  - build.gradle:
    - changes to SDK version, target, and compile need to use Tools -> Android -> Sync
  - documentation:
    - developer.android.com
    - develop: documentation and training
      - training
      - api guides
      - reference
      - samples
      - android studio
      - android sdk
      - google services
  - download:
    - Tools -> SDK Manager -> Android SDK
      - click on sdk version of interest
      - click download SDK tools
      - select documentation

## Ch 7: UI Fragments and the Fragment Manager

- fragment:
  - definition: controller object that performs tasks (deputized by Activity)
  - ui-fragment: fragments that manage the ui.
    - contains layout of its own
    - activity view contains spot where fragment appears
    - activity can have more than one fragment
    - fragment is incapable of getting a view by itself. It needs
      to be placed in activity hierarchy
    - types:
      - support: built into library included in application
        - more uniform across devices
      - native: built into device
- AppCompat:
  - google's compatibility library
  - add dependency in build.gradle in app module
- Add Dependency:
  - gradle responsible for downloading dependency compile time
  - groupId:artifactId:version:
    - groupId: unique identifier for set group of libraries in maven
    - artifactId: name of specific library within package
    - version: number for the library
  - AppCompat is the dependency to add:
    - automatically add: File -> Project Structure -> click app -> click dependencies

```java
// in file app/build.gradle add this code:

dependencies {
compile fileTree(dir: 'libs', include: ['*.jar'])
...
// adjust version to be the one you want
compile 'com.android.support:appcompat-v7:25.0.1'
...
}
```
