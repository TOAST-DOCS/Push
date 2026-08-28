<!-- machine_translated: true -->

<!-- pre-align:aligned sig=4b8f8603ee06 -->

<a id="section-1"></a>
## Notification> Push > Release Notes { #section-1 }

<a id="section-1-1"></a>
### June 25, 2024 { #section-1-1 }
<a id="section-1-1-1"></a>
#### [Console, API]
##### Feature Updates
* Changed the maximum available period for scheduled delivery
    * Changed the maximum available date for scheduled delivery to be up to 60 days from now 
    * The change applies to the console and all versions of the APIs.

<a id="section-1-2"></a>
### February 27, 2024 { #section-1-2 }
<a id="section-1-2-1"></a>
#### [Console]
##### Added Features
* Added FCM Service Account Credential Authentication
    * On June 20, 2024, the FCM Legacy API will be terminated. As a result, you must use the FCM HTTP (V1) API to send FCM messages, and API authentication requires **Service Account Credential**instead of a **Server Key**.
        * <a href="https://firebase.google.com/docs/cloud-messaging/migrate-v1" target="_blank">Go to the FCM Migration Guide</a>
        * Go to <a href="https://docs.nhncloud.com/ko/Notification/Push/ko/console-guide/#_1">Console Guide</a>
    * After you enroll for **Service Account Credential**, FCM messages are sent via the FCM HTTP V1 API. To continue sending with FCM after June 20, 2024, you must register **Service Account Credential**in the console.

<a id="section-1-3"></a>
### October 31, 2023. { #section-1-3 }
<a id="section-1-3-1"></a>
#### [Console]
##### Feature Updates
* Added a SecretKey when setting up the Logging feature
    * Starting October 31, 2023, when activating the Logging feature, you must add SecretKey of the Log&Crash Search service.
    * If you are already using the feature before October 31, 2023, SecretKey input is not required as transition is scheduled.

<a id="section-1-4"></a>
### March 14, 2023 { #section-1-4 }
<a id="section-1-4-1"></a>
#### [API]
##### Added Features
* Added the Query Token List API
    * Added API to query token lists (v2.4).

<a id="section-1-5"></a>
### December 13, 2022 { #section-1-5 }
<a id="section-1-5-1"></a>
#### [API]
##### Added Features
* Added a paging feature when viewing general logs
  * Added pageNumber to the field list.
##### Updates
* Changed the maximum limit from 1000 to 100 when viewing failed messages

<a id="section-1-6"></a>
### May 10, 2022 { #section-1-6 }
<a id="section-1-6-1"></a>
#### [API]
##### Bug Fixes
* Fixed an issue where an error occurred if there was no `X-SECRET-KEY` header when calling v2.2 API
    * Fixed the issue so that API authentication can be done with `X-User-Access-Key-ID` and `X-Secret-Access-Key` headers.

<a id="section-1-7"></a>
### March 29, 2022 { #section-1-7 }
<a id="section-1-7-1"></a>
#### [Console]
##### Added Features
* Added a feature to provide a compressed file after splitting the file if the number of tokens exceeds 1 million when using the token file download
    * When downloading stored tokens as a file using the **Token File Download** feature in the **Token** tab, a feature to provide a compressed file after splitting the file if the number of tokens exceeds 1 million has been added.

<a id="section-1-8"></a>
### February 15, 2022 { #section-1-8 }
<a id="section-1-8-1"></a>
#### [Console]
##### Added Features
* Added a token file download feature
    * Added a feature to download stored tokens as a file using the **Token File Download** feature in the **Token** tab.
##### Bug Fixes
* Fixed an error where a UID was saved as 'UNKNOWN' while saving the delivery history
    * Fixed an error where a UID was saved as 'UNKNOWN' in the expired token history when using the **Logging** feature in the **Setting** tab.
* Fixed an error where duplicate authentication failure notification emails were sent
    * Fixed an error where, when authentication failed when sending a push message, duplicate notification emails were sent

<a id="section-1-9"></a>
### January 11, 2022 { #section-1-9 }
<a id="section-1-9-1"></a>
#### [API]
##### Added Features
* Added a receipt/confirmation feature to the Amazon Device Messaging (ADM) push type
    * Added a feature that enables receipt/confirmation when sending ADM.
##### Bug Fixes
* Fixed an error where a failure to send an iOS message with FCM was handled as a success
    * Fixed an error where, when sending a message after setting an incorrect APNS certificate to Firebase, it was handled as a success.

<a id="section-1-10"></a>
### October 26, 2021 { #section-1-10 }
<a id="section-1-10-1"></a>
#### [Console]
##### Added Features
* Added a pop-up for modifying token date and time
    * Added a pop-up that allows you to modify the date and time of the registered token.
    * It can be used to change the consent date and time of the token in order to test features such as reserving the advertisement opt-in notification message.

