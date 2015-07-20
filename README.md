# MoaiAndroidImmersiveMode
Simple integration of Immersive Mode for your Android project. Based on JDance's code found at http://getmoai.com/forums/immersive-mode-t2415/?sid=78608f7778dfdd6844cc9385a700bd15
This version handles keyboard input better and some other rare cases.

INSTALLATION:
Place ImmersiveModeHandler.java in the same folder as Moai.java.

Add package "com.ziplinegames.moai.ImmersiveModeHandler" to sExternalClasses array in Moai.java.

In MoaiActivity.java import the package:
```java
import android.graphics.Point;
```

Add the following lines in the onCreate function under the line where mMoaiView variable gets created:
```java
Point screenSize = ImmersiveModeHandler.getScreenSize();
Moai.setScreenSize(screenSize.x, screenSize.y);
Moai.setViewSize(screenSize.x, screenSize.y);
```

Put this line near the end of the function but it probably doesn't matter as long as it's after the above.
```java
ImmersiveModeHandler.setupView(mMoaiView);
```

In the onResume function we also have to resume the immersiveModeHanlder:
```java
ImmersiveModeHandler.enableImmersiveMode();
```

You will also want to add a line to the LinearLayoutIMETrap file in the function dispatchKeyEventPreIme:

```java
if ( activityReference != null ) {
    InputMethodManager imm = ( InputMethodManager ) activityReference.getSystemService ( Context.INPUT_METHOD_SERVICE );  
    
    ImmersiveModeHandler.handleKeyDown(event.getKeyCode(), event); //Handle key presses.
    
    if ( imm.isActive () && event.getKeyCode () == KeyEvent.KEYCODE_BACK && event.getAction () == KeyEvent.ACTION_UP  ) {
```