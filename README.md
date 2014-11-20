# Snackbar
[![Build Status](https://travis-ci.org/nispok/snackbar.svg?branch=master)](https://travis-ci.org/nispok/snackbar)

Library that implements <a href="http://www.google.com/design/spec/components/snackbars-and-toasts.html">Snackbars</a> from Google's <a href="http://www.google.com/design/spec/material-design/introduction.html">Material Design documentation</a>.

![Example App](./art/home.png)
![Example App](./art/home-1line.png) <br />
![Example App](./art/home-2line.png)
![Example App](./art/home-colored.png) <br />
![Example App](./art/list-1line.png)

## Installation
You can import the library from source as a module or grab via Gradle:
 <br />
 ```groovy
 compile 'com.nispok:snackbar:2.1.1'
 ```
## Usage
<br />
Using the <code>Snackbar</code> class is easy, this is how you would display it on a <code>HelloWorldActivity</code>:
<br />
```java
Snackbar.with(getApplicationContext()) // context
    .text("Single-line snackbar") // text to display
    .show(this); // activity where it is displayed
```
If you want an action button to be displayed, just assign a label and an <code>ActionClickListener</code>:
<br />
```java
Snackbar.with(getApplicationContext()) // context
    .text("Item deleted") // text to display
    .actionLabel("Undo") // action button label
    .actionListener(new Snackbar.ActionClickListener() {
        @Override
        public void onActionClicked() {
            Log.d(TAG, "Undoing something");
        }
     }) // action button's ActionClickListener
     .show(this); // activity where it is displayed
```
If you need to know when the <code>Snackbar</code> is shown or dismissed, assign a <code>EventListener</code> to it. This is useful if you need to move other objects while the <code>Snackbar</code> is displayed. For instance, you can move a Floating Action Button up while the <code>Snackbar</code> is on screen:
<br />
```java
Snackbar.with(getApplicationContext()) // context
    .text("This will do something when dismissed") // text to display
    .eventListener(new Snackbar.EventListener() {
        @Override
        public void onShow(int height) {
           myFloatingActionButton.moveUp(height);
        }        
        @Override
        public void onDismiss(int height) {
           myFloatingActionButton.moveDown(height);
        }
    }) // Snackbar's DismissListener
    .show(this); // activity where it is displayed
```
There are two <code>Snackbar</code> types: single-line (default) and multi-line (2 lines max). You can also set the duration of the <code>Snackbar</code> similar to a <a href="http://developer.android.com/reference/android/widget/Toast.html"><code>Toast</code></a>. Animation disabling is also possible.
<br />
```java
Snackbar.with(getApplicationContext()) // context
    .type(Snackbar.SnackbarType.MULTI_LINE) // Set is as a multi-line snackbar
    .text("This is a multi-line snackbar. Keep in mind that snackbars are " +
        "meant for VERY short messages") // text to be displayed
    .duration(Snackbar.SnackbarDuration.LENGTH_SHORT) // make it shorter
    .animation(false) // don't animate it
    .show(this); // where it is displayed
```
You can also change the <code>Snackbar</code>'s colors.
<br />
```java
Snackbar.with(getApplicationContext()) // context
    .text("Different colors this time") // text to be displayed
    .textColor(Color.GREEN) // change the text color
    .color(Color.BLUE) // change the background color
    .actionLabel("Action") // action button label
    .actionColor(Color.RED) // action button label color
    .actionListener(new Snackbar.ActionClickListener() {
        @Override
        public void onActionClicked() {
            Log.d(TAG, "Doing something");
        }
     }) // action button's ActionClickListener    
    .show(this); // activity where it is displayed
```
Finally, you can attach the <code>Snackbar</code> to a AbsListView (ListView, GridView) or a RecyclerView.
<br />
```java
Snackbar.with(getApplicationContext()) // context
    .type(Snackbar.SnackbarType.MULTI_LINE) // Set is as a multi-line snackbar
    .text("This is a multi-line snackbar. Keep in mind that snackbars are " +
        "meant for VERY short messages") // text to be displayed
    .duration(Snackbar.SnackbarDuration.LENGTH_LONG) // make it shorter
    .animation(false) // don't animate it
    .attachToAbsListView(listView) // Attach to ListView - attachToRecyclerView() is for RecyclerViews
    .show(this); // where it is displayed
```
It uses [Roman Nurik's SwipeToDismiss sample code](https://github.com/romannurik/android-swipetodismiss) to implement the swipe-to-dismiss functionality. This is enabled by default. You can disable this if you don't want this functionality:<br />
<br />
```java
Snackbar.with(SnackbarSampleActivity.this) // context
    .text("Can't swipe this") // text to be displayed
    .swipeToDismiss(false) // disable swipe-to-dismiss functionality
    .show(this); // activity where it is displayed
```
If you would like to add features to it or report any bugs, refer to the [issues](https://github.com/nispok/snackbar/issues) section.<br /><br />

# Examples
There's a sample app included in the project. [SnackbarSampleActivity](./sample/src/main/java/com/nispok/sample/snackbar/SnackbarSampleActivity.java) is where you want to start.

# Contributors
+ [William Mora](https://github.com/wmora) - [@_williammora](https://twitter.com/_williammora) - william.r.mora@gmail.com
+ [Lewis Deane](https://github.com/lewisjdeane)
+ [Andrew Hughes](https://github.com/ashughes)
+ [David Richardson](https://github.com/davidjrichardson)

## License
[MIT](./LICENSE)