<a id="section-1-10-2"></a>
#### [API]
##### Added Features
* Added a cause of failure to the 'extra2' field of the statistics query API delivery failure event.
* Added a query condition to v2.4 scheduled message query API
    * Added 'deliveryFrom' and 'deliveryTo' conditions that let you query messages based on the scheduled delivery date and time.
    * Scheduled messages with schedules that fall between 'deliveryFrom' and 'deliveryTo' are retrieved.
##### Bug Fixes
* Fixed a query condition processing error in v2.4 scheduled message query API
    * Fixed an error where the 'from' and 'to' query conditions were not processed in the v2.4 scheduled message query API.

<a id="section-1-11"></a>
### July 27, 2021 { #section-1-11 }
<a id="section-1-12"></a>
### [Console] { #section-1-12 }
<a id="section-1-12-1"></a>
#### Added Features
* Added the feature of reserving a guide message for the ad opt-in acceptance
    * Added a feature of sending a guide message to tokens that have reached two years since their last acceptance of ad opt-in. 
    * Every month at a specific time set by the user, a guide message will be sent to the target tokens.
    * The guide message must contain the information about the user's opt-in acceptance and the time of opt-in and how to set ad opt-in.
    * If you place the temporary replacer for opting in to receive advertisement messages (###AD_AGREEMENT_DATE_TIME###) in the body, when sending a message, its time will be replaced with the opt-in acceptance time of the token.
    * This can be set in **Reserve Message for Acceptance of Ad Opt-in** under the **Settings** tab.

<a id="section-1-13"></a>
### December 29, 2020 { #section-1-13 }
<a id="section-1-14"></a>
### [API] { #section-1-14 }
* Added v2.4 Statistics Total API
     * Added a Total API to sum up the retrieved statistical data.
        <a href="https://docs.toast.com/en/Notification/Push/ko/api-guide/#stats-total-api" target="_blank">Go to</a>

<a id="section-1-15"></a>
### June 9, 2020 { #section-1-15 }
<a id="section-1-16"></a>
### [Console] { #section-1-16 }
<a id="section-1-16-1"></a>
#### Added Features 
* Added APNS JWT Authentication
    * Added JWT as method of authentication for sending APNS push messages. You can register Key ID, Team ID, Topic, or Encryption Key required to authenticate JWT on the **Certificate** tab of console.
    * With the registration of APNS JWT certificate information, registered certificate is deleted. 
    * <a href="https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/establishing_a_token-based_connection_to_apns" target="_blank">Go to Apple Developer Guide</a>

<a id="section-1-17"></a>
### [Doc] { #section-1-17 }
<a id="section-1-17-1"></a>
#### Added Guide
* Added a guide for **Getting Authentication Information for APNS JWT**
    * <a href="https://docs.toast.com/ko/Notification/Push/ko/console-guide/#get-apns-jwt" target="_blank">Direct link</a>


<a id="section-1-18"></a>
### March 24, 2020 { #section-1-18 }
<a id="section-1-19"></a>
### [Console] { #section-1-19 }
<a id="section-1-19-1"></a>
#### Added Features
* Updated Statistics
    * Added the **Statistics Event Key Management** tab. You can add a new statistics event key on console and set it up for message delivery. With messages sent, statistical data are collected as of configured statistics event key, and then you can search from the new statistics tab. 
        * <a href="https://docs.toast.com/en/Notification/Push/ko/console-guide/#stats-event-key" target="_blank">Direct Link</a>

<a id="section-1-20"></a>
### [API] { #section-1-20 }
* Added v2.4 API
    * Added a statistics API to query with statistics event key. Statistics APIs of v2.3 are no longer provided. 
        * <a href="https://docs.toast.com/en/Notification/Push/ko/api-guide/#stats-api" target="_blank">Direct Link</a>
* Added Multi-tenant Tokens 
   * Added the multi-tenant feature allowing a token to be shared by many UIDs. You may attach '#tenant=Tenant_Information' at the end of a token for a token registration. Even if many UIDs share a same token, the token can be maintained if it has different tenant information.  

<a id="section-1-21"></a>
### January 21, 2020 { #section-1-21 }
<a id="section-1-21-1"></a>
#### [Doc]
##### Added Guide
* Added a guide for **Why Message Reception Data Metrics Are Low**
    * <a href="https://docs.toast.com/en/Notification/Push/ko/console-guide/#low-received-event-rates" target="_blank">Direct link</a>

<a id="section-1-22"></a>
### December 24, 2019 { #section-1-22 }
<a id="section-1-22-1"></a>
#### [Console]
##### Added Features
* Added HTML style, message click action, and batch input fields to the message sending page
    * When you use **HTML Style**, you can use HTML in the title and content on Android devices. iOS devices are not supported, and HTML will not be displayed. If you do not use **HTML Style**, the HTML code will be displayed as-is on Android and iOS.
    * You can use **Message Click Action** to navigate to a scheme or URL defined in the app.

<a id="section-1-23"></a>
### October 29, 2019 { #section-1-23 }
<a id="section-1-23-1"></a>
#### [API]
##### Added Features 
* Added Badge Attribute for Android  
    * The badge attribute can be delivered to Android, as well as iOS. 
    With TOAST SDK, the badge delivered onto app icon is automatically displayed. 
* Display Messages excluding HTML for iOS
    * Currently, iOS does not show HTML within push messages, unlike Android. 
    By setting 'True' for 'content.default.style.useHtmlStyle', HTML can be removed from messages before delivered for iOS. 
* Updated Rich Messages to Separate Media for Android and iOS
    * Added 'richMessage.androidMedia' and 'richMessage.iosMedia', other than 'richMessage.media. 
    Rich message has been updated to enable separate media setting for Android and iOS.  
* Changed the 'sourceType' and 'extension' to be Optional for Rich Message Media 
    * 'richMessage.media.sourceType' and 'richMessage.media.extension' have been changed to be optional, not required. 
    No setting is required for media extension, be it external or internal, to deliver rich messages.  
* Action Definition Enabled at Click of Push Messages 
    * Actions (e.g. URL or Scheme) to be executed by the click of a push message can be defined at 'content.default.clickAction'. 
    With TOAST SDK, action is executed automatically.  

<a id="section-1-24"></a>
### September 24, 2019 { #section-1-24 }
<a id="section-1-24-1"></a>
#### [API]
##### Bug Fixes 
* Fixed delivery error of iOS rich messages 
    * Fixed error in which image is not properly displayed on iOS if a rich message is delivered while Receive/Confirm Messages is not enabled.  


<a id="section-1-24-2"></a>
#### [Console]
##### Added Features 
* Querying Token List from Token Tab 
    * Updated to allow query of tokens from token tab without search conditions. 
* Sending Messages to iOS via FCM 
    * Messages can be sent to an iOS app which applies FCM SDK. 
        *  <a href="https://firebase.google.com/docs/cloud-messaging/http-server-ref" target="_blank">Go to FCM Guide</a>
    * By using attributes such as 'notification', 'content_available', or 'mutual_content', messages can be sent to iOS apps via FCM. 

<a id="section-1-25"></a>
### May 28, 2019 { #section-1-25 }
<a id="section-1-25-1"></a>
#### [API]
* Improved Receive/Confirm Message data collection performance
    * We have improved message receiving/confirmation data collection performance.

<a id="section-1-26"></a>
### March 26, 2019 { #section-1-26 }
<a id="section-1-26-1"></a>
#### [API]
##### Bug Fixes
* Fixed an error where the from (to, to) setting does not apply in the invalid token lookup API
    * Invalid token lookup API, there was an error that ignores the settings unless both from and to are set.
    * Fixed to apply period setting even if only one of from and to is set.

<a id="section-1-26-2"></a>
#### [Console]
##### Added Features
* Added duplicate message prevention function
    * Even if the exact same message is sent several times, it will not be sent for the set time.
    * Unsent messages will fail. The reason for the dispatch failure is "DUPLICATED_MESSAGE_TOKEN".
    * Duplicate criterion is message type, content (content), outgoing contact, reception agreement setting guide, advertisement display position, token.
    * Settings tab "Duplicate message prevention settings" can be set.

<a id="section-1-27"></a>
### February 26, 2019 { #section-1-27 }
<a id="section-1-27-1"></a>
#### [API]
##### Added Features
* Added v2.3 API
    * Added Token Delete API. Can be called without Secret Key.
    * Added new push type 'FCM'. You must use 'FCM' instead of 'GCM' when making API calls.

<a id="section-1-27-2"></a>
#### [Console]
##### Bug Fixes
Fix broken, typo, link errors
    * Certificates tab Corrected errors and typo in some tooltips.
    * Fixed setting tab typo.
    * Fixed incorrect SDK guide link.

##### Added Features
* User console added.

<a id="section-1-28"></a>
### December 18, 2018 { #section-1-28 }
<a id="section-1-28-1"></a>
#### [API]
##### Bug Fixes
* Fixed an error that invalid VoIP token was not deleted normally.
    * Fixed an error that prevents APNS_VOIP, APNS_SANDBOXVOIP token from being deleted when sending a message.

<a id="section-1-29"></a>
### October 30, 2018 { #section-1-29 }
<a id="section-1-29-1"></a>
#### [Console]
##### Added Features
* Rich message feature added to message sending page
    * You can send a rich message from the Send Message page.
        * <a href="https://docs.toast.com/en/Notification/Push/ko/console-guide/#_3" target="_blank"> Go to Console Guide  </a>
    * Provide preview functionality to see how rich messages are displayed on Android and iOS.
* Added the ability to set the position of the advertisement marker
    * Added the ability to set whether to display the text that indicates that it is an advertising message in the title or content part.
    * You can set it in the setting tab "Ad display position setting".

##### Bug Fixes
* Fixed an error where token lookups are displayed in UTC
    * There was an error displaying the time in UTC when searching for tokens. Corrected to display in your browser's local time.


<a id="section-1-29-2"></a>
#### [API]
##### Added Features
* Rich message feature added to message dispatch API
    * Added the ability to display buttons, media (images, movies, sounds) in push messages.
         * <a href="https://docs.toast.com/en/Notification/Push/ko/api-guide/#7" target="_blank">Go to API Guide </a>
    * Available in v2.0 message delivery APIs and in apps with the latest SDKs.

<a id="section-1-29-3"></a>
#### [SDK]
##### Android
* Added rich message function
    * Rich messages such as buttons, images, large icons, groups can be transmitted.
* Added API for reply function of rich message
    * Listener class registration API has been added to handle reply button.
* Android 9 compatible
    * Fixed bug where receive / open metrics are not collected on Android 9 devices when target version is 28 (Android 9) or higher.

##### iOS
* Added rich message function
    * Rich messages such as buttons, images, and movies can be transmitted.
* Added category setting function
    * If you set the category in the initialization and set it as the category identifier of your own in the message, you can receive the corresponding category action.
* Added indicator collection methodology
    * It is possible to collect verification indices without initialization by inputting the indicator collection information (AppKey) in the application's info.plist file.
    * It is possible to automatically transmit the reception indices by inputting the four index acquisition information (AppKey) of the info.plist file of the user Notification Service Extension. (TCPushServiceExtension extension required)
* Improved token registration
    * Only the system token is registered when the token registration request is made without initialization, and the issued token can be freely registered through the API from the service server.

##### Bug Fixes
* Error that data is missing from 1 second to 59 seconds when querying from list query API to minutes
    * As an example, if you look up data by 10:11, there is an error that the data of 11 minutes 59 seconds is missing.
    In this case, we improved to include 59 seconds.

<a id="section-1-30"></a>
### August 28, 2018 { #section-1-30 }
<a id="section-1-30-1"></a>
#### [API]
##### Added Features
* Added Logging API
    * Added API to inquire saved data with Logging function that can be activated in Console.
    * Provides two types of APIs: general query, bulk query.
         * <a href="https://docs.toast.com/en/Notification/Push/ko/api-guide/#_18" target="_blank"> Go to Log view </a>
* v2.2 API Update
    * Updated Logging API to update the latest API version to v2.2.
    * As of v2.2, API security setting is used for API authentication.
         * <a href="https://toast.com/account/api_settings" target="_blank"> Go to API Security Settings </a>
    * Supported API versions: v1.3, v2.0, v2.1, v2.2

##### Bug Fixes
* Errors that the APNS_VOIP token is deleted when the app type is set to 'Single Token' in the token setting
    * The APNS_VOIP token is a token for VoIP, so it must be managed separately from the GCM, APNS, etc. for push messages,
    When set to a single token, there was an error that APNS_VOIP was managed the same as other tokens and the APNS_VOIP token was deleted.
    * Modified so that the APNS_VOIP tokens and the GCM, APNS, and TENCENT tokens are managed separately.
* Improved error in statistics API timeout in some projects
    * There was a timeout error in some projects. Fixed timeout not to occur through optimization.

<a id="section-1-31"></a>
### July 24, 2018 { #section-1-31 }
<a id="section-1-31-1"></a>
#### [API]
##### Updates
* Improved response message
    * Improved to better understand the cause of failure in header.resultMessage of Response Body by adding more details.

<a id="section-1-31-2"></a>
#### [SDK]
##### Android
* Amazon Device Messaging support

##### iOS
* VoIP type support
* Some API changes due to VoIP type addition

<br>

<a id="section-1-32"></a>
### June 26, 2018 { #section-1-32 }
<a id="section-1-32-1"></a>
#### [Console]
##### Added Features
* Add Amazon Device Messaging (ADM) push type
    * Added ADM push type to send push messages to Amazon device (Kindle Fire).
    * You can register your app on the Amazon developer site, get a Client ID, Client Secret, and register it.
     <a href="https://docs.toast.com/en/Notification/Push/ko/console-guide/#adm-client-id-client-secret" target="_blank"> ADM Guide Shortcut </ a>


<a id="section-1-32-2"></a>
#### [API]
##### Added Features
* Add Amazon Device Messaging (ADM) push type

##### Bug fixes
* Fixed an error that caused some targets to be missing when sending a promotional push message
    * Fixed on May 30, 2018 as a hotfix.
    * Fixed an error where some destinations were missing when sending a push message with a shipping logic error.
* Fixed an error that duplicate reception when using local time function when sending reservation message
    * Fixed an error sending a reservation message in a non-existent time zone when using the local time feature.

<a id="section-1-32-3"></a>
#### [SDK]
##### Android
* Apply latest Tencent SDK (3.2.3)
* API improvements

##### iOS
* Improvement of indicator collection and transmission function
* Automate message check indicator collection and transmission

<br>

<a id="section-1-33"></a>
### May 29, 2018 { #section-1-33 }
<a id="section-1-33-1"></a>
#### [Console]
##### Updates
* Add message ID
    * Added message ID to the details part of popup when selecting message.

<a id="section-1-33-2"></a>
#### [API]
##### Added Features
* Added v2.1 token lookup API
    * You can check the device ID you collect when you register the token.
    * You can check the date of the most recent registration request for this token.

##### Updates
* Advertising
    * When sending an advertising message with MessageType set to AD, an advertising display text is added to the message title and content in accordance with the Act on Promotion of Information and Communications Network (Articles 50 through 50-8).
    * The position of the advertising display text has been changed as follows.

```
Previous display position, where both "(ad)" and the contact information are displayed in the body
- title: Subject
- body: '(ad)' 'Contact'\n Content\n'Consent withdrawal method'

New display position, where "(ad)" and the contact information are displayed in the title
- title: '(ad)' Subject 'Contact'
- body: Content\n'Consent withdrawal method'
```

##### Bug Fixes
* Fixed an error where the query period was ignored in the receive/confirm statistics API
    * Fixed an error where the query period was ignored when a message ID and query period were entered together.

<a id="section-1-33-3"></a>
#### [SDK]
##### Android
* Improved SDK usability

<br>

<a id="section-1-34"></a>
### May 2, 2018 { #section-1-34 }
<a id="section-1-34-1"></a>
#### [SDK]
##### Android
* Fixed a token registration bug
* Changed minimum supported version (API 9 -> API 15)

##### iOS
* Fixed a token registration bug
* Changed minimum supported version (iOS 7.0 -> iOS 8.0)
* Changed SDK library format (static library -> framework)

<br>

<a id="section-1-35"></a>
### April 24, 2018 { #section-1-35 }
<a id="section-1-35-1"></a>
#### [Console]
##### Added Features
* Added token management settings
    * Token expiration period setting
        * Tokens that have had no registration requests during the configured period are excluded from message delivery targets.
        * You can reduce costs because tokens of users who have not used the app during the configured period can be excluded from message delivery targets.
    * App type setting
        * Manages tokens according to the type of the integrated app.
        * If users of the app can use the app installed on multiple devices simultaneously, you must set it to Multiple. (Default)
      When set to Multiple, a user can have multiple tokens.
      For example, if a user uses both a phone and a tablet, push messages are received on both devices.
        * If users can only use the app on one device at a time, you must set it to Single.
      When set to Single, a user can have only one token.
      For example, if a user uses both a phone and a tablet, push messages are received on only one of the two devices.

##### Updates
* Localized error messages to Korean
    * Localized the error messages displayed when errors occur in the Push Console to Korean.

<a id="section-1-35-2"></a>
#### [API]
##### Added Features
* Added the deviceId field to the v2.0 token registration API
    * Added the deviceId field to distinguish a user's device.
    * When registering a token, if a token with the same deviceId already exists, the existing token is deleted and the new one is registered.
    * We recommend setting IDFV (identifierForVendor) for iOS and Android ID for Android.
    * The SDK with the device ID collection feature is scheduled to be released on May 2.

<a id="section-1-35-3"></a>
#### [ETC]
##### Bug Fixes
* [Mail] HTML error in certificate expiration notification email
    * Fixed an error where the background color of the lower area was not displayed due to incorrect HTML in the certificate expiration notification email.

<br>

<a id="section-1-36"></a>
### March 22, 2018 { #section-1-36 }
<a id="section-1-36-1"></a>
#### [Console]
##### Feature Updates
* Tab menu on service page moved to console
    * Tab menu can be located on console, to move to pages, from the menu on the left or on the top right.
* Sorted tokens by most recent registration when querying UIDs
    * Changed the order of tokens displayed when querying UIDs in the Token tab on the console to sort by most recent registration.

<a id="section-1-36-2"></a>
#### [API]
##### Added Features
* Added Uid API
    * Added APIs for adding/querying/modifying/deleting Tags for UIDs.
    * This API does not require a Secret Key. It can be called from an app.
(Calling an API that requires a Secret Key from an app is not recommended, as the Secret Key may be exposed externally.)

##### Bug Fixes
* Fixed an error that allowed spaces to be entered in tag names
    * Fixed an error in the tag creation API where spaces could be entered in the tagName field.

<br>

<a id="section-1-37"></a>
### February 22, 2018 { #section-1-37 }
<a id="section-1-37-1"></a>
#### [Console]
##### Added Features
* Added iOS VoIP delivery feature
    * Added a feature to send VoIP push messages to iOS.
    * Currently not supported in the SDK; support will be added in a future release.
    * To send VoIP messages, the following steps are required:
        1. Register a VoIP certificate (a VoIP-specific certificate or a Universal certificate can be registered)
        2. Register the VoIP token and handle push message reception (set the token's push type to APNS_VOIP or APNS_SANDBOXVOIP)
        <a href="https://developer.apple.com/library/content/documentation/Performance/Conceptual/EnergyGuide-iOS/OptimizeVoIP.html" target="_blank">Go to Apple iOS PushKit Guide</a>
        3. When sending a message, select the push type 'APNS_VOIP' or 'APNS_SANDBOXVOIP'

##### Feature Updates
* Improved the 'RemoveGuide' description on the message sending page
    * Added an example to the field for entering the opt-out method for advertising push messages when sending advertising messages.
    'Example: Menu > Settings > Notification Settings'

<a id="section-1-37-2"></a>
#### [API]
##### Added Features
* Added iOS VoIP delivery feature
* Added deliveryType to the message query API query conditions
    * The following values can be set for deliveryType:
     'INSTANT', 'RESERVATION'

##### Feature Updates
* Improved deletion of scheduled messages with delivery history
    * Previously, when a scheduled message was deleted, it was removed even if it had already been sent, making it difficult to check the delivery history.
    * Improved so that when attempting to delete a scheduled message with delivery history, the status is changed to 'CANCEL' instead of being deleted.

##### Bug Fixes
* Fixed an error where the response time was too long to retrieve the scheduled message list
    * Fixed an error where, when a large number of scheduled messages were registered, the response time became too long to retrieve the list.
* Fixed an error where the item count was incorrect when querying immediate and scheduled messages
    * Fixed an error where the filtering conditions were not applied to the item count when querying messages, causing incorrect counts.
* Fixed an error where data in negative UTC offset time zones was not collected during message receipt/confirmation data collection
    * Fixed an error where negative UTC offset time zones were not properly handled, causing data to not be collected.
* Fixed an issue where the event field was not applied in the message receipt/confirmation statistics query API
    * Fixed an error where setting a value for the event field did not apply filtering.
    The following values can be set for event:
    'SENT', 'SENT_FAILED', 'RECEIVED', 'OPENED'

<a id="section-1-37-3"></a>
#### [ETC]
##### Feature Updates
* Improved common message delivery
    * Previously, when sending a common message, the language code of the content and the language code of the token had to be exactly the same for the message to be sent in that language code.
    The feature has been improved to measure the similarity of language codes and send messages using the most similar language code.
    For example, if the content's language code is 'zh' and the tokens' language codes are 'zh-Hans' or 'zh-Hans-CN', the message will still be sent as 'zh'.

<br>

<a id="section-1-38"></a>
### December 12, 2017 { #section-1-38 }
<a id="section-1-38-1"></a>
#### [API]
##### Bug Fixes
* Fixed an error where the delivery time was calculated incorrectly during local time scheduled delivery
    * When using local time delivery (isLocalTime = true) for scheduled delivery,
    fixed an error in the delivery time calculation logic for each time zone.

<a id="section-1-38-2"></a>
#### [ETC]
##### Feature Updates
* Updated libraries with security vulnerabilities
    * Updated libraries with discovered security vulnerabilities to patched versions.

<br>

<a id="section-1-39"></a>
### November 23, 2017 { #section-1-39 }
<a id="section-1-39-1"></a>
#### [Console]
##### Added Features
* Added the Logging feature
    * Added a feature to save message delivery history to Log & Crash Search.
    You can activate the feature by registering the Appkey of your Log & Crash Search service in the Logging section of the **Setting** tab.
    * The saved message delivery history can be viewed on the Log & Crash Search page.
    * <a href="/en/Notification/Push/en/console-guide/#_9" target="_blank">Go to Logging Description</a>

##### Bug Fixes
* Fixed an error where pop-ups were hidden behind the product usage guide on low-resolution screens
    * Fixed an error where pop-ups were obscured by the product usage guide on some low-resolution screens.
* Fixed an error with the Edit and Delete buttons in the Reservation tab
    * Fixed an error where the Edit and Delete buttons in the Reservation tab could be clicked even when they were in an unclickable state.

<a id="section-1-39-2"></a>
#### [API]
##### Updates
* Added a limit to the v2.0 failed message query API
    * Previously, querying failed messages returned all results.
    If the result size was large, a response timeout could occur, so the response has been changed to return up to 1,000 results at a time.
    * If there are more than 1,000 results, an abnormal response is returned. In the case of an abnormal response, you must query a shorter period for the from and to parameters.
    * <a href="/en/Notification/Push/en/api-guide/#_15" target="_blank">Go to API Reference</a>
        * Messages > Query > Query Failed Message List

<a id="section-1-39-3"></a>
#### [ETC]
##### Bug Fixes
* [Mail] Fixed an error where an incorrect Appkey was displayed when sending a certificate expiration notification email
    * Fixed an error where, when the Push service was reactivated after a period of non-use, the certificate expiration notification email displayed the old Appkey.

<br>

<a id="section-1-40"></a>
### September 21, 2017 { #section-1-40 }
<a id="section-1-40-1"></a>
#### [Console]
##### Bug Fixes
* Fixed an error where there was no sort order when querying tags
    * Fixed to sort by creation date in descending order when querying tags.
* Fixed an error where more than two days of the week could not be selected when registering a scheduled message
    * Fixed an error where more than two days of the week could not be selected when the schedule type was set to 'EVERY_WEEK'.

<a id="section-1-40-2"></a>
#### [API]
##### Updates
* Updated to disallow spaces in tag names when registering tags

<br>

<a id="section-1-41"></a>
### 2017.08.24 { #section-1-41 }
<a id="section-1-41-1"></a>
#### [Console]
##### Added Features
* Added tag message delivery
    * You can send messages by selecting a tag from the Send Message or Scheduled Message tabs.
    * If you set Type to 'TAG' in Target, you can select from registered tags.
    * You can send messages by querying the selected tags with 'OR' or 'AND' conditions.
    * For example, if you select the 'Seoul', '30s', and 'Male' tags and send a message with the 'AND' condition, the message will be sent to males in their 30s living in Seoul.
* Added Token tab
    * You can search for tokens registered by UID or token from the web console.
    * For UID searches, both exact and partial match searches are available.
    * You can add new tokens or delete found tokens.
* Added Tag tab
    * You can manage tags.
    * You can query UIDs with tags attached.
    * You can attach or remove tags from UIDs.

##### Updates
* Removed channel message delivery feature
    * With the addition of the tag message delivery feature, the channel message delivery feature has been removed from the console.
    * The existing channel message delivery feature is still available via the v1.3 message delivery API.

<a id="section-1-41-2"></a>
#### [API]
##### Updates
* Improved recipient criteria for notification/promotional/night-time promotional push messages
    * In accordance with the Act on Promotion of Information and Communications Network (Articles 50 through 50-8), tokens of users in the Republic of Korea are automatically filtered based on their consent to receive messages.
    * Recently, with various language codes being generated in iOS, there was an issue where tokens might not be classified as tokens for users in the Republic of Korea.
    * Previously, only tokens with language codes 'ko' or 'ko-kr' were classified as tokens for users in the Republic of Korea, but this has been improved to classify tokens with language codes containing 'ko', 'kor', or 'ko-' as tokens for users in the Republic of Korea.

##### Bug Fixes
* Fixed a bug where the scheduled message status could not be updated
    * Fixed an error where, even after scheduled message delivery was completed, the reservationStatus added in the v2.0 reservation API was not updated to COMPLETED.
* Fixed a bug where a token was deleted when the same value was set for the oldToken and token fields during token registration
    * Fixed as a hotfix on August 3, 2017.
    * oldToken is a field used when a token change occurs or when changing a token stored on the server to a new token.
    * Fixed a bug where calling the token registration API with the same value set for oldToken as the token caused the registration to be skipped after deletion.
    * After the patch, if oldToken and token are the same, the token is updated without deletion.

<a id="section-1-41-3"></a>
#### [SDK]
##### Android
* Improved token registration feature
* Improved initialization behavior

##### iOS
* Improved token registration feature

<br>

<a id="section-1-42"></a>
### July 20, 2017 { #section-1-42 }
<a id="section-1-42-1"></a>
#### [API]
##### Added Features
* Added Tag API
    * You can manage UIDs by attaching tags to them.
    * You can add and manage contacts for UIDs.
    * When sending a message, you can send it by setting tags and conditions.
For example, if you set target.type to 'TAG' and target.to to 'Male, AND, 30s' when sending a message, the message will be sent to UIDs with the 'Male' and '30s' tags.
    * This is first released via API, and the tag feature will be available in the CONSOLE after the August regular maintenance.
    <a href="/en/Notification/Push/en/api-guide/#_13" target="_blank">Go to API Reference</a>
* Added a query API for failed messages
    * An API has been added to query messages that failed when sending.
    You can use this API to check the reason for delivery failure.
    <a href="/en/Notification/Push/en/api-guide/#_15" target="_blank">Go to API Reference</a>

##### Bug Fixes
* Fixed an error where an existing token was not deleted when a new token existed during token modification
    * Fixed an error where, when changing oldToken to token in the Token Registration API, oldToken was not deleted if the token already existed.
* Fixed an Internal Error response when querying messages
    * Fixed an issue where entering a DateTime in an incorrect format for from or to when querying messages resulted in an Internal Error response; it now responds with a Client Error.
* Fixed an error where createdDateTime was incorrectly set when modifying a scheduled message
    * Fixed an error where, when modifying a scheduled message, not only updatedDateTime (modification date/time) but also createdDateTime (creation date/time) was updated to the updatedDateTime value.

<br>

<a id="section-1-43"></a>
### May 25, 2017 { #section-1-43 }
<a id="section-1-43-1"></a>
#### [SDK]
##### Android
* Added API for checking the SDK version
* Changed indicator-related APIs

##### iOS
* Added API for checking the SDK version

<br>

<a id="section-1-44"></a>
### April 25, 2017 { #section-1-44 }
<a id="section-1-44-1"></a>
#### [Console]
##### Added Features
* Added Dashboard and Settings tabs
    * Added a [Dashboar]d tab where you can view message receipt and confirmation statistics.
    * Added a [Settings] tab where you can configure the message receipt and confirmation data collection feature.

<a id="section-1-44-2"></a>
#### [API]
##### Added Features
* Added Message Delivery Receipt data collection and statistics query feature
    * Added a feature to collect message receipt and user confirmation data after delivery and view the data as statistics.
    * You can enable this feature in [CONSOLE] > [Settings] tab, and check the statistics query API description in v2.0 API Reference.
    * This feature is only available in apps that use SDK v1.4 or later.    
    <a href="/en/Notification/Push/en/sdk-guide/#_4" target="_blank">Go to SDK Receive and Open Guide</a>
* Added v2.0 API
    * Added a Token Statistics API.
    * Added a Scheduled Message API.
    * Added a Message Receipt and Confirmation Statistics Query API.
    * The v1.3 Feedback API has been changed to the v2.0 Invalid Token API.
    * Response messages are now displayed in greater detail.
    <a href="/en/Notification/Push/en/api-guide" target="_blank">Go to v2.0 API Reference</a>

<br>

<a id="section-1-45"></a>
### February 23, 2017 { #section-1-45 }
<a id="section-1-45-1"></a>
#### [API]
##### Bug Fixes
* Fixed an issue where scheduled messages with a delivery period of more than one month were not sent
    * Fixed an issue where scheduled messages registered through January 2017 with a delivery end date of February or later were not sent.

<a id="section-1-45-2"></a>
#### [SDK]
##### Android
* Removed warning logs during build
* Updated play-service dependency

##### iOS
* Improved stability

<br>

<a id="section-1-46"></a>
### January 19, 2017 { #section-1-46 }
<a id="section-1-46-1"></a>
#### [API]
##### Added Features
* Added the createdDateTime (message creation time) field to the message query API response body

<a id="section-1-46-2"></a>
#### [ETC]
##### Feature Updates
* [Mail] Changed the certificate expiration notification email account (support@cloud.toast.com -> noreply@cloud.toast.com)

<br>

<a id="section-1-47"></a>
### December 22, 2016 { #section-1-47 }
<a id="section-1-47-1"></a>
#### [API]
##### Bug Fixes
* [API] Fixed an issue where scheduled messages were not sent after one month had passed since registration
* [API] Fixed an issue where scheduled messages set to be sent on the 1st of each month were not sent
* [API] Fixed an issue where a new version FCM API Key could not be registered
* [API] Fixed an issue where tokens were not deleted when the delivery result was 'MismatchSenderId' or 'NotRegistered'

<br>

<a id="section-1-48"></a>
### November 24, 2016 { #section-1-48 }
<a id="section-1-48-1"></a>
#### [SDK]
##### Android
* Changed the default channel value
* Updated GCM library to version 9.6.0
* Added more granular error logging
* Bug fixes

##### iOS
* Changed the default channel value

<br>

<a id="section-1-49"></a>
### October 6, 2016 { #section-1-49 }
<a id="section-1-49-1"></a>
#### [API]
##### Feature Updates
* Changed the MPS unit from 1,000/second to 100/second

<br>

<a id="section-1-50"></a>
### September 29, 2016 { #section-1-50 }
<a id="section-1-50-1"></a>
#### [Console]
##### Feature Updates
* Updated to allow certificates to be replaced directly without deleting them first
* Fixed an issue where the APNS Universal Certificate could not be registered in APNS_SANDBOX (Development)

<a id="section-1-50-2"></a>
#### [API]
##### Bug Fixes
* Fixed an issue where APNS_SANDBOX tokens were excluded from the token query API based on UID
* Fixed an issue where an empty string ("") could be registered through the token registration API

<a id="section-1-50-3"></a>
#### [ETC]
##### Policy Changes
* Changed the data retention period policy; data is now stored for up to the last 30 days (messages, scheduled messages, and feedback)

<br>

<a id="section-1-51"></a>
### August 18, 2016 { #section-1-51 }
<a id="section-1-51-1"></a>
#### [Console]
##### Bug Fixes
* Fixed an issue where the day of the week was displayed differently from the saved content when editing a scheduled message