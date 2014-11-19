---
title: "Check Activities"
description: "Typically in Android applications an Activity is a 'Screen' in an app."
layout: guide
published: 1
categories:
  - android
order: 603
---

## Details 

Typically in Android applications an Activity is a “Screen” in an app. An activity can be invoked by any application if it is exported, thus allowing the user access to regions of the application often in unintended ways. If you define an Intent filter for an Activity it will automatically make it public and accessible by other applications. Even if an Activity is not public it can still be invoked with root privileges. This could allow an attacker to jump around an application in a way the developer did not intend, such as jumping past a password lock screen to access the data.

## Remediation

Don’t assume that activities must be accessed in the order you intended. To prevent this the Activity can check to see if the app is in the “unlocked” state and if not jump back to the lock screen. Regardless of what Intent filters are defined, publicly accessible Activities can be directly invoked with bad data so input validation is important.  Do not put sensitive data into Intents used to start Activities. A malicious program can insert an Intent filter with higher priority and grab the data.

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

```
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

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8); [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE 927](http://cwe.mitre.org/data/definitions/927.html)
