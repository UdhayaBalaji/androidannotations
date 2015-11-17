**Get rid of ASyncTasks!!**

# @Background #
The **@Background** annotation indicates that an activity **method** will run in **a thread** other than the [ui thread](http://developer.android.com/guide/topics/fundamentals.html#threads).

The method must not be private and must not declare throwing any exception.

Usage example:
```
void myMethod() {
    someBackgroundWork("hello", 42);
}

@Background
void someBackgroundWork(String aParam, long anotherParam) {
    [...]
}
```

Equivalent boilerplate code:
```
void myMethod() {
    new Thread() {
        public void run() {
            try {
                 someBackgroundWork("hello", 42);
            } catch (RuntimeException e) {
                Log.e(TAG, "A runtime exception was thrown while executing code in a background thread", e);
            }
        }
    }.start();
}

void someBackgroundWork(String aParam, long anotherParam) {
    [...]
}
```
_In fact, @Background is not strictly equivalent to the previous code : we use a shared cached [thread pool executor](http://download.oracle.com/javase/1.5.0/docs/api/java/util/concurrent/Executors.html#newCachedThreadPool%28%29) to prevent creating too much threads._

# `@UiThread` #
The **`@UiThread`** annotation indicates that an activity **method** will run in the [ui thread](http://developer.android.com/guide/topics/fundamentals.html#threads).

The method must not be private and must not declare throwing any exception.

Usage example:
```
void myMethod() {
    doInUiThread("hello", 42);
}

@UiThread
void doInUiThread(String aParam, long anotherParam) {
    [...]
}
```

Equivalent boilerplate code:
```
void myMethod() {
    runOnUiThread(new Runnable() {
        public void run() {
            try {
                 doInUiThread("hello", 42);
            } catch (RuntimeException e) {
                Log.e(TAG, "A runtime exception was thrown while executing code in the ui thread", e);
            }
        }
    });
}

void doInUiThread(String aParam, long anotherParam) {
    [...]
}
```

# `@UiThreadDelayed` #
The **`@UiThreadDelayed`** annotation indicates that an activity **method** will run in the [ui thread](http://developer.android.com/guide/topics/fundamentals.html#threads), **after** the specified amount of time elapses.

The method must not be private and must not declare throwing any exception.

Usage example:
```
void myMethod() {
    doInUiThreadDelayed("hello", 42);
}

@UiThreadDelayed(2000)
void doInUiThreadDelayed(String aParam, long anotherParam) {
    [...]
}
```

Equivalent boilerplate code:
```

Handler handler = new Handler();

void myMethod() {
    handler.postDelayed(new Runnable() {
        public void run() {
            try {
                 doInUiThreadDelayed("hello", 42);
            } catch (RuntimeException e) {
                Log.e(TAG, "A runtime exception was thrown while executing code in the ui thread", e);
            }
        }
    }, 2000);
}

void doInUiThreadDelayed(String aParam, long anotherParam) {
    [...]
}
```

# Fork / Join for the poor Android dev #

Let's say you want to split a background operation into two separate operations than run concurrently, and then do something on the UI thread when both are done.

Here is a simple way to implement this, thanks to @Background and @UiThread.

```
@EActivity
public class MyActivity extends Activity {

  static class Counter {
    int i;
  } 

  void someForkableWork() {
    Counter c = new Counter();
    doStuffA(c);
    doStuffB(c);
  }

  @Background
  void doStuffA(Counter c) {
    // Do some stuff
    joinWork(c);
  }

  @Background
  void doStuffB(Counter c) {
    // Do some stuff
    joinWork(c);
  }

  @UiThread
  void joinWork(Counter c) {
    if (++c.i < 2) {
      return;
    }

    // Do some stuff on the Ui thread
  }

}
```

# Publish progress made easy #

It's actually quite easy to deal with progress reports when you let AndroidAnnotations handle thread related boilerplate code. Here is a simple example :

```
@EActivity
public class MyActivity extends Activity {


  @Background
  void doSomeStuffInBackground() {
    publishProgress(0);
    // Do some stuff
    publishProgress(10);
    // Do some stuff
    publishProgress(100);
  }

  @UiThread
  void publishProgress(int progress) {
    // Update progress views
  }


}
```

No more **AsyncTask<Param, Progress, Result>**!!