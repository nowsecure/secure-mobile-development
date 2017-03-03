# 检查 Activities

通常在Android应用程序中，Activity是应用程序中的“屏幕”。

## 详细描述

任何应用程序都可以调用[`exported` 和 `enabled`](http://developer.android.com/guide/topics/manifest/activity-element.html)的Activity . 这可能允许攻击者以开发者可能不想要的方式加载UI元素，例如跳过密码锁定屏幕访问数据或功能。 默认情况下，不会导出Activity，但是，如果为Activity定义了Intent过滤器，系统将导出Activity。

## 建议

Activities 可以通过检查内部应用程序状态来验证它们是否可以加载来确保正确的行为。 例如，首先看看应用程序是否处于“未锁定”状态，如果没有，则跳回到锁定屏幕。 无论定义什么Intent过滤器，`exported` /`enabled`都可以直接使用未定义的数据调用Activity，因此当对不受信任的源提供的数据进行操作时，建议使用输入验证。

传递Intent额外ID的示例代码，而不是整个对象。

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
避免对私有的Activities添加intent过滤器，而是使用显式intent。

```xml
<activity
	android:name="com.app.YourActivity"
	android:label="@string/app_name"
	android:excludeFromRecents="true"
	android:exported="false" >
</activity>
```

## 参考

 * [http://commonsware.com/blog/2013/09/11/beware-accidental-apis-avoid-intents-extras.html](http://commonsware.com/blog/2013/09/11/beware-accidental-apis-avoid-intents-extras.html)
 * [http://commonsware.com/blog/2014/04/30/if-your-activity-has-intent-filter-export-it.html](http://commonsware.com/blog/2014/04/30/if-your-activity-has-intent-filter-export-it.html)

## CWE/OWASP

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8); [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE-927: Use of Implicit Intent for Sensitive Communication](http://cwe.mitre.org/data/definitions/927.html)
