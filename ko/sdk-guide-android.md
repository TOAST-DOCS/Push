## Notification > Push > Android SDK 가이드
Push SDK를 적용하면 모바일 애플리케이션과 Push를 쉽게 연동할 수 있습니다.

## 주요 기능
* OS에 알림 토큰 등록
* 알림 메시지 수신 및 표시
* 메시지 수신 및 수신된 메시지를 통한 애플리케이션 실행 지표 수집

## 다운로드
[TOAST Document](http://docs.toast.com/ko/Download/)에서 **Notification > Push** 아래의 **Android SDK (AAR)**을 클릭해 파일을 다운로드합니다.

## 지원 환경
#### 버전
* API 레벨 15(4.0.3) 이상

#### 지원 플랫폼
* Google Cloud Messaging(이하 GCM)
* Tencent Mobile Push(이하 Tencent)
* Amazon Device Messaging(이하 ADM)

## 공통 프로젝트 설정
* SDK(AAR) 다운로드 및 추가
    * 프로젝트 폴더 하위에 libs 폴더가 없으면 생성합니다.
    * 다운로드한 AAR 파일을 프로젝트의 libs 폴더에 추가합니다.
* build.gradle에 SDK 추가
    * dependencies에 다음과 같이 추가합니다.
```
dependencies {
    compile fileTree(dir: 'libs', include: ['*.aar'])
    compile 'com.android.support:appcompat-v7:26.1.0'
    compile 'com.android.support:support-v4:26.1.0'
}
```

## GCM 설정
### 프로젝트 설정
* build.gradle에 GCM SDK 추가
    * dependencies에 다음과 같이 추가합니다.
```groovy
dependencies {
    compile 'com.google.android.gms:play-services-gcm:11.0.0'
}
```

### AndroidManifest.xml 수정
* 아래에 '[YOUR_PACKAGE_NAME]'으로 되어 있는 모든 부분을 애플리케이션 기본 페키지 네임으로 변경합니다.

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android" package="[YOUR_PACKAGE_NAME]">
<application android:icon="@drawable/app_icon">
        <receiver android:name="com.google.android.gms.gcm.GcmReceiver" android:exported="true"
                android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="[YOUR_PACKAGE_NAME]" />
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
<permission android:name="[YOUR_PACKAGE_NAME].permission.C2D_MESSAGE" android:protectionLevel="signature"/>
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
<uses-permission android:name="[YOUR_PACKAGE_NAME].permission.C2D_MESSAGE" />
</manifest>
```

## Tencent 설정
### 프로젝트 설정
가이드는 Tencent SDK 3.2.3을 기준으로 작성되었습니다.

* Tencent SDK 다운로드 페이지인 [腾讯移动推送 | 信鸽](http://xg.qq.com/xg/ctr_index/download)에서 Tencent SDK를 다운로드합니다.
* 다운로드한 SDK의 압축을 해제하고 아래 파일을 프로젝트 하위의 libs 폴더에 추가합니다.
    * 필수
        * libs/jg_filter_sdk_1.1.jar
        * libs/mid-core-sdk-4.0.6.jar
        * libs/wup-1.0.0.E-SNAPSHOT.jar
        * libs/Xg_sdk_v3.2.3_20180403_1839.jar
        * libs/armeabi 폴더 전체
    * 선택 : 다른 아키텍처 사용을 원하는 경우
        * Other-Platform-SO/{아키텍처 이름의 폴더}
* build.gradle 수정
```groovy
android {
    sourceSets {
        main {
            jniLibs.srcDirs = ['libs']
        }
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
}
```

### AndroidManifest.xml 수정
* 아래에 '[YOUR_PACKAGE_NAME]'으로 되어 있는 모든 부분을 애플리케이션 기본 페키지 네임으로 변경합니다.

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android" package="[YOUR_PACKAGE_NAME]">
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
    <service android:name="com.tencent.android.tpush.rpc.XGRemoteService" android:exported="true" >
        <intent-filter>
            <action android:name="[YOUR_PACKAGE_NAME].PUSH_ACTION" />
        </intent-filter>
    </service>
    <provider
    android:name="com.tencent.android.tpush.XGPushProvider"
    android:authorities="[YOUR_PACKAGE_NAME].AUTH_XGPUSH"
    android:exported="true"/>
    <provider
        android:name="com.tencent.android.tpush.SettingsContentProvider"
        android:authorities="[YOUR_PACKAGE_NAME].TPUSH_PROVIDER"
        android:exported="false" />
    <provider
        android:name="com.tencent.mid.api.MidProvider"
        android:authorities="[YOUR_PACKAGE_NAME].TENCENT.MID.V3"
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

## ADM 설정
### 프로젝트 설정
* Amazon Device Messaging(이하 ADM)은 Fire OS 2세대 이상의 기기에서 사용할 수 있습니다.
* [Amazon Developer SDKs 다운로드 페이지](https://developer.amazon.com/sdk-download)에서 Amazon Device Messaging SDK를 다운로드합니다.
* 다운로드한 SDK의 압축을 해제하고 amazon-device-messaging-*.jar 파일을 프로젝트 하위의 libs 폴더에 추가합니다.
* build.gradle을 수정합니다.
```groovy
dependencies {
    compileOnly files('libs/amazon-device-messaging-1.0.1.jar')
}
```

### AndroidManifest.xml 수정
* 아래에 '[YOUR_PACKAGE_NAME]'으로 되어 있는 모든 부분을 애플리케이션 기본 페키지 네임으로 변경합니다.

#### Namespace 추가
```xml
<manifest xmlns:amazon="http://schemas.amazon.com/apk/res/android">
```

#### 권한 추가
```xml
<permission
    android:name="[YOUR_PACKAGE_NAME].permission.RECEIVE_ADM_MESSAGE"
    android:protectionLevel="signature" />
<uses-permission android:name="[YOUR_PACKAGE_NAME].permission.RECEIVE_ADM_MESSAGE" />
<uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
```

#### Handler 및 Receiver 추가
- [YOUR_HANDLER_CLASS]에는 사용자가 작성한 Handler의 클래스를 입력합니다.
- [YOUR_RECEIVER_CLASS]에는 사용자가 작성한 Receiver의 클래스를 입력합니다.
    - Handler 및 Receiver 구현은 아래를 참고합니다.
```xml
<amazon:enable-feature android:name="com.amazon.device.messaging" android:required="true"/>
<service
    android:name="[YOUR_HANDLER_CLASS]"
    android:exported="false" />

<receiver
    android:name="[YOUR_RECEIVER_CLASS]"
    android:permission="com.amazon.device.messaging.permission.SEND" >
    <intent-filter>
        <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
        <action android:name="com.amazon.device.messaging.intent.RECEIVE" />

        <category android:name="[YOUR_PACKAGE_NAME]" />
    </intent-filter>
</receiver>
```

### Handler 및 Receiver 구현
- 알림에 제목과 본문만 필요할 경우, 기본 Handler와 Receiver를 사용할 수 있습니다.
    - 기본 Handler : com.toast.android.pushsdk.listener.DefaultPushSdkADMHandler
    - 기본 Receiver : com.toast.android.pushsdk.listener.DefaultPushSdkADMReceiver
- 사용자 Handler는 com.toast.android.pushsdk.listener.AbstractPushSdkADMHandler 클래스를 상속해야 합니다.
```java
public class CustomADMHandler extends AbstractPushSdkADMHandler {
    public CustomADMHandler() {
        super(CustomADMHandler.class);
    }

    @Override
    protected void onMessage(Intent intent) {
        Bundle extras = intent.getExtras();
        String value = extras.getString("key");
        // 수신한 데이터를 이용해서 알림 표시
    }
}
```
- 사용자 Receiver는 com.amazon.device.messaging.ADMMessageReceiver 클래스를 상속해야 합니다.
```java
public class CustomADMReceiver extends ADMMessageReceiver {
    public CustomADMReceiver() {
        super(CustomADMHandler.class); // 반드시 사용자 Handler의 클래스를 입력해야 합니다.
    }
}
```

## PushParams
### PushParams란?
* PushParams는 토큰 등록 및 조회를 위해서 필요한 객체입니다.
* PushParams.Builder 클래스를 통해서 객체를 생성할 수 있습니다.
* PushParams에 포함된 정보는 아래와 같습니다.

| 프로퍼티                | 설명                                 | 필수 여부 | 기본값           |
| ----------------------- | ------------------------------------ | --------- | ---------------- |
| appKey                  | Push 서비스 키                       | 필수      | 없음             |
| userId                  | 사용자 식별자                        | 필수      | 없음             |
| context                 | 컨텍스트                             | 필수      | 없음             |
| pushType                | 푸시 유형(GCM, Tencent)              | 필수      | 없음             |
| channel                 | 채널                                 | 선택      | default          |
| country                 | 국가 코드                            | 선택      | 시스템 국가 코드 |
| language                | 언어 코드                            | 선택      | 시스템 언어 코드 |
| isNotificationAgreement | 알림 표시 동의 여부                  | 선택      | false            |
| isAdAgreement           | 광고성 정보 알림 표시 동의 여부      | 선택      | false            |
| isNightAdAgreement      | 야간 광고성 정보 알림 표시 동의 여부 | 선택      | false            |

#### PushParams 생성
* PushParams는 토큰 등록 및 조회를 위해서 필요한 객체입니다.
* PushParams.Builder 클래스를 통해서 객체를 생성할 수 있습니다.
* 예제 코드
```java
PushType pushType = null;
if (isGCM) {
    pushType = PushType.gcm("[YOUR_SENDER_ID]");
} else if (isTencent) {
    long yourAccessId = 1234567890L; // [YOUR_ACCESS_ID]
    pushType = PushType.tencent(yourAccessId, "[YOUR_ACCESS_KEY]");
} else if (isADM) {
    pushType = PushType.adm();
}

PushParams.Builder builder = new PushParams.Builder(this, "[YOUR_APP_KEY]", "[YOUR_USER_ID]", pushType);

builder.setChannel("default"); // 선택값
builder.setNotificationAgreement(true); // 선택값
builder.setAdAgreement(true); // 선택값
builder.setNightAdAgreement(true); // 선택값
builder.setCountry("KR"); // 선택값
builder.setLanguage("ko"); // 선택값

PushParams pushParams = builder.build();
```

## 토큰 등록
* 푸시 타입에 따라 토큰을 생성해서 서버에 토큰을 등록합니다.
* 예제 코드
```java
PushSdk.register(pushParams, new PushRegisterCallback() {
    @Override
    public void onRegister(PushRegisterResult result) {
        if (result.isSuccessful()) {
            // 토큰 등록 성공
        } else {
            // 토큰 등록 실패
            Log.e(TAG, "error,code=" + result.getCode() + ",message=" + result.getMessage());
        }
    }
});
```

> **Tencent를 사용하는 경우 예외 사항**
>
> Tencent는 WRITE_SETTINGS 권한이 필요하며, API 레벨 23(6.0)에서는 별도의 대화 상자가 나타납니다.
> 설정 대화 상자에서 권한을 허용하더라도, 콜백으로 ERROR_PERMISSION_REQUIRED 오류가 반환됩니다.
> 이 경우, 다시 토큰 등록을 호출하면 정상적으로 토큰이 등록됩니다.

## 토큰 정보 조회
* 현재 서버에 저장된 토큰 정보가 PushQueryResult 객체에 담겨 콜백으로 반환됩니다.
* 예제 코드
```java
PushSdk.query(pushParams, new PushQueryCallback() {
    @Override
    public void onQuery(PushQueryResult result) {
        if (result.isSuccessful()) {
            // 토큰 정보 조회 성공
            TokenInfo tokenInfo = result.getTokenInfo();
        } else {
            // 토큰 정보 조회 실패
            Log.e(TAG, "error,code=" + result.getCode() + ",message=" + result.getMessage());
        }
    }
});
```

## 지표 수집
### 수신(Received) 지표
* SDK에서 제공하는 기본 리시버를 사용하는 경우, 수신 지표가 자동으로 수집됩니다.
* 사용자가 직접 리시버를 구현하는 경우, 수신 지표 수집을 위해서 아래 메서드를 리시버에 추가해야 합니다.
* 예제 코드
```java
public static class CustomPushReceiver extends GcmListenerService {
    @Override
    public void onMessageReceived(String from, Bundle data) {
        PushAnalytics.onReceived(this, data);
        // 알림 등록 로직 수행
    }
}
```

### 실행(Opened) 지표
* 알림 영역의 알림을 통해서 실행했을 경우를 실행 지표라고 합니다.
* 실행 지표 수집을 위해서는 액티비티와 푸시 리시버를 수정해야 합니다.
* MainActivity 혹은 알림 클릭 시 실행되는 액티비티에 다음과 같은 코드를 추가해야 합니다.
```java
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        PushAnalytics.onOpened(this, getIntent());
    }

    @Override
    protected void onNewIntent(Intent intent) {
        PushAnalytics.onOpened(this, intent);
    }
}
```
* 푸시 리시버에 다음과 같은 코드를 추가해야 합니다.
    * 이 코드는 SDK에서 제공하는 기본 리시버를 사용하는 경우 추가할 필요가 없습니다.
```java
public static class CustomPushReceiver extends GcmListenerService {
    @Override
    public void onMessageReceived(String from, Bundle data) {
        Intent launchIntent = new Intent(context, MainActivity.class);
        Intent intent = PushAnalytics.newIntentForOpenedEvent(launchIntent, bundle);

        // 혹은 Intent intent = PushAnalytics.newIntentForOpenedEvent(context, MainActivity.class, bundle);
    }
}
```

## 디버그 로그 활성화
* Push SDK는 SDK의 디버그 로그를 활성화하는 메서드를 제공합니다.
* <span style="color:#f47141">반드시 개발 중에만 디버그 로그를 활성화해야 합니다. 릴리스할 때는 제거하거나 false로 설정해야 합니다.</span>
```java
PushSdk.setDebug(true);
```

## 오류 코드
* 오류 코드는 com.toast.android.pushsdk.annotations.PushResultCode 어노테이션에 @IntDef 로 정의되어있습니다.

| 오류 코드                      | 설명                      |
| ------------------------- | ----------------------- |
| ERROR_SYSTEM_FAIL         | 시스템 문제로 토큰 획득에 실패한 경우   |
| ERROR_NETWORK_FAIL        | 네트워크 문제로 요청에 실패한 경우     |
| ERROR_SERVER_FAIL         | 서버에서 실패 응답을 반환한 경우      |
| ERROR_ALREADY_IN_PROGRESS | 토큰 등록/조회가 이미 실행 중인 경우   |
| ERROR_INVALID_PARAMETERS  | 파라미터가 잘못된 경우            |
| ERROR_PERMISSION_REQUIRED | 권한이 필요한 경우(Tencent만 해당) |
| ERROR_PARSE_JSON_FAIL     | 서버 응답을 파싱하지 못한 경우       |