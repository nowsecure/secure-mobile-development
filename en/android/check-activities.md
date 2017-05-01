# Check Activities

Typically in Android applications an Activity is a 'Screen' in an app.

## Details

An Activity can be invoked by any application if it is [`exported` and `enabled`](http://developer.android.com/guide/topics/manifest/activity-element.html). This could allow an attacker to load UI elements in a way the developer may not intend, such as jumping past a password lock screen to access data or functionality. By default Activities are not exported, however, if you define an Intent filter for an Activity it will be exported by the system.

## Remediation

Activities can ensure proper behavior by checking internal app state to verify they are ready to load. For example, first see if the app is in the "unlocked" state and if not jump back to the lock screen. Regardless of what Intent filters are defined, `exported`/`enabled` Activities can be directly invoked with unsanitized data, so input validation is recommended when operating on data provided by an untrusted source.

Sample Code of passing intent extra ID instead of the whole object.

```java
//bad passing the whole paracable object
public static Intent getStartingIntent(Context context,
		User user) {
	Intent i = new Intent(context, UserDetailsActivity.class);
	i.putExtra(EXTRA_USER, user);
	return i;
}

//better to pass just the ID to lookup the user details
public static Intent getStartingIntent(Context context,
		String userId) {
	Intent i = new Intent(context, UserDetailsActivity.class);
	i.putExtra(EXTRA_USER_ID, userId);
  return i;
}
```

Avoid intent filters on Activities if they are private, instead use explicit intent.

```xml
<activity
	android:name="com.app.YourActivity"
	android:label="@string/app_name"
	android:excludeFromRecents="true"
	android:exported="false" >
</activity>
```

## References

 * [http://commonsware.com/blog/2013/09/11/beware-accidental-apis-avoid-intents-extras.html](http://commonsware.com/blog/2013/09/11/beware-accidental-apis-avoid-intents-extras.html)
 * [http://commonsware.com/blog/2014/04/30/if-your-activity-has-intent-filter-export-it.html](http://commonsware.com/blog/2014/04/30/if-your-activity-has-intent-filter-export-it.html)

## CWE/OWASP

 * [M1 - Improper Platform Usage](https://www.owasp.org/index.php/Mobile_Top_10_2016-M1-Improper_Platform_Usage), [M4 - Insecure Authentication](https://www.owasp.org/index.php/Mobile_Top_10_2016-M4-Insecure_Authentication)
 * [CWE-927: Use of Implicit Intent for Sensitive Communication](http://cwe.mitre.org/data/definitions/927.html)
