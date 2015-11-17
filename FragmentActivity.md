Since release **2.1** of `AndroidAnnotations`, activities containing Fragments should work normally with `AndroidAnnotations`.

```
@EActivity(R.id.main)
public class DetailsActivity extends FragmentActivity {

}
```

However, please notice that there is currently no specific support for Fragments. If you need specific features for Fragments, please leave a comment on [Issue 50](https://code.google.com/p/androidannotations/issues/detail?id=50).