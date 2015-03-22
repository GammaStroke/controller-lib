# controller-lib
This Android-library should help you to show a common game controller on the screen and react to its user input

At the moment the only supported Buttons are the Directionbuttons (8-way) and the Action-Input of a user, such as on the Playstation- or the XBox-Controller

This library uses VectorDrawable and has downwards support down to API Level 7 (using MrVector)

## Dependencies:
* [MrVector](https://github.com/telly/MrVector) in Version 0.2.0
* appcompat
 
## How to use in your project:
To use this library, add a new repository to your repositories, setup in gradle:
```groovy
allprojects {
    repositories {
        jcenter()
        ...
        maven {
            url "https://jitpack.io"
        }
        ...
    }
}
```
then add this library as a dependency

```groovy
compile 'com.github.Unic8:controller-lib:0.0.2'
```

## Add both of the Views to your layout:

```xml
    <com.unicate.controller.views.DirectionView
        android:id="@+id/viewDirection"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:layout_alignParentLeft="true"
        android:layout_alignParentStart="true"/>

    <com.unicate.controller.views.ActionView
        android:id="@+id/viewAction"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:layout_alignParentRight="true"
        android:layout_alignParentEnd="true" />
```

and in your code create a Helper, add the views to it and set a listener:
```java
ControllerHelper controller = new ControllerHelper((DirectionView) findViewById(R.id.viewDirection), (ActionView) findViewById(R.id.viewAction));
controller.setControllerInputListener(new ControllerHelper.ControllerInputListener() {
    @Override public void onInputChanged(ControllerInput input) {
        Log.e("CHANGE", input.toString());
    }

    @Override public void onInputFinished(ControllerInput input) {
        Log.e("FINISH", input.toString());
    }
});
```

## Customizing:
If you want to customize the views, you can do it in the layout xml. I recommend creating a style for it, but thats up to you.

Since both views extend from InputView, you can customize a lot with this already. Both views will react on this attributes.

### InputView options:

* inputBackground (vector-drawable reference)
  * This attribute takes (for now only) a VectorDrawable (Create a VectorDrawable with Lollipop or MrVector)
  * This VectorDrawable defines the size of the View (I should fix that, yes)
* deadZone (0...1)
  * All Buttons are around the center of the view, like pieces of cake. If the user goes too close to the
center of the view it could happen that he accidentially hits other buttons than he wanted to. To avoid that you can set a deadZone. The value has to be between 0 and 1. 0 means no deadZone, 1 means everything is deadZone ;)
* buttonCenterDistance (0...1)
  * each button on the view can have its own drawable. This value tells the view how far from the center of the view the buttons will be drawn. 0 means all buttons get drawn in the middle of the view. 1 means on the edge of the view. As origin of the buttons, the center of the drawables will be used.
* rotateButtons (0...360)
  * Rotate the whole Button Circle
* vibrate (true|false)
  * Vibrates on touch. Remember the Vibrate permissions!
* debug_drawDeadZone (true|false)
  * This is for debugging only, but if you need it, use it. It draws the deadZone ontop of everything else
* debug_drawPieces (true|false)
  * This is for debugging only, but if you need it, use it. It draws the button pieces, when klicking on them

Example:
```xml
    <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
                    xmlns:app="http://schemas.android.com/apk/res-auto" />
                    ...
    <com.unicate.controller.views.DirectionView
        app:inputBackground="@drawable/my_vectordrawable"
        app:vibrate="true"
        android:id="@+id/viewDirection"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:layout_alignParentLeft="true"
        android:layout_alignParentStart="true"/>
```
### DirectionView options

* button_r_normal - VectorDrawable for the unpressed Button: Right
* button_r_pressed - VectorDrawable for the pressed Button: Right
* button_d_normal - VectorDrawable for the unpressed Button: Down
* button_d_pressed - VectorDrawable for the pressed Button: Down
* button_l_normal - VectorDrawable for the unpressed Button: Left
* button_l_pressed - VectorDrawable for the pressed Button: Left
* button_u_normal - VectorDrawable for the unpressed Button: Up
* button_u_pressed - VectorDrawable for the pressed Button: Up
* diagonal_mode (true|false)
  * When this is set to true, the DirectionView will not draw the between buttons (ul,ur,dr,dl), it will highlight the buttons arround it. So in case of ul it will highlight the buttons Up and Left. The result in the Listener will stay the same in both cases.

These values will only be drawn, if diagonal_mode is set to false
* button_ur_normal
* button_ur_pressed
* button_ul_normal
* button_ul_pressed
* button_dr_normal
* button_dr_pressed
* button_dl_normal
* button_dl_pressed

### ActionView

The buttons are drawn from the right to the bottom, to the left - up and to the right again. So there indexes are as well. This is a bit inconsistent (i.e. to the listener), I should fix that in future releases.

* button1_enabled - VectorDrawable for the right button if not pressed
* button1_pressed - VectorDrawable for the right button if pressed
* button2_enabled - VectorDrawable for the bottom button if not pressed
* button2_pressed - VectorDrawable for the bottom button if pressed
* button3_enabled - VectorDrawable for the left button if not pressed
* button3_pressed - VectorDrawable for the left button if pressed
* button4_enabled - VectorDrawable for the top button if not pressed
* button4_pressed - VectorDrawable for the top button if pressed

# Screenshot
![screenshot_2015-03-21-17-55-19](https://cloud.githubusercontent.com/assets/2174386/6766014/971adf68-cff5-11e4-9f7d-530251462886.png)



