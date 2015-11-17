**This page is deprecated, the 2.2 is out**

**AndroidAnnotations 2.2 RC2** has been released to Maven Central. Please **test it**, and report **any bug**.

> # [Download AndroidAnnotations 2.2-RC2](http://search.maven.org/remotecontent?filepath=com/googlecode/androidannotations/androidannotations/2.2-RC2/androidannotations-2.2-RC2.zip) #

# Main Changes since release 2.1.2 #

## AndroidAnnotations is on Maven Central ##

If you used Maven, you don't need to use our custom repository any more, because we now deploy our releases on Maven Central. So you only need this:

```
<dependencies>
        <!-- [...] -->
	<dependency>
		<groupId>com.googlecode.androidannotations</groupId>
		<artifactId>androidannotations</artifactId>
		<version>2.2-RC2</version>
		<scope>provided</scope>
	</dependency>
	<dependency>
		<groupId>com.googlecode.androidannotations</groupId>
		<artifactId>androidannotations</artifactId>
		<classifier>api</classifier>
		<version>2.2-RC2</version>
	</dependency>
</dependencies>
```

See [Issue 94](https://code.google.com/p/androidannotations/issues/detail?id=94).

## Rest API available ##

You can now easily create Rest client in your AndroidAnnotations projects!

We build on top of the great Spring Android Rest Template, which provides a lot of goodies. AndroidAnnotations aims at using Spring Android Rest Template in an easy way.

Here is a quick tutorial :

**Add [Spring Android Rest Template](http://www.springsource.org/spring-android) to your classpath** Add a json or xml deserializing library to your classpath ([gson](http://code.google.com/p/google-gson/), [jackson](http://jackson.codehaus.org/), etc).
**Create an interface annotated with @Rest, that defines your services :**

```
@Rest("http://myrestapp.herokuapp.com/api/v1")
public interface MyRestClient {
	
	@Get("/book/{bookId}")
	Book getBook(String bookId);

       // You can add as many methods as you want, and use @Post, @Put, etc
	
	RestTemplate getRestTemplate();

}
```

**Inject an implementation in your activity with @RestService**

```
@EActivity
public class MyActivity extends Activity {
  @RestService
  MyRestClient restClient;
}
```

**You can also create an instance of the implementation manually.**

```
MyRestClient restClient = new MyRestClient_();
```

See  [Issue 55](https://code.google.com/p/androidannotations/issues/detail?id=55).

## @EViewGroup ##

If you create custom view groups, you can now use some features of AndroidAnnotations inside those viewgroups. Here is an example :

```
@EViewGroup(R.layout.customViewGroup)
public class CustomViewGroup extends FrameLayout {

    @ViewById(R.id.title)
    TextView tv;

    @ViewById
    TextView subtitle;
    
    public CustomViewGroup(Context context, int i) {
        super(context);
    }

    @Click(R.id.title)
    public void title() {
    }

    @LongClick(R.id.title)
    public void titleLongClick() {
    }

    @Touch(R.id.title)
    public void titleTouched(MotionEvent e) {
    }
}
```

The content of customViewGroup.xml could be this :

```
<merge xmlns:android="http://schemas.android.com/apk/res/android" >
        
        <TextView  
                android:id="@+id/title"
            android:layout_width="fill_parent" 
            android:layout_height="wrap_content" 
            android:text="@string/hello"
            />
            
        <TextView  
                android:id="@+id/subtitle"
            android:layout_width="fill_parent" 
            android:layout_height="wrap_content" 
            android:text="@string/hello"
            />
            
</merge>
```

And you could then start using **CustomViewGroup`_`** in your other xml layout files.

See [Issue 113](https://code.google.com/p/androidannotations/issues/detail?id=113)  &  [issue 63](https://code.google.com/p/androidannotations/issues/detail?id=63).

## Other changes ##

  * [Issue 93](https://code.google.com/p/androidannotations/issues/detail?id=93) : View binding & @AfterViews are executed every time setContentView is called
  * [Issue 95](https://code.google.com/p/androidannotations/issues/detail?id=95) : @HtmlRes & @FromHtml? annotations to inject spanned html strings
  * [Issue 83](https://code.google.com/p/androidannotations/issues/detail?id=83) : @Click & friends with multiple id parameters
  * [Issue 107](https://code.google.com/p/androidannotations/issues/detail?id=107) : abstract annotated activities generate abstract activities instead of final activities
  * [Issue 111](https://code.google.com/p/androidannotations/issues/detail?id=111) : Convention over configuration can now do "camel case => snake case" conversion.
  * [Issue 104](https://code.google.com/p/androidannotations/issues/detail?id=104) : Support for @OptionsMenu? and @OptionsItems?
  * [Issue 127](https://code.google.com/p/androidannotations/issues/detail?id=127) : @NoTitle? and @Fullscreen on activities
  * [Issue 87](https://code.google.com/p/androidannotations/issues/detail?id=87) : @Trace to trace methods and durations

For a more complete list of changes, see the [release notes](ReleaseNotes.md)

# Know Issues #

## Exception in @Rest when using @Get without value ##

If you use @Get and forget to set the value, AndroidAnnotations crashes instead of just having the clean compile error.

See [Issue 134](https://code.google.com/p/androidannotations/issues/detail?id=134).

## Disable warning on @EActivity when the activity is abstract ##

AndroidAnnotations adds a warning to your activity when it's not registered in the AndroidManifest.xml, even if this activity is abstraact

See [Issue 137](https://code.google.com/p/androidannotations/issues/detail?id=137).

## Provide setRestTemplate() implementation in @Rest ##

@Rest and @RestService is not really convenient to use when you need to provide a custom RestTemplate. This shouldn't be hard to implement thought..

See [Issue 135](https://code.google.com/p/androidannotations/issues/detail?id=135).

## Error: @EActivity can only be used on an element that extends android.app.Activity ##

If you use an abstract enhanced activity and do a clean build, it fails and leaves the project in quite a bad state.

See [issue 133](https://code.google.com/p/androidannotations/issues/detail?id=133).