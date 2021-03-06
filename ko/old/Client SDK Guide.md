## Notification > Push > Client SDK Developer's Guide
이전 버전보기: <select onchange="location.href=this.value">
<option selected value="/ko/Notification/Push/ko/Client%20SDK%20Guide">v1.4</option>
<option value="/ko/Notification/Push/ko/Client%20SDK%20Guide%20v1.32">v1.32</option></select>

TOAST Cloud Push SDK를 적용하면 모바일 애플리케이션과 TOAST Cloud Push를 쉽게 연동할 수 있다.

## 푸시 SDK Download

SDK를 다운로드하려면 메뉴에서 [Downloads > Latest Version]을 클릭한 후, 왼쪽 메뉴에서 [Notification > Push]를 클릭한다.

## 텐센트(TENCENT) 푸시 SDK Download

GCM(Google Cloud Messaging) 사용이 불가능한 중국에서 푸시 메시지 발송이 필요할 경우, 텐센트(TENCENT) 푸시 서비스를 이용할 수 있다.
TENCENT 푸시 SDK와 통합하는 방법에 대해 설명한다.

[Tencent Push SDK 다운로드 페이지](http://xg.qq.com/xg/ctr_index/download)

가이드는 TENCENT(Xg Push) 3.0 버전 기준으로 작성되었다.

## 토큰 등록

기기 식별을 위한 토큰(Token)을 서버에 등록하는 과정이다. 등록이 성공하면 해당 기기에서 푸시 메시지를 수신할 수 있다.

### iOS, APNS

**YourAppDelegate.m**

```
@implementation YourAppDelegate
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSDictionary* options = @{
                              kTCPushKeyServerUrl : @"https://api-push.cloud.toast.com",
                              kTCPushKeyPushType : kTCPushTypeAPNS,
                              kTCPushKeyAgreeNotification : @YES,
                              kTCPushKeyCountry : @"KR",
                              kTCPushKeyLanguage : @"ko",
                              kTCPushKeyTimeout : @(30)
                            };
    int errorCode = [TCPushSdk registerWithAppKey:@"your_app_key" userId:@"your_userid" onRegister:^(int error) {
        [self handleError:error];
    } options:options];

    if(errorCode != kTCPushErrorNone)
    {
        [self handleError:errorCode];
    }
    return YES;
}

- (void)handleError:(int)error
{
    // TODO Handle error code.
}
...
@end
```

### Android, GCM

**AndroidManifest.xml**

아래에 'your.package.name'으로 되어 있는 모든 부분을 애플리케이션 기본 페키지 네임으로 변경한다.

```
<manifest xmlns:android="http://schemas.android.com/apk/res/android" package="your.package.name">
  <application android:icon="@drawable/app_icon">
        <receiver android:name="com.google.android.gms.gcm.GcmReceiver" android:exported="true"
                android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="your.package.name" />
            </intent-filter>
        </receiver>
    <service android:name="com.toast.android.pushsdk.PushSdk$GcmListener" android:exported="false">
      <intent-filter>
        <action android:name="com.google.android.c2dm.intent.RECEIVE" />
      </intent-filter>
    </service>
        <service android:name="com.toast.android.pushsdk.PushService$IdListener" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
  </application>
  <permission android:name="your.package.name.permission.C2D_MESSAGE" android:protectionLevel="signature"/>
  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.WAKE_LOCK" />
  <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
  <uses-permission android:name="your.package.name.permission.C2D_MESSAGE" />
</manifest>
```

**YourActivity.java**
YOUR_APPKEY, YOUR_UID, YOUR_SENDER_ID에 값을 설정한다.

```
package com.toast.cloud.push.demo.app.your;

public class YourActivity extends Activity {
    private final String YOUR_APPKEY = "YOUR_APPKEY";
    private final String YOUR_UID = "YOUR_UID";

    private final Activity YOUR_ACTIVITY = this;
    private final String YOUR_SENDER_ID = "YOUR_SENDER_ID";
    private final String YOUR_PUSH_TYPE = PushSdk.PUSH_TYPE_GCM;
    private final long YOUR_ACCESS_ID = Long.MIN_VALUE;
    private final String YOUR_ACCESS_KEY = "YOUR_ACCESS_KEY";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        final Map<String, Object> options = new HashMap<String, Object>();
        options.put(PushSdk.KEY_ACTIVITY, YOUR_ACTIVITY); // Required.
         // Only GCM
        if (PushSdk.PUSH_TYPE_GCM.equals(YOUR_PUSH_TYPE)) {
        	options.put(PushSdk.KEY_SENDER_ID, YOUR_SENDER_ID); // Required.
        }
        options.put(PushSdk.KEY_SERVER_URL, "https://api-push.cloud.toast.com");
        // Optional. Default: https://api-push.cloud.toast.com
        options.put(PushSdk.KEY_CHANNEL, "default"); // Optional(v1.3)
        options.put(PushSdk.KEY_PUSH_TYPE, YOUR_PUSH_TYPE);
        // Optional.  PushSdk.PUSH_TYPE_GCM or PushSdk.PUSH_TYPE_TENCENT. Default: PushSdk.PUSH_TYPE_GCM.
        // Only TENCENT
        if (PushSdk.PUSH_TYPE_TENCENT.equals(YOUR_PUSH_TYPE)) {
            options.put(PushSdk.KEY_ACCESS_ID, YOUR_ACCESS_ID); // Required.
            options.put(PushSdk.KEY_ACCESS_KEY, YOUR_ACCESS_KEY); // Required.
        }
        options.put(PushSdk.KEY_AGREE_NOTIFICATION, true); // Optional. Default: false.
        options.put(PushSdk.KEY_AGREE_AD, true); // Optional. Default: false.
        options.put(PushSdk.KEY_AGREE_NIGHT_AD, true); // Optional. Default: false.
        options.put(PushSdk.KEY_COUNTRY, "KR"); // Optional. Default: "US".
        options.put(PushSdk.KEY_LANGUAGE, "ko"); // Optional. Default: "en".
        options.put(PushSdk.KEY_TIMEOUT, 30.0); // Optional. Time Unit: Second. Default: 30.

        final int error = PushSdk.register(YOUR_APPKEY, YOUR_UID, new PushSdk.OnRegister() {
            @Override
            public void fire(int error) {
                // TODO Implement handling error
            }
        }, options);
        // TDDo Implement handling error
    }
}
```
- 위 설명은 Android SDK v1.3 이상에만 적용된다. v1.3이하 사용자는 아래와 같이 토큰 등록시 채널을 꼭 등록해야 한다.
```java
 options.put(PushSdk.KEY_CHANNEL, "default");
```

**build.gradle**

```
apply plugin: 'com.android.application'

android {
    compileSdkVersion 23
    buildToolsVersion "23.0.1"

    defaultConfig {
        minSdkVersion 11
        targetSdkVersion 19
        versionCode 1
        versionName "10"
        multiDexEnabled true
    }
    sourceSets {
        main {
            jniLibs.srcDirs = ['libs']
        }
    }
    buildTypes {
        release {
            minifyEnabled false
        }
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.android.support:appcompat-v7:23.1.0'
    compile 'com.android.support:support-v4:23.1.0'
    compile 'com.google.android.gms:play-services-gcm:9.6.0'
}
```

### Android, TENCENT

**AndroidManifest.xml**
다음 내용을 추가한다.
'your.package.name' 항목에 앱의 패키지 이름을 입력해야 한다.

```
<manifest xmlns:android="http://schemas.android.com/apk/res/android" package="your.package.name">
  <application android:icon="@drawable/app_icon">
    <receiver android:name="com.tencent.android.tpush.XGPushReceiver" android:process=":xg_service_v3" >
      <intent-filter android:priority="0x7fffffff" >
        <action android:name="com.tencent.android.tpush.action.SDK" />
        <action android:name="com.tencent.android.tpush.action.INTERNAL_PUSH_MESSAGE" />
        <action android:name="android.intent.action.USER_PRESENT" />
        <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
      </intent-filter>
    </receiver>
    <service android:name="com.tencent.android.tpush.service.XGPushServiceV3" android:exported="true" android:persistent="true" android:process=":xg_service_v3">
    </service>
    <receiver android:name="com.toast.android.pushsdk.PushSdk$XgListener">
      <intent-filter>
        <action android:name="com.tencent.android.tpush.action.PUSH_MESSAGE" />
        <action android:name="com.tencent.android.tpush.action.FEEDBACK" />
      </intent-filter>
    </receiver>
    <service android:name="com.tencent.android.tpush.service.XGDaemonService" android:process=":xg_service_v3" />
    <provider
    android:name="com.tencent.android.tpush.XGPushProvider"
    android:authorities="your.package.name.AUTH_XGPUSH"
    android:exported="true"/>
    <provider
        android:name="com.tencent.android.tpush.SettingsContentProvider"
        android:authorities="your.package.name.TPUSH_PROVIDER"
        android:exported="false" />
    <provider
        android:name="com.tencent.mid.api.MidProvider"
        android:authorities="your.package.name.TENCENT.MID.V3"
        android:exported="true" >
    </provider>
  </application>
  <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
  <uses-permission android:name="android.permission.BROADCAST_STICKY" />
  <uses-permission android:name="android.permission.KILL_BACKGROUND_PROCESSES" />
  <uses-permission android:name="android.permission.GET_TASKS" />
  <!--permissions requiring user alerts-->
  <uses-permission android:name="android.permission.READ_PHONE_STATE" />
  <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
  <uses-permission android:name="android.permission.RECEIVE_USER_PRESENT" />
  <uses-permission android:name="android.permission.RESTART_PACKAGES" />
  <uses-permission android:name="android.permission.WRITE_SETTINGS" />
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
  <uses-permission android:name="android.permission.READ_LOGS" />

  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.WAKE_LOCK" />
  <uses-permission android:name="android.permission.VIBRATE" />
</manifest>
```

- 현재 Android M (6.0 MarshMallow)에서 정상적인 동작을 하지 않을 수 있다. TENCENT SDK 패치가 필요한 부분이며, 패치될 예정이다.

위와 같이 설정한, options에 PushSdk.pushType을 PushSdk.PUSH_TYPE_TENCENT로 설정한다.
그리고, PushSdk.KEY_ACCESS_ID, PushSdk.KEY_ACCESS_KEY에 발급받은 ACCESS ID와 ACCESS KEY를 설정한다.
ACCESS ID, ACCESS KEY 발급은 [Developer's Guide]를 참고한다.


### Options

options는 플랫폼에 따라 Dictionary나 Map, 또는 그에 준하는 Key/Value Collection으로 정의된다. 각각의 Key/Value는 다음과 같다.

|Key|	Type|	Values|	Platform|
|---|---|---|---|
|KEY_PUSH_TYPE(pushType)|	string|	PushSdk.PUSH_TYPE_APNS, PushSdk.PUSH_TYPE_APNS_SANDBOX, <br/> PushSdk.PUSH_TYPE_GCM, PushSdk.PUSH_TYPE_TENCENT|	iOS, Android|
|KEY_AGREE_NOTIFICATION <br/> (isNotificationAgreement)|	boolean|	알림 푸시 메시지 수신 여부|	iOS, Android|
|KEY_AGREE_AD <br/> (isAdAgreement)|	boolean|	광고 푸시 메시지 알림 수신 여부|	iOS, Android|
|KEY_AGREE_NIGHT_AD <br/> (isNightAdAgreement)|	boolean|	야간 광고 푸시 메시지 알림 수신 여부|	iOS, Android|
|KEY_COUNTRY(country)|	string|	국가 코드 (3 byte 제한). <br/> ISO 3166-1 alpha-2, ISO 3166-1 alpha-3|	iOS, Android|
|KEY_LANGUAGE(language)|	string|  언어 코드 (8 byte 제한). <br/> ISO 639-1, ISO 639-2, <br/> iOS(language code + script code)|	iOS, Android|
|KEY_TIMEOUT(timeout)|	double|	토큰 등록 또는 조회시 사용되는 시간이다. 단위는 초다.|	iOS, Android|
|KEY_ACTIVITY(activity)|	object|	android.app.Activity|	Android|
|KEY_SENDER_ID(senderId)|	string|	GCM을 사용하기 위해 필요하다. <br/> [[Google Developer Console](https://console.developers.google.com/project)]에서 확인할 수 있다.|	Android(GCM)|
|KEY_ACCESS_ID(accessId)|	string|	TENCENT를 사용하기 위해 필요하다. <br/> [[Tencent 푸시 서비스 대시보드](http://xg.qq.com/xg/ctr_index/login?go_to_url=http%3A%2F%2Fxg.qq.com%2Fxg%2Fapps%2Fctr_app%2Findex)]에서 확인할 수 있다.|	Android(TENCENT)|
|KEY_ACCESS_KEY <br/> (accessKey)|	string|	TENCENT를 사용하기 위해 필요하다. <br/> [[Tencent 푸시 서비스 대시보드](http://xg.qq.com/xg/ctr_index/login?go_to_url=http%3A%2F%2Fxg.qq.com%2Fxg%2Fapps%2Fctr_app%2Findex)]에서 확인할 수 있다.|	Android(TENCENT)|

## 푸시 메시지 수신

### Android, GCM

SDK를 사용하면 추가적인 구현 없이 기본적으로 푸시 메시지를 수신하고 화면에 메시지가 표시된다. 필요에 따라 커스텀한 푸시 메시지를 표시하고 싶다면, 아래와 같이 Custom Receiver를 등록한다.

**YourGcmListener.java**

```
package com.toast.cloud.push.demo.app.your;

public class YourGcmListener extends PushSdk.GcmListener {
    private static final int NOTIFICATION_ID = 1;

    @Override
    public void onMessageReceived(String from, Bundle data) {
        final NotificationManager notificationManager = (NotificationManager)
                this.getSystemService(Context.NOTIFICATION_SERVICE);

        final PendingIntent contentIntent = PendingIntent.getActivity(this, 0, new Intent(this, DemoActivity.class), 0);
        final String text = data.toString();
        NotificationCompat.Builder mBuilder =
                new NotificationCompat.Builder(this)
                        .setSmallIcon(R.drawable.ic_stat_gcm)
                        .setContentTitle("GCM Notification")
                        .setStyle(new NotificationCompat.BigTextStyle().bigText(text))
                        .setContentText(text);

        mBuilder.setContentIntent(contentIntent);
        notificationManager.notify(NOTIFICATION_ID, mBuilder.build());
    }
}
```

**AndroidManifest.xml**
PushSdk$GcmListener를 YourGcmListener로 수정한다.

```
    ...
    <service android:name="your.package.name.YourGcmListener" android:exported="false">
     <intent-filter>
       <action android:name="com.google.android.c2dm.intent.RECEIVE" />
      </intent-filter>
    </service>
    ...
```

### Android, TENCENT

SDK를 사용하면 추가적인 구현 없이 기본적으로 푸시 메시지를 수신하고 화면에 메시지가 표시된다. 필요에 따라 커스텀한 푸시 메시지를 표시하고 싶다면, 아래와 같이 Custom Receiver를 등록한다.

**YourXgListener.java**

```
package your.package.name;

public class YourXgListener extends PushSdk.XgListener {
    private static final int NOTIFICATION_ID = 2;

    @Override
    public void onTextMessage(Context context, XGPushTextMessage message) {
        final NotificationManager notificationManager = (NotificationManager)
                context.getSystemService(Context.NOTIFICATION_SERVICE);

        final PendingIntent contentIntent = PendingIntent.getActivity
        (context, 0, new Intent(context, DemoActivity.class), 0);
        final String text = "title: " + message.getTitle() + ", content: " + message.getContent() + ", customContent: "
         + message.getCustomContent();
        NotificationCompat.Builder mBuilder =
                new NotificationCompat.Builder(context)
                        .setSmallIcon(R.drawable.ic_stat_gcm)
                        .setContentTitle("TENCENT Notification")
                        .setStyle(new NotificationCompat.BigTextStyle().bigText(text))
                        .setContentText(text);

        mBuilder.setContentIntent(contentIntent);
        notificationManager.notify(XgListener.NOTIFICATION_ID, mBuilder.build());
    }
}
```

**AndroidManifest.xml**

PushSdk$XgListener 부분을 위에서 작성한 커스텀 클래스로 변경한다.

```
	...
	<receiver android:name="com.toast.cloud.push.demo.app.XgListener">
		<intent-filter>
			<action android:name="com.tencent.android.tpush.action.PUSH_MESSAGE" />
			<action android:name="com.tencent.android.tpush.action.FEEDBACK" />
		</intent-filter>
	</receiver>
	...
```

## 토큰 조회

APPKEY, UID, options로 등록된 Token을 조회할 수 있다.
요청의 결과로 아래 { 키 : 값 } 이 반환된다.

```
{
    "pushType" : "GCM",
    "isNotificationAgreement": true,
    "isAdAgreement": true,
    "isNightAdAgreement": true,
    "timezoneId" : "Asia/Seoul",
    "country": "KR",
    "language": "ko",
    "uid" : "User ID",
    "token" : "Token"
}
```

### iOS, APNS

**pushsdk.m**

```
void HandleQuery(int error, NSDictionary* options);
......
NSDictionary* options = @{kTCPushKeyServerUrl : @"https://api-push.cloud.toast.com", // Optional, Default : https://api-push.cloud.toast.com
                            kTCPushKeyPushType : kTCPushTypeAPNS, // Optional, Default : kTCPushTypeAPNS
                            kTCPushKeyTimeout : @(30)}; // Optional, Default : 30
[TCPushSdk queryForAppKey:appKey userId:userId onQuery:^(int error, NSDictionary* options) { // options 매개변수는 nil이면 안됨
	if(!options)
    {
        NSString* token = options[@"token"];
        // TODO Handle a token
    }
	} options:options];
......
```

### Android, GCM, TENCENT

**YourActivity.java**

```
    private void getRegisteredToken(final Map<string, object=""> options) {
        HashMap<String, Object> options = new HashMap<String, Object>() {
            {
                put(PushSdk.KEY_ACTIVITY, MainActivity.this); // Required.
                put(PushSdk.KEY_PUSH_TYPE, pushType); // Optional, Default : PUSH_TYPE_GCM
                put(PushSdk.KEY_TIMEOUT, 30.0); // Optional. Time Unit: Second. Default: 30.
            }
        };
        PushSdk.query(YOUR_APPKEY, YOUR_UID, new PushSdk.OnQuery() {
            @Override
            public void fire(int i, Map<string, object=""> map) {
                String token = (String)map.get("token");
                // TODO Handle a token
            }
        }, options);
    }
```

## 수신 및 오픈 여부 적용
- 클라이언트에서 푸시 수신 및 확인 여부 등에 대한 정보를 서버에 전송할 수 있다.
- 지표는 웹 콘솔을 통해서 볼 수 있다.

### Android, GCM

**YourActivity.java**

- **PushAnalytics.onOpened** 메소드를 호출한다.

```
public class YourActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        PushAnalytics.initialize(this, "https://collector-push.cloud.toast.com", "appKey");
        PushAnalytics.onOpened(this, getIntent());
        // ... your codes
    }

    @Override
    protected void onNewIntent(Intent intent) {
        PushAnalytics.onOpened(this, intent);
        // ... your codes
    }
}
```

**YourListener.java**

- 만약 ToastCloud Push SDK에서 제공하는 기본 리스너(PushSdk.GcmListener)를 사용할 경우, 자동으로 수신 및 오픈 여부를 사용할 수 있다. 따라서, 기본 리스너를 사용한다면 이 부분을 생략해도 된다.
    - **단, 기본 리스너를 사용하더라도 Activity에서 PushAnalytics.initialize와 PushAnalytics.onOpened 메소드는 호출해야 한다.**
- PendingIntent 생성 시, 액티비티 전환 Intent를 **PushAnalytics.newIntentForOpenedEvent**를 이용해서 생성한다.
- PendingIntent.getActivity 메소드 호출 시, 마지막 매개변수인 Flag를 **PendingIntent.FLAG_UPDATE_CURRENT**로 전달한다.
- 수신 확인을 위해 **PushAnalytics.onReceived** 메소드를 호출한다.

```
public class YourGcmListener extends PushSdk.GcmListener {
    private static final int NOTIFICATION_ID = 1;

    @Override
    public void onMessageReceived(String from, Bundle data) {
        final NotificationManager notificationManager = (NotificationManager)
                this.getSystemService(Context.NOTIFICATION_SERVICE);

        Intent launchIntent = PushAnalytics.newIntentForOpenedEvent(this, DemoActivity.class, data);
        final PendingIntent contentIntent = PendingIntent.getActivity(this, 0, launchIntent, PendingIntent.FLAG_UPDATE_CURRENT);
        final String text = data.toString();
        NotificationCompat.Builder mBuilder =
                new NotificationCompat.Builder(this)
                        .setSmallIcon(R.drawable.ic_stat_gcm)
                        .setContentTitle("GCM Notification")
                        .setStyle(new NotificationCompat.BigTextStyle().bigText(text))
                        .setContentText(text);

        mBuilder.setContentIntent(contentIntent);
        notificationManager.notify(NOTIFICATION_ID, mBuilder.build());

        PushAnalytics.onReceived(this, data);
    }
}
```

### iOS
- iOS의 수신 및 오픈 여부는 iOS 10 이상에서만 동작하며, UserNotification 프레임워크의 Notification Service Extension을 이용한다.

#### Notification Service Extension 을 이용한 수신 여부 적용
- 현재 프로젝트에 Notification Service Extension 타겟을 추가한다.
    - File > New > Target > Notification Service Extension을 선택한다.
- 추가된 Notification Service Extension(이하 NSE)의 프로젝트 설정에 Push SDK 라이브러리를 추가한다.
    - 이미 Push SDK가 프로젝트에 있다면, 추가적인 복사 작업 없이 라이브러리를 추가하면 된다.
- **NotificationService.m** 파일에 들어가면 기본적인 샘플 코드가 생성돼 있다.
- 다음과 같이 코드를 수정하면 수신 여부 확인 기능이 적용된다.
    - URL과 앱키는 웹 콘솔에서 받은 정보를 입력해주면 된다.

**NotificationService.m**

```
#import "NotificationService.h"
#import "pushsdk.h"

@interface NotificationService ()

@property (nonatomic, strong) void (^contentHandler)(UNNotificationContent *contentToDeliver);
@property (nonatomic, strong) UNMutableNotificationContent *bestAttemptContent;

@end

@implementation NotificationService

- (void)didReceiveNotificationRequest:(UNNotificationRequest *)request withContentHandler:(void (^)(UNNotificationContent * _Nonnull))contentHandler {
    self.contentHandler = contentHandler;
    self.bestAttemptContent = [request.content mutableCopy];

	[TCPushAnalytics onReceivedNotificationWithUrl:@"URL"
											appKey:@"APPKEY"
										  userInfo:request.content.userInfo
								 completionHandler:^{
		self.contentHandler(self.bestAttemptContent);
	}];
}

- (void)serviceExtensionTimeWillExpire {
    // Called just before the extension will be terminated by the system.
    // Use this as an opportunity to deliver your "best attempt" at modified content, otherwise the original push payload will be used.
    self.contentHandler(self.bestAttemptContent);
}

@end
```

#### UserNotification 프레임워크를 이용한 오픈 여부 적용
- 자신의 AppDelegate에 UNUserNotificationCenterDelegate 딜리게이트를 적용한다.
- 그리고 AppDelegate 구현에 **(void)userNotificationCenter:didReceiveNotificationResponse:withCompletionHandler:** 메소드를 추가한다.
- 메소드 내부에 오픈 여부를 위한 API를 호출한다.
    - URL과 앱키는 웹콘솔에서 받은 정보를 입력해주면 된다.

**AppDelegate.h**

```
@interface AppDelegate : UIResponder <UIApplicationDelegate, UNUserNotificationCenterDelegate>
```

**AppDelegate.m**

```
#import "AppDelegate.h"
#import "pushsdk.h"
@interface AppDelegate ()
@end
@implementation AppDelegate
- (BOOL)application:(UIApplication *)app didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter];
    center.delegate = self;
    return YES;
}
- (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void (^)())completionHandler {
    [TCPushAnalytics onOpenedNotificationWithUrl:@"URL"
                                          appKey:@"APPKEY"
                                        userInfo:response.notification.request.content.userInfo
                               completionHandler:^{
                                   completionHandler();
                               }];
}
@end
```

## 오류 처리

각각의 오류에 대해 다음과 같은 처리를 권장한다.

|에러 코드|	요약|	처리 방법|
|---|---|---|
|ERROR_NONE(0)|	오류 없음|	요청 성공이므로 따로 에러 처리할 필요 없다.|
|ERROR_SYSTEM_FAIL(1)|	푸쉬 알림 시스템 서비스 요청 실패|	기반이 되는 OS나 외부 플랫폼의 서비스 요청(토큰 요청 등)이 실패한 것이다. OS와 플랫폼 라이브러리 버전, 네트워크 상태 등을 체크한 후 재시도해야 한다.|
|ERROR_NETWORK_FAIL(2)|	네트워크 송수신 실패|	토스트 클라우드 서버에 연결하거나, 데이터 송수신 시 에러가 발생한 것으로, 서버와 기기의 네트워크 상태를 체크한 후 재시도할 것.|
|ERROR_SERVER_FAIL(3)|	서버 응답 실패|	서버에서 정상적으로 응답 데이터를 보내줬으나 응답의 결과값이 실패인 경우로서, 요청 시의 데이터나 외부 플랫폼 설정 키 값이 정확한지 체크한 후 수정하여 재시도할 것.|
|ERROR_ALREADY_IN_PROGRESS(4)|	이전 요청 처리 중|	이미 요청한 내용을 실행 중인 상태로, 응답 콜백이 불린 후 재시도할 것.|
|ERROR_INVALID_PARAMETERS(5)|	인자 오류|	요청 인자에 잘못된 값이 있는 경우로, 인자에 누락된 키나 틀린 값이 없는지 체크한 후 수정하여 재시도할 것.|
|ERROR_PERMISSION_REQUIRED(6)|	인자 오류|	요청 인자에 잘못된 값이 있는 경우로, 인자에 누락된 키나 틀린 값이 없는지 체크한 후 수정하여 재시도할 것.|

<br/>
<br/>
<br/>

* *문서 수정 내역*
    * *(2017.07.20) 국가 코드, 언어 코드에 대한 제약 추가*
    * *(2017.05.25) 수신 및 오픈 API 수정에 따른 가이드 수정*
    * *(2017.04.20) 수신 및 오픈 여부 적용 가이드 신규 작성*
    * *(2017.04.20) 텐센트 SDK 버전 업데이트 및 가이드 수정(2.47 -> 3.0)*
    * *(2017.02.23) 텐센트 SDK 버전 업데이트 (2.39 -> 2.47)*
    * *(2017.02.23) 텐센트 AndroidManifest.xml 일부 권한 추가*
