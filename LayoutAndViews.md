# @EActivity #

The @EActivity annotation indicates that an activity is part of `AndroidAnnotations`. Its value parameter must be a valid layout id, that will be used as the [content view](http://developer.android.com/reference/android/app/Activity.html#setContentView%28int%29) for the activity. The activity **must not** be final, and **can** be abstract.

You can leave the value parameter empty, which means that no content view will be set. You will probably want to set the content view yourself in the onCreate() method, before the binding is done.

Usage example:
```
@EActivity(R.layout.main)
public class MyActivity extends Activity {
[...]
```
Equivalent boilerplate code:
```
public class MyActivity extends Activity {
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
    }
[...]
```

And without any layout id:
```
@EActivity
public class MyListActivity extends ListActivity {
[...]
```
Equivalent boilerplate code:
```
public class MyListActivity extends ListActivity {
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
    }
[...]
```

# `@ViewById` #

The `@ViewById` annotation indicates that an activity **field** should be bound with the corresponding View component from the layout. It is the same as calling the [findViewById()](http://developer.android.com/reference/android/app/Activity.html#findViewById%28int%29) method. The view id can be set in the annotation parameter, ie `@ViewById(R.id.myTextView)`. If the view id is not set, the name of the field will be used. The field must not be private.

Usage example:
```
@ViewById
EditText myEditText;

@ViewById(R.id.myTextView)
TextView textView;
```
Equivalent boilerplate code:
```
EditText myEditText;

TextView textView;

@Override
public void onCreate(Bundle savedInstanceState) {
    [...]
    myEditText = (EditText) findViewById(R.id.myEditText);
    textView = (TextView) findViewById(R.id.myTextView);
}
```

# `@AfterViews` #

The `@AfterViews` annotation indicates that a **method** should be called after the views binding has happened.

**When _onCreate()_ is called, `@ViewById` fields are not set yet.** Therefore, you can use `@AfterViews` on methods to write code that depends on views.

Usage example:
```
@EActivity(R.layout.main)
public class MyActivity extends Activity {

    @ViewById
    TextView myTextView;

    @AfterViews
    void updateTextWithDate() {
        myTextView.setText("Date: " + new Date());
    }
[...]
```
Equivalent boilerplate code:
```
public class MyActivity extends Activity {

    TextView myTextView;

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        myTextView = (TextView) findViewById(R.id.myTextView);
        myTextView.setText("Date: " + new Date());
    }
[...]
```

You can annotate **multiple methods** with `@AfterViews`. Don't forget that you should **not** use any view field in **onCreate()**:
```
@EActivity(R.layout.main)
public class MyActivity extends Activity {

    @ViewById
    TextView myTextView;

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // DON'T DO THIS !! It will throw a NullPointerException, myTextView is not set yet.
        // myTextView.setText("Date: " + new Date());
    }
[...]
```

# `@BeforeCreate` #

Any method annotated with `@BeforeCreate` will be called before your **onCreate()** method is called. The method may have a Bundle parameter (which will be the **onCreate** savedInstanceState parameter).

This can be useful to separate code logics, or if you don't like the the look of the **super.onCreate()** code, or if you don't need the savedInstanceState param.

Usage example:
```
@EActivity
public class MyActivity extends Activity {

    @BeforeCreate
    void init() {
        // do some init code
    }

[...]
```
Equivalent boilerplate code:
```
public class MyActivity extends Activity {

    @Override
    public void onCreate(Bundle savedInstanceState) {
        // do some init code
        super.onCreate(savedInstanceState);
    }
[...]
```