# @Click #

The **@Click** annotation indicates that an activity **method** must be called when the corresponding **view** is **clicked**.

The view id can be set in the annotation parameter, ie **@Click(R.id.myButton)**.

If the view id is **not set**, the **name of the method** will be used.

The method may have zero or one parameter, and this parameter can only be a View (the view that was clicked). The method must not be private. Two different methods cannot handle the same view.

Usage example:
```
@Click(R.id.myButton)
void myButtonWasClicked() {
    [...]
}
@Click
void anotherButton() {
    [...]
}
@Click
void yetAnotherButton(View clickedView) {
    [...]
}
```

Equivalent boilerplate code:


```
@Override
public void onCreate(Bundle savedInstanceState) {

    View myButton = findViewById(R.id.myButton);
    myButton.setOnClickListener(new OnClickListener() {
        public void onClick(View v) {
          myButtonWasClicked();
        }
    });

    View anotherButton = findViewById(R.id.anotherButton);
    anotherButton.setOnClickListener(new OnClickListener() {
        public void onClick(View v) {
          anotherButton();
        }
    });

    View yetAnotherButton = findViewById(R.id.yetAnotherButton);
    yetAnotherButton.setOnClickListener(new OnClickListener() {
        public void onClick(View clickedView) {
          yetAnotherButton(clickedView);
        }
    });
}

void myButtonWasClicked() {
    [...]
}
void anotherButton() {
    [...]
}
void yetAnotherButton(View clickedView) {
    [...]
}
```

# Other events #

`AndroidAnnotations` supports other kind of events, and it works exactly as with @Click.

Currently, `AndroidAnnotations` supports the following [events](http://developer.android.com/guide/topics/ui/ui-events.html#EventListeners) on views:

  * [clicks](http://developer.android.com/reference/android/view/View.OnClickListener.html) with @Click
  * [long clicks](http://developer.android.com/reference/android/view/View.OnLongClickListener.html) with `@LongClick`
  * [touches](http://developer.android.com/reference/android/view/View.OnTouchListener.html) with @Touch
  * [items clicks](http://developer.android.com/reference/android/widget/AdapterView.OnItemClickListener.html) with `@ItemClick`
  * [long item clicks](http://developer.android.com/reference/android/widget/AdapterView.OnItemLongClickListener.html) with `@LongItemClick`
  * [item selection](http://developer.android.com/reference/android/widget/AdapterView.OnItemSelectedListener.html) with `@ItemSelect`