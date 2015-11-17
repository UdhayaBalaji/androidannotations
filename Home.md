"_The ratio of time spent reading `[`code] versus writing is well over 10 to 1 [...] `[`therefore] making it easy to read makes it easier to write._" - **Robert C. Martin**
<table width='100%'><tbody><tr>
<td>
<a href='http://code.google.com/p/androidannotations/wiki/GettingStarted'><img src='http://wiki.androidannotations.googlecode.com/git/logo.png' /></a>
</td>
<td>
<font size='6'><strong>Is your Android code:</strong></font>
<font size='5'>
<ul>
<ul><li><strong>easy to write?</strong>
</li><li><strong>readable?</strong>
</li><li><strong>simple to maintain?</strong>
</ul>
</font>
</td>
<td>
<wiki:gadget url="http://wiki.androidannotations.googlecode.com/git/gadget/plusone.xml" width="200" height="100" border="0"/><a href='https://androidannotations.ci.cloudbees.com/'><img src='http://web-static-cloudfront.s3.amazonaws.com/images/badges/BuiltOnDEV.png' /></a>
</td>
</tr>
<tr>
<td><a href='http://www.ebusinessinformation.fr'><img src='http://wiki.androidannotations.googlecode.com/git/providedbylogo.png' /></a></td>
</tr>
</tbody></table></li></ul>

We provide those good things for **less than 50kb**, without any [perf impact](FAQ#Does_AndroidAnnotations_have_any_perf_impact?.md)! Any question? Please ask them on the dedicated [mailing list](http://groups.google.com/group/androidannotations).
## [AndroidAnnotations 2.2](ReleaseNotes#Latest_release:_2.2.md) is out! ##
```
@EActivity(R.layout.translate) // Sets content view to R.layout.translate
public class TranslateActivity extends Activity {

    @ViewById // Injects R.id.textInput
    EditText textInput;

    @ViewById(R.id.myTextView) // Injects R.id.myTextView
    TextView result;

    @AnimationRes // Injects android.R.anim.fade_in
    Animation fadeIn;

    @Click // When R.id.doTranslate button is clicked 
    void doTranslate() {
         translateInBackground(textInput.getText().toString());
    }

    @Background // Executed in a background thread
    void translateInBackground(String textToTranslate) {
         String translatedText = callGoogleTranslate(textToTranslate);
         showResult(translatedText);
    }
   
    @UiThread // Executed in the ui thread
    void showResult(String translatedText) {
         result.setText(translatedText);
         result.startAnimation(fadeIn);
    }

    // [...]
}
```

# [Get Started!](GettingStarted.md) #

## Apps already using AndroidAnnotations ##
| **Your App Here** | [![](http://androidmarket.googleusercontent.com/android/market/com.mdb.android.airhorn/hi-256-0-bf91620f5ef81688dee3e232aaee2710229ab76c#in.png)](https://market.android.com/details?id=com.mdb.android.airhorn) | [![](https://androidmarket.googleusercontent.com/android/market/info.piwai.marketappshare/hi-124-6#in.png)](https://market.android.com/details?id=info.piwai.marketappshare) | [![](https://androidmarket.googleusercontent.com/android/market/com.excilys.condor.android.application/hi-256-0-63585098d7fa2bd3e772f22e4ab79b00271de73c#in.png)](https://market.android.com/details?id=com.excilys.condor.android.application) |
|:------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Let Us Know!](http://groups.google.com/group/androidannotations) | **Air Horn**                                                                                                                                                                                                     | **App EasyShare**                                                                                                                                                            | **Capico**                                                                                                                                                                                                                                      |
| [![](https://androidmarket.googleusercontent.com/android/market/com.mdb.android.lightsaber/hi-124-6#in.png)](https://market.android.com/details?id=com.mdb.android.lightsaber) | [![](https://androidmarket.googleusercontent.com/android/market/com.mdb.android.electricshaver/hi-256-1-d5612d853cf09162a980bf3f94d12a9a4109960f#in.png)](https://market.android.com/details?id=com.mdb.android.electricshaver) | [![](https://androidmarket.googleusercontent.com/android/market/com.bearstouch.smsscheduler/hi-256-2-d2e052a1c952576c25a38e24d571255c6c207ca2#in.png)](https://market.android.com/details?id=com.bearstouch.smsscheduler) | [![](https://androidmarket.googleusercontent.com/android/market/com.mdb.android.cointoss/hi-256-0-a58434f94067ff93f5e8d4efa1702698e8fbeb5b#in.png)](https://market.android.com/details?id=com.mdb.android.cointoss)                             |
| **Light Saber Jedi** | **Electric Shaver**                                                                                                                                                                                              | **SMS Scheduler**                                                                                                                                                            | **Coin Flip**                                                                                                                                                                                                                                   |
| [![](https://lh4.ggpht.com/3iFk8P-gUnKytgbSyouuzFDXh6Fh146vEjIvqXVOX3UgxDNPoBxf5daPGiDZdenBpCs=w124#in.png)](https://market.android.com/details?id=com.mdb.android.magicball) |
| **Magic 8 Ball**  |


**Want more?** [@Transactional](SQLiteTransactions.md), [@StringRes](Resources.md), [@Extra](Extras.md), [@SystemService](SystemServices.md), [@ItemSelected](HandlingEvents.md), [@LongItemClicked](HandlingEvents.md), [@RoboGuice](RoboGuiceIntegration.md), [@UiThreadDelayed](WorkingWithThreads.md) and **[much more](ReleaseNotes.md)**!

And thanks to our compile time checks, you won't forget to register your activities in the manifest any more.


---

The project logo is based on the [Android logo](http://upload.wikimedia.org/wikipedia/commons/d/d7/Android_robot.svg), created and [shared by Google](http://code.google.com/policies.html) and used according to terms described in the [Creative Commons 3.0 Attribution License](http://creativecommons.org/licenses/by/3.0/).

Android is a trademark of Google Inc. Use of this trademark is subject to [Google Permissions](http://www.google.com/permissions/index.html).