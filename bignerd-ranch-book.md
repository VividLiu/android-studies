# Big Nerd Ranch
- [Big Nerd Ranch](#big-nerd-ranch)
  - [Java Gotchas](#java-gotchas)
  - [Conventions](#conventions)
  - [Shortcuts](#shortcuts)
  - [Useful Links](#useful-links)
  - [Useful Java utilities](#useful-java-utilities)
  - [Ch 3: Activity Lifecyle](#ch-3-activity-lifecyle)
  - [Ch 4: Debugging Android Apps](#ch-4-debugging-android-apps)
  - [Ch 5: Your Second Activity](#ch-5-your-second-activity)
  - [Ch 6: Android SDK Versions and Compatibility](#ch-6-android-sdk-versions-and-compatibility)
  - [Ch 7: UI Fragments and the Fragment Manager](#ch-7-ui-fragments-and-the-fragment-manager)
    - [Hosting a UI Fragment](#hosting-a-ui-fragment)
      - [Fragment lifecycle](#fragment-lifecycle)
      - [Defining container view](#defining-container-view)
    - [Creating a UI Fragment](#creating-a-ui-fragment)
    - [Implementing fragment lifecycle methods](#implementing-fragment-lifecycle-methods)
    - [Wiring widgets in a fragment](#wiring-widgets-in-a-fragment)
    - [Adding a UI Fragment to the FragmentManager](#adding-a-ui-fragment-to-the-fragmentmanager)
    - [Fragmentmanager and the fragmenet lifecycle](#fragmentmanager-and-the-fragmenet-lifecycle)
    - [Architecture with Fragments](#architecture-with-fragments)
  - [Ch 8: Displaying Lists with RecyclerView](#ch-8-displaying-lists-with-recyclerview)
    - [Singleton's for centralized data storage](#singletons-for-centralized-data-storage)
    - [An Abstract Activity for Hosting a Fragment](#an-abstract-activity-for-hosting-a-fragment)
    - [RecyclerView, Adapter, and ViewHolder](#recyclerview-adapter-and-viewholder)
    - [Binding List Items](#binding-list-items)
    - [Responding to Touch Events](#responding-to-touch-events)
      - [ListView and GridView](#listview-and-gridview)
      - [Singletons](#singletons)


## Java Gotchas

- **implements** vs **extends**
- **class inheritance**


## Conventions

| convention | description |
|------------|-------------|
| sVariableName| prefix variables with "s" to declare them as static |


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

### Hosting a UI Fragment

to host a fragment an activity must:

- define a spot in its layout for the fragment's view
- manage the lifecycle of the fragment instance

#### Fragment lifecycle

Fragment lifecycle:

- fragment lifecycle methods are called by hosting activity and NOT OS
- state reflects activities state

Options for hosting fragment in UI:

- layout fragment: add fragment to the activity's layout
  - inflexible
- add fragment to the activity's code
  - only way to have control at runtime


#### Defining container view

- container view for a fragment will be a frame layout
  - layout is generic and can be used for other fragments

### Creating a UI Fragment

Steps for creating UI fragment

- define widgets in a layout file
- create class and set its view to associate with the layout
- inflate the widgets from the layout in the code

### Implementing fragment lifecycle methods

- onCreate lifecycle method for Fragment is public and not private as the Activity onCreate method
- Fragment has a bundle for saving and retrieving state
- onCreate method for Fragment does **NOT** inflate the view
  - onCreateView is where the view gets inflated

```java
// resource: layout resource
// root: parent view
// attachToRoot: determines whether inflater adds the inflated view to the parent view
Layout.Inflator.inflate(resource, ViewGroup root, attachToRoot)
```

### Wiring widgets in a fragment

```java
// use explicit method to get the view id for fragments
// Activity view find has alias: Activity.findViewById(int)
View.findViewById(int)
```

- listeners on fragments same as those on activities

### Adding a UI Fragment to the FragmentManager

- **fragment transaction** used to add, remove, attach, detech or replace fragments in the fragment list

- **fragment manager** handles list of backstack of fragments. Responsible for adding fragments to the list

Example of adding UI fragment:

```java
@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_crime);

        FragmentManager fm = getSupportFragmentManager();

        // fragment manager identifies fragment by resource id of the framelayout
        Fragment fragment = fm.findFragmentById(R.id.fragment_container);

        // fragment will be null initially. fragment manager saves list of fragments.
        // when activity is recreated the fragment manager will retrieve the list and recreate the listed fragments

        if (fragment == null) {
            fragment = new CrimeFragment();
            // transaction adds the fragment to the backlist
            // methods follow fluid interface
            fm.beginTransaction()
                    .add(R.id.fragment_container, fragment)
                    .commit()
        }
    }

```

### Fragmentmanager and the fragmenet lifecycle

**fragment manager** for an activity is responsible for calling the fragment lifecycle metods

  1. onAttach, onCreate, onCreateView will be called when you add the fragment in the fragment manager
  1. onActivityCreated will be called after Activity's onCreate method is called. This method will be called after the fragment is added
  1. onStart: when activity/fragment becomes visible
  1. onResume: when activity/fragment returns to foreground
  1. onPause, onStop, onDestroyView
  1. onDestroy and onDetach will be called when activity is shutting down

- if a fragment is added to an already resumed activity the onAttach, onCreate, onCreateview, onActivityCreated, onStart and onResumed will be called in succession

### Architecture with Fragments

- use fragments to encapsulate major components
- two or three fragments maximum per page
- for smaller reusable view components extract them into custom views

## Ch 8: Displaying Lists with RecyclerView

### Singleton's for centralized data storage

**singleton** class allows only one instance of itself to be created

- exists as long as it exists in memory
- construct with private constructor and a get method

```java
public class CrimeLab {
    private static CrimeLab sCrimeLab;

    public static CrimeLab get(Context context) {
        if (sCrimeLab == null) {
            sCrimeLab = new CrimeLab(context);
        }
        return sCrimeLab;

    }

    // Can not be called by externals methods
    private CrimeLab(Context context) {
    }
}
```

### An Abstract Activity for Hosting a Fragment

Steps for utilizing an abstract Activity class efficiently

- Create a generic fragment-hosting layout; useful when activities use essentially the same layout but potentially different fragments
- Create an Abstract Activity class that adds fragments to the layout

```java
public abstract class SingleFragmentActivity extends AppCompatActivity {

    // method must be implemented by class implementing this abstract class
    protected abstract Fragment createFragment();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_fragment);

        // fragment that controls the fragment section of the view
        FragmentManager fm = getSupportFragmentManager();
        Fragment fragment = fm.findFragmentById(R.id.fragment_container);

        if (fragment == null) {
            fragment = createFragment();
            fm.beginTransaction()
                    .add(R.id.fragment_container, fragment)
                    .commit();
        }
    }
}
```

- use the abstract class, need to subclass and implement the abstract method

```java
public class CrimeActivity extends SingleFragmentActivity {

    @Override
    protected Fragment createFragment() {
        return new CrimeFragment();
    }

}
```

- need to declare activities in the AndroidManifest.xml. Otherwise the new classes will not be registered.

### RecyclerView, Adapter, and ViewHolder

**RecyclerView** is a subclass of ViewGroup

- Benefits: efficient memory usage for displaying views by keeping copies of visible items
- Reuses view incrementally during scroll
- responsible for recycling views and positioning them on screen
- never creates Views by themselves, it always creates ViewHolders, which bring their itemViews along for the ride
- communicates with its Adapter to:
  - getItemCount(): returns total items
  - calls the Adapters onCreateViewHolder method
  - receives the ViewHolder from Adapter
- dependency can be added using File -> Project Structure... -> Select app module on the left -> then the Dependency tab using the "+" button
  - choose Library dependency to add a dependency

- as soon as you create a RecyclerView you need to attach it to a LayoutManager, otherwise if your run your app it will crash
- each item in RecyclerView needs its own view hierarchy

- example of creating a layout file with RecyclerView


```xml
<android.support.v7.widget.RecyclerView
xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/crime_recycler_view"
    android:layout_width="match_parent"
    android:layout_height="match_parent"/>
```

**ViewHolder** it does a single job by holding on to the View

- its itemView keeps reference of the view
- itemView is the reason why ViewHolder exists 

```java
// sample implementation
    private class CrimeHolder extends RecyclerView.ViewHolder {
        public CrimeHolder(LayoutInflater inflater, ViewGroup parent) {
            super(inflater.inflate(R.layout.list_item_crime, parent, false));
        }
    }

```

**Adapters** are a controller object between controller object that sits between RecyclerView and the data set that the RecyclerView should display

- creates the necessary ViewHolders
- binding ViewHolders to data from the model layer

```java
private class CrimeAdapter extends RecyclerView.Adapter<CrimeHolder> {
        private List<Crime> mCrimes;

        public CrimeAdapter(List<Crime> crimes) {
            mCrimes = crimes;
        }

        @NonNull
        @Override
        // create a new ViewHolder
        public CrimeHolder onCreateViewHolder(@NonNull ViewGroup parent, int i) {
            LayoutInflater layoutInflater = LayoutInflater.from(getActivity());

            return new CrimeHolder(layoutInflater, parent);
        }

        @Override
        // bind the data to the CrimeHolder
        public void onBindViewHolder(@NonNull CrimeHolder crimeHolder, int i) {

        }

        @Override
        public int getItemCount() {
            return mCrimes.size();
        }
    }

}
```

Need to connect Adapter to RecyclerView

- implement a method called updateUI in fragment that performs this

```java
public class CrimeListFragment extends Fragment {
  ...
private CrimeAdapter mAdapter;
private void updateUI() {
  CrimeLab crimeLab = CrimeLab.get(getActivity());
  List<Crime> crimes = crimeLab.getCrimes();

  mAdapter = new CrimeAdapter(crimes);
  mCrimeRecyclerView.setAdapter(mAdapter);
}
...
}
...
```

### Binding List Items

**ViewHolder** contains all the real code for performing data binding

- associate widget with the field should happen in constructor
- bind method in ViewHolder gets called repeatedly when updating the View
- Adapter onBindViewHolder method calls the ViewHolder.bind method

```java
    private class CrimeHolder extends RecyclerView.ViewHolder {

        // store the association to widget
        private TextView mTitleTextView;
        private TextView mDateTextView;

        private Crime mCrime;

        public CrimeHolder(LayoutInflater inflater, ViewGroup parent) {
            super(inflater.inflate(R.layout.list_item_crime, parent, false));

            // extract the association to widget
            mTitleTextView = (TextView) itemView.findViewById(R.id.crime_title);
            mDateTextView = (TextView) itemView.findViewById(R.id.crime_date);
        }

        // performs the binding for data updates
        public void bind(Crime crime) {
            mCrime = crime;
            mTitleTextView.setText(mCrime.getTitle());
            mDateTextView.setText(mCrime.getDate().toString());
        }



    }


    private class CrimeAdapter extends RecyclerView.Adapter<CrimeHolder> {
        ...

        @Override
        public void onBindViewHolder(@NonNull CrimeHolder holder, int position) {
            Crime crime = mCrimes.get(position);
            holder.bind(crime);
        }

        ...
    }

```

### Responding to Touch Events

RecyclerView simply forwards raw touch events

- it is up to user to deal with touch events
- use OnClickListener to handle them. Implement listener on ViewHolder

```java

private class CrimeHolder extends RecyclerView.ViewHolder
            implements View.OnClickListener {
       ...

        @Override
        public void onClick(View v) {
            // can process event in here
            Toast.makeText(getActivity(),
                    mCrime.getTitle() + " clicked!", Toast.LENGTH_SHORT)
                    .show();

        }
      ...
    }
```

#### ListView and GridView

Core Android contains ListView, GridView and Adapter

- used to be preferred methods for creating lists and grids
- superceded by RecyclerView
  - More extensible
  - Easier for creating animations

#### Singletons

Singletons:

- outlive fragment and activities; exist accross rotations
- useful when many activities and fragments are modifying a model
- should not be used for permanent storage
- are destroyed when Android reclaims memory
- hard to unit test because calling static method
- alternative to singleton is a **dependency injector**
  - allows for objects to be shared as a Singleton but makes it possible to be swapped out during unit testing

