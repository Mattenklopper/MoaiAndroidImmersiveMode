# MoaiAndroidImmersiveMode
Simple integration of Immersive Mode for your Android project. Based on JDance's code found at http://getmoai.com/forums/immersive-mode-t2415/?sid=78608f7778dfdd6844cc9385a700bd15

INSTALLATION:
Place ImmersiveModeHandler.java in the same folder as Moai.java.

Add package "com.ziplinegames.moai.ImmersiveModeHandler" to sExternalClasses array.

In MoaiActivity.java add the following lines in the onCreate function:

Under the line where mMoaiView variable gets created and before screensizes are set:
```java
Point screenSize = ImmersiveModeHandler.getScreenSize();
```

I put this line near the end of the function but it probably doesn't matter.
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