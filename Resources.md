All **@XXXRes** annotations indicate that an activity **field** should be injected with the corresponding [Android resource](http://developer.android.com/guide/topics/resources/index.html) from your 'res' folder. The resource id can be set in the annotation parameter, ie `@StringRes(R.string.hello)`.

If the resource id is **not set**, the **name** of the field will be used. The field must not be private.

# `@StringRes` #

The `@StringRes` annotation can be used to retrieve string resources.

Usage example:
```
@StringRes(R.string.hello)
String myHelloString;

@StringRes
String hello;
```

Equivalent boilerplate code:
```
String myHelloString;

String hello;

@Override
public void onCreate(Bundle savedInstanceState) {
    [...]
    myHelloString = getString(R.string.hello);
    hello = getString(R.string.hello);
}
```

# `@ColorRes` #

The `@ColorRes` annotation can be used to retrieve color resources.

Usage example:
```
@ColorRes(R.color.backgroundColor)
int someColor;

@ColorRes
int backgroundColor;
```

Equivalent boilerplate code:
```
int someColor;

int backgroundColor;

@Override
public void onCreate(Bundle savedInstanceState) {
    [...]
    Resources resources = getResources();
    someColor = resources.getColor(R.color.backgroundColor);
    backgroundColor = resources.getColor(R.color.backgroundColor);
}
```

# `@AnimationRes` #

`@AnimationRes` can be used to inject **`XmlResourceParser`** fields (not very useful) or **Animation** fields (much more interesting).

Usage example:
```
@AnimationRes(R.anim.fadein)
XmlResourceParser xmlResAnim;
    
@AnimationRes
Animation fadein;
```
Equivalent boilerplate code:
```
XmlResourceParser xmlResAnim;
    
Animation fadein;

@Override
public void onCreate(Bundle savedInstanceState) {
    [...]
    fadein = AnimationUtils.loadAnimation(this, R.anim.fadein);
    Resources resources = getResources();
    xmlResAnim = resources.getAnimation(R.anim.fadein);
}
```


# Other `@XXXRes` #

Here is the list of other supported resource annotations:

  * `@BooleanRes`
  * `@ColorStateListRes`
  * `@DimensionRes`
  * `@DimensionPixelOffsetRes`
  * `@DimensionPixelSizeRes`
  * `@DrawableRes`
  * `@IntArrayRes`
  * `@IntegerRes`
  * `@LayoutRes`
  * `@MovieRes`
  * `@TextRes`
  * `@TextArrayRes`
  * `@StringArrayRes`