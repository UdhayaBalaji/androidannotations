# onBackPressed() #

Since Android 2.0, activities can implement onBackPressed() to modify the default behavior when the user presses the back key.

There was [an article](http://android-developers.blogspot.com/2009/12/back-and-other-hard-keys-three-stories.html) on the Android blog that showed how to reproduce this for pre 2.0 Android versions.

We automatically support that since `AndroidAnnotations` 2.1 (with [issue 46](https://code.google.com/p/androidannotations/issues/detail?id=46)): if an **@EActivity** annotated class has an **onBackPressed()** method, the generated class adds the needed code for support on pre 2.0 Android versions.


For instance:
```
@EActivity
public class MyActivity extends Activity {
    
    public void onBackPressed() {
        // Do something
    }
[...]
}
```
Generates:
```
public final class MyActivity_ extends MyActivity
{

    @Override
    public boolean onKeyDown(int keyCode, KeyEvent event) {
        if (((SdkVersionHelper.getSdkInt()< 5)&&(keyCode == KeyEvent.KEYCODE_BACK))&&(event.getRepeatCount() == 0)) {
            onBackPressed();
        }
        return super.onKeyDown(keyCode, event);
    }
[...]
}
```