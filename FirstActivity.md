Now that your project is [configured](Configuring.md) to use `AndroidAnnotations`, let's have fun with it!

  * Create a new activity (or use an already existing one)
  * Use @EActivity, `@UiView` and @Click on the activity, following this example :

```
@EActivity(R.layout.main)
public class MyActivity extends Activity {

    @ViewById
    EditText myInput;
        
    @ViewById(R.id.myTextView)
    TextView textView;
        
    @Click
    void myButton() {
         String name = myInput.getText().toString();
    	 textView.setText("Hello "+name);
    }
}
```
The main.xml layout works as usual :
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    >
	<EditText  
	    android:id="@+id/myInput"
	    android:layout_width="fill_parent" 
	    android:layout_height="wrap_content" 
	    />
	<Button  
	    android:id="@+id/myButton"
	    android:layout_width="fill_parent" 
	    android:layout_height="wrap_content" 
	    android:text="Click me!"
	    />        
	<TextView  
		android:id="@+id/myTextView"
	    android:layout_width="fill_parent" 
	    android:layout_height="wrap_content" 
	    />    
</LinearLayout>
```
  * Save the file (Eclipse will compile it, and generate a subclass of `MyActivity`, named `MyActivity_`)
  * Register `MyActivity_` instead of `MyActivity` in your manifest :
```
<activity android:name=".MyActivity_" />
```

You should **always** register your activity with a "`_`" suffix in the Android Manifest. This is because `AndroidAnnotations` **generates a subclass** for each annotated activity. It has the same package and name, plus a "`_`" suffix.

Don't worry too much though, `AndroidAnnotations` will tell you if you forget to register your activities in the `AndroidManifest.xml`.

**To learn more about what you can do with `AndroidAnnotations`, read the [documentation](http://code.google.com/p/androidannotations/wiki/HowItWorks).**