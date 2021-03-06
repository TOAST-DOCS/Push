## Notification > Push > Release Notes

### 2018.07.24
#### 기능 개선
* [API] 응답 메시지 개선
    * Response Body의 header.resultMessage에 실패 원인에대해 더 자세한 내용을 추가해 이해를 돕도록 개선했습니다.

### 2018.06.26
#### 버그 수정
* [API] 광고성 푸시 메시지 발송시 일부 대상이 누락되는 오류 수정
    * 2018년 05월 30일 핫픽스로 수정되었습니다.
    * 발송 로직 오류로 광고성 푸시 메시지 발송시 일부 대상이 누락되는 오류를 수정했습니다.
* [API] 예약 메시지 발송시 현지 시간 기능을 사용할 경우, 중복 수신이 되는 오류 수정
    * 현지 시간 기능을 사용한 경우, 존재하지 않는 시간대로 예약 메시지를 발송하는 오류를 수정했습니다.

#### 기능 개선
* [Android SDK] 지원하는 Tencent SDK 버전 업데이트 (3.2.3)
* [iOS SDK] 지표 수집 및 전송 기능 개선

#### 기능 추가
* [API, Console] ADM(Amazon Device Messaging) 푸시 타입 추가
    * 아마존 디바이스(Kindle Fire)로 푸시 메시지를 발송할 수 있게 ADM 푸시 타입을 추가했습니다.
    * 아마존 개발자 사이트에서 앱을 등록하고 Client ID, Client Secret을 발급받아 등록 후 발송할 수 있습니다.
    <a href="https://docs.toast.com/en/Notification/Push/en/console-guide/#adm-client-id-client-secret" target="_blank">ADM 가이드 바로가기</a>
* [Android SDK] 개선된 API 추가 (기존 API도 호환)
* [iOS SDK] 실행(Opened) 지표 수집 및 전송 자동화


### 2018.05.29
#### 배포
* [Android SDK] v1.4.4 배포
* [iOS SDK] v1.5.0 배포

#### 버그 수정
* [API] 수신/확인 통계 API 조회 기간이 무시되는 오류 수정
    * 메시지 아이디와 조회 기간을 같이 입력할 경우, 조회 기간이 무시되는 오류를 수정했습니다.

#### 기능 개선
* [Console] 메시지 아이디 추가
    * 메시지 선택시 팝업의 Details부분에 메시지 아이디를 추가했습니다.
* [API] 광고성 메시지, 광고 표시 문구 위치 변경
    * MessageType이 AD인 광고성 메시지를 발송하는 경우, 정보통신망법 규정((제50조부터 제50조의 8)에 따라
    메시지 제목과 내용에 광고 표시 문구가 추가되고 있습니다.
    * 광고 표시 문구 위치가 아래와 같이 변경됩니다.

```
기존 표시 위치, '(광고)'와 연락처 모두 body에 표시됨
- title: 제목
- body: '(광고)' '연락처'\n내용\n'수신 동의 철회 방법'

새로운 표시 위치, '(광고)'와 연락처가 title에 표시됨
- title: '(광고)' 제목 '연락처'
- body: 내용\n'수신 동의 철회 방법'
```

* [Android SDK] PushAnalytics.initialize 호출하지 않아도 동작하도록 수정했습니다.
    * PushAnalytics.initialize 는 Deprecated 될 예정입니다.
* [Android SDK] 기본 리시버를 사용할 경우, 안드로이드 8.0 이상에서 Notification Channel을 사용합니다.

#### 기능 추가
* [API] v2.1 토큰 조회 API 추가
    * 토큰 등록시 같이 수집하는 디바이스 아이디를 확인할 수 있습니다.
    * 해당 토큰의 최근 등록 요청 일시를 확인할 수 있습니다.

### 2018.05.02
#### 배포
* [SDK] v1.4.3 배포

#### 버그 수정
* [Android SDK] GCM, Tencent를 동시에 사용할 경우, Tencent 토큰이 GCM 토큰을 덮어쓰는 문제를 해결했습니다.
* [iOS SDK] Background Thread에서 Register 요청 시 Warnning 메시지 뜨던 현상을 제거했습니다
    * Main Thread에서 요청하도록 수정

#### 기능 개선
* [SDK] 서버 API를 v1.3에서 v2.0으로 업데이트했습니다.
* [SDK] 최소 버전을 변경했습니다.
    * [Android SDK] 기존 최소 버전 API level 9(2.3) 에서 API level 15(4.0.1)로 변경
    * [iOS SDK] 기존 최소 버전 iOS 7.0 에서 iOS 8.0으로 변경
* [iOS SDK] .a 에서 .framework 로 SDK 제공방식을 변경했습니다.

### 2018.04.24
#### 버그 수정
* [Mail] 인증서 만료 안내 메일 내 HTML 오류
    * 인증서 만료 안내 메일 내 HTML이 잘 못되어 하단 영역의 배경색이 표시되지않는 오류를 수정했습니다.

#### 기능 개선
* [Console] 오류 메시지 한글화
    * 푸시 Console 내 오류 발생시 표시되는 메시지를 한글화했습니다.

#### 기능 추가
* [Console] 토큰 관리 설정 기능 추가
    * 토큰 만료 기간 설정
        * 설정한 기간동안 등록 요청이 없는 토큰들을 메시지 발송 대상에서 제외합니다.
        * 설정한 기간동안 앱을 사용하지 않는 사용자들의 토큰이 메시지 발송 대상에서 제외할 수 있기때문에 요금을 절약할 수 있습니다.
    * 앱 유형 설정
        * 연동된 앱의 유형에따라 토큰을 관리합니다.
        * 앱의 사용자가 여러 기기에 설치된 앱을 동시에 사용할 수 있는 경우, Multiple로 설정해야 합니다. (기본)
      Multiple로 설정하면 사용자는 여러 개의 토큰을 가지게 됩니다.
      예로, 사용자가 휴대폰과 태블릿을 사용한다면, 두 곳에서 푸시 메시지를 수신합니다.
        * 사용자가 한번에 한 기기에서만 앱을 사용할 수 있다면, Single로 설정해야 합니다.
      Single로 설정하면 사용자는 하나의 토큰만 가지게 됩니다.
      예로, 사용자가 휴대폰과 태블릿을 사용한다면, 두 곳중 한 곳에서만 푸시 메시지를 수신합니다.
* [API] v2.0 토큰 등록 API, deviceId 필드 추가
    * 사용자의 기기를 구별할 수 있도록 deviceId 필드를 추가했습니다.
    * 토큰 등록시 같은 deviceId로 토큰이 있을 경우, 기존의 토큰을 삭제하고, 새로 등록합니다.
    * iOS는 IDFV(identifierForVendor), Android는 Android ID를 설정하는 것을 권장합니다.
    * Device ID를 수집하는 기능이 추가된 SDK는 5월 2일에 배포 예정입니다.

### 2018.03.22
#### 버그 수정
* [API] 태그 이름에 공백 입력이 가능한 오류 수정
    * 태그 생성 API에서 tagName 필드에 공백 입력이 가능한 오류를 수정했습니다.

#### 기능 개선
* [Console] 상품 페이지 내에 있던 탭 메뉴, 콘솔로 이동
    * 콘솔로 탭 메뉴를 옮겨, 좌측 서브 메뉴나 우측 상단에서 페이지를 이동할 수 있습니다.
* [Console] Uid 조회시 토큰을 최근 등록순으로 정렬
    * 콘솔에서 Token 탭에서 Uid 조회시 표시되는 토큰들의 순서를 최근 등록순으로 변경했습니다.

#### 기능 추가
* [API] Uid API 추가
    * Uid에 Tag를 추가/조회/수정/삭제할 수 있는 API를 추가했습니다.
    * 이 API는 Secret Key가 필요 없습니다. 앱에서 호출가능한 API 입니다.
(호출시 Secret Key가 필요한 API를 앱에서 호출할 경우, Secret Key가 외부에 공개될 수 있기때문에 권장하지 않음)

### 2018.02.22
#### 버그 수정
* [API] 예약 메시지 조회시 응답 시간이 길어져 목록을 가져오지 못하는 오류 수정
    * 등록한 예약 메시지가 많을 경우, 응답 시간이 길어져 목록을 가져오지 못하는 오류를 수정했습니다.
* [API] 즉시 발송 및 예약 메시지 조회시 목록 수가 맞지 않는 오류 수정
    * 메시지 조회시 목록 수에 필터링 조건이 포함안되어 목록 수가 맞지 않는 오류를 수정했습니다.
* [API] 메시지 수신/확인 데이터 수집시 UTC 기준 마이너스(-) 시간대의 데이터 수집 안되는 오류 수정
    * UTC 시간 처리시 마이너스(-) 시간대 시간이 정상적으로 처리되지 않아 수집안되는 오류를 수정했습니다.
* [API] 메시지 수신/확인 통계 조회 API에서 event 필드가 적용 안되던 문제 수정
    * event 필드에 값을 설정해도 필터링되지 않는 오류를 수정했습니다.
    event에 설정할 수 있는 값은 다음과 같습니다.
    'SENT', 'SENT_FAILED', 'RECEIVED', 'OPENED'

#### 기능 개선
* [Console] 메시지 발송 페이지 'RemoveGuide' 설명 개선
    * 광고성 메시지 발송시 광고성 푸시 수신 동의 철회 방법 입력란에 예시를 추가했습니다.
    '예, 메뉴 > 설정 > 알림 설정'
* [API] 발송 내역이 있는 예약 메시지 삭제 개선
    * 기존 예약 메시지를 삭제하면, 이미 발송된 내역이 있어도 예약 메시지가 삭제되어 발송 내역 확인에 어려움이 있었습니다.
    * 발송 내역이 있는 예약 메시지 삭제 시도시 삭제되신 상태를 'CANCEL'로 수정해 관리하도록 개선했습니다.
* [ETC] 공통 메시지 발송 개선
    * 기존 공통 메시지 발송시 컨텐츠의 언어 코드와 토큰의 언어 코드가 완전히 같아야 해당 언어 코드로 발송이 되었습니다.
    이번에 언어 코드의 유사성을 측정해 가장 유사한 언어 코드로 발송이 되도록 기능이 개선되었습니다.
    예, 컨텐츠의 언어 코드가 'zh'이고 토큰들의 언어코드가 'zh-Hans', 'zh-Hans-CN'이어도 'zh'로 발송됩니다.

#### 기능 추가
* [API] 메시지 조회 API 조회조건에 deliveryType 추가
    * deliveryType에 설정할 수 있는 값은 다음과 같습니다.
     'INSTANT', 'RESERVATION'
* [API, Console]iOS VoIP 발송 기능 추가
    * iOS로 VoIP 푸시 메시지를 발송하는 기능을 추가했습니다.
    * SDK에서는 현재 지원하지 않으며, 추후 지원 예정입니다.
    * VoIP 발송을 위해서는 다음과 같은 과정이 필요합니다.
        1. VoIP 인증서 등록 (VoIP 전용 인증서 또는 Universal 인증서 등록 가능)
        2. VoIP 토큰 등록 및 푸시 메시지 수신 처리 (토큰의 푸시 타입을 APNS_VOIP 또는 APNS_SANDBOXVOIP로 설정)
        <a href="https://developer.apple.com/library/content/documentation/Performance/Conceptual/EnergyGuide-iOS/OptimizeVoIP.html" target="_blank">Apple iOS Pushkit 가이드 바로가기</a>
        3. 메시지 발송시 푸시 타입 'APNS_VOIP' 또는 'APNS_SANDBOXVOIP'를 선택

### 2017.12.12
#### 버그 수정
* [API] 현지 시간 예약 발송시 발송 시간이 잘 못 계산되는 오류 수정
    * 예약 발송에서 현지 시간 발송(isLocalTime = true)을 사용할 때,
    시간대별 발송 시간 계산 로직 오류를 수정했습니다.

#### 기능 개선
* [ETC] 보안 취약 라이브러리 업데이트
    * 보안 취약점이 발견된 라이브러리를 수정된 버전으로 업데이트했습니다.

### 2017.11.23
#### 기능 추가
* [CONSOLE] Logging 기능 추가
    * 메시지 발송 내역을 Log & Crash Search에 저장할 수 있는 기능을 추가했습니다.
    사용하고 있는 Log & Crash Search의 앱키(Appkey)를 Setting 탭 Logging에 등록해 기능을 활성화 시킬 수 있습니다.
    * 저장된 메시지 발송 내역은 Log & Crash Search 페이지에서 확인할 수 있습니다.
    * <a href="/en/Notification/Push/en/console-guide/#_9" target="_blank">메시지 발송 내역 저장 설명 바로 가기</a>

#### 버그 수정
* [CONSOLE] 저해상도에서 팝업이 상품 사용법에 가려지는 오류 수정
    * 일부 저해상도 화면에서 팝이 노출시 상품 사용법에 가려지는 오류를 수정했습니다.
* [MAIL] 인증서 만료 안내 메일 발송시 잘 못된 앱키가 표시되는 오류
    * 푸시 상품 사용 종료 후 다시 사용한 경우, 인증서 만료 안내 메일 발송시 예전 앱키(Appkey)로 표시되는 오류를 수정했습니다.
* [CONSOLE] Reservation 탭에서 Edit, Delete 버튼 오류 수정
    * Reservation 탭에서 Edit, Delete 버튼이 클릭할 수 없는 상태에서 클릭되는 오류를 수정했습니다.

#### 기능 개선
* [API] v2.0 실패한 메지시 조회 API Limit 추가
    * 기존에는 실패한 메시지 조회시 결과 전체를 응답했습니다.
    결과 크기가 큰경우, Response Timeout이 발생할 수 있어, 한 번에 최대 1,000개 까지 응답하도록 수정했습니다.
    * 결과가 1,000개 이상일 경우, 비정상 응답합니다. 비정상 응답일 경우, from, to 기간을 더 짧게 조회해야 합니다.
    * <a href="/en/Notification/Push/en/api-guide/#_15" target="_blank">API Reference 바로 가기</a>
        * 메시지 > 조회 > 실패한 메시지 목록 조회

### 2017.09.21
#### 버그 수정
* [CONSOLE] Tag 조회시 정렬 기준이 없는 오류 수정
    * Tag 조회시 생성 일자 기준 내림 차순으로 정렬되도록 수정했습니다.
* [CONSOLE] 예약 메시지 등록시 요일이 3개 이상 선택안되는 오류 수정
    * 예약 타입을 'EVERY_WEEK'으로 설정했을 때, 요일이 3 개 이상 선택안되는 오류를 수정했습니다.

#### 기능 개선
* [API] Tag 등록시 이름에 빈칸 허용하지 않도록 수정

### 2017.08.24
#### 기능 추가
* [CONSOLE] Tag 메시지 발송 추가
    * 메시지 발송, 예약 메시지 발송 탭에서 Tag를 선택해 메시지를 발송할 수 있습니다.
    * Target에 Type을 'TAG'로 설정하면, 등록된 Tag들을 선택할 수 있습니다.
    * 선택된 Tag들을 'OR' 또는 'AND' 조건으로 질의해 메시지를 보낼 수 있습니다.
    * 예로, '서울', '30대', '남자' Tag를 선택 후, 'AND' 조건으로 메시지를 발송하면,   
    서울에 사는 30대 남자에게 메시지가 발송 됩니다.
* [CONSOLE] Token 탭 추가
    * 웹콘솔에서 Uid, Token으로 등록된 Token을 검색할 수 있습니다.
    * Uid 검색의 경우 전체 일치뿐만 아니라 부분 일치 검색도 가능합니다.
    * 새로운 토큰을 추가하거나, 검색된 토큰을 삭제할 수 있습니다.
* [CONSOLE] Tag 탭 추가
    * Tag를 관리할 수 있습니다.
    * Tag가 붙은 Uid들을 조회할 수 있습니다.
    * Uid에 Tag를 붙이거나 제거할 수 있습니다.

#### 버그 수정
* [API] 예약 메시지 상태 변경이 안되는 버그 수정
    * 예약 메시지 발송이 완료되었지만, v2.0 예약 API에서 추가된 reservationStatus가 COMPLETED(완료)로 업데이트되지 않는 오류를 수정했습니다.
* [API] 토큰 등록시 oldToken, token 필드에 같은 값이 설정될 경우, 삭제되는 버그 수정
    * 2017년 08월 03일 핫픽스로 수정되었습니다.
    * oldToken은 토큰 변경이 발생하거나, 서버에 저장된 토큰을 새로운 토큰으로 변경하기 위해 사용하는 필드입니다.
    * oldToken에 token과 같은 값을 설정해 토큰 등록 API를 호출할 경우, 삭제 후 등록이 생략되는 버그를 수정했습니다.
    * 패치 후, oldToken과 token이 같으면 삭제 없이 토큰을 업데이트 합니다.
* [SDK] v1.4.2 릴리즈
    * [Android,iOS] 토큰 등록시 잘못된 요청으로 인해 토큰이 삭제될 수 있는 로직에 대한 방어 로직이 추가되었습니다.
    * [Android] PushAnaytics의 초기화 여부를 확인하는 **PushAnalytics.isInitialize** 메소드가 추가되었습니다.

#### 기능 개선
* [API] 알림/홍보성/야간홍보성 푸시 메시지 수신 대상 기준 개선
    * 정보통신망법 규정((제50조부터 제50조의 8)에 따라 대한민국 사용자들의 토큰들은 수신동의 여부에 따라 메시지 발송시 자동 필터링 됩니다.
    * 최근 iOS에서 다양한 언어 코드가 생성되면서 대한민국 사용자 토큰으로 분류되지 않을 수 있는 문제가 있었습니다.
    * 기존에 언어 코드가 'en', 'ko-kr'만 대한민국 사용자 토큰으로 분류했지만,     
    'ko', 'kor' 또는 'ko-'를 포함하는 언어 코드를 대한민국 사용자 토큰으로 분류하도록 개선했습니다.
* [CONSOLE] Channel 메시지 발송 기능 제외
    * Tag 메시지 발송 기능이 추가되면서 CONSOLE에서 Channel 메시지 발송 기능이 제외되었습니다.
    * 기존 Channel 메시지 발송 기능은 v1.3 메시지 발송 API로 이용할 수 있습니다.

### 2017.07.20
#### 기능 추가
* [API] 태그(Tag) API 추가     
    * Uid에 태그를 붙여 관리할 수 있습니다.
    * Uid에 연락처(Contact)을 추가해 관리할 수 있습니다.
    * 메시지 발송시 태그와 조건을 설정해 메시지를 발송할 수 있습니다.    
예, 메시지 발송시 target.type을 'TAG', target.to를 '남자, AND, 30대'로 설정하면, '남자'와 '30대' 태그가 붙은 Uid를 대상으로 메시지가 발송됩니다.
    * API로 먼저 공개되며, 8월 정기 점검 후 CONSOLE에서 태그 기능을 사용하실 수 있습니다.
    <a href="/en/Notification/Push/en/api-guide/#_13" target="_blank">API Reference 바로 가기</a>
* [API] 실패 처리된 메시지 조회 API 추가
    * 메시지 발송시 실패된 메시지를 조회할 수 있는 API가 추가되었습니다.
    이 API를 이용해 발송이 실패 원인에 대한 내용을 확인할 수 있습니다.     
    <a href="/en/Notification/Push/en/api-guide/#_15" target="_blank">API Reference 바로 가기</a>

#### 버그 수정
* [API] 토큰 수정시 새로운 토큰이 존재할 때, 기존 토큰은 삭제 안되는 오류 수정
    * 토큰 등록 API에서 oldToken을 token으로 변경할 때, token이 존재할 경우 oldToken이 삭제 안되던 오류를 수정했습니다.
* [API] 메시지 조회시 Internal Error 응답 오류 수정
    * 메시지 조회시 from, to에 잘 못된 형식의 DateTime(일시)를 입력할 경우 Internal Error로 응답하던 것을 Client Error로 응답하도록 수정했습니다.
* [API] 예약 메시지 수정시 createdDateTime이 잘못 설정되는 오류 수정
    * 예약 메시지 수정시 updatedDateTime(수정 일시)뿐만 아니라 createdDateTime(생성 일시)까지 updatedDateTime 값으로 업데이트되는 오류를 수정했습니다.

### 2017.05.25
#### 기능 추가
* [SDK] SDK 버전 확인을 위한 API 추가
    * SDK 버전 확인을 위한 API가 추가되었습니다.
* [Android SDK] 수신 및 오픈 확인 API 추가 및 Deprecated
    * 수신 및 오픈 확인 API 일부가 추가 및 Deprecated 되었습니다.
    * 해당 기능을 사용하기 위해서 반드시 **PushAnalytics.initialize** 메소드를 호출해줘야 합니다.


### 2017.04.25
#### 기능 추가
* [API] 메시지 수신, 확인 데이터 수집(Message Delivery Receipt), 통계 조회 기능 추가
    * 메시지 발송 후, 기기에 수신, 사용자의 메시지 확인 데이터를 수집해 통계로 조회할 수 있는 기능을 추가되었습니다.
    * [CONSOLE] > [Settings] 탭에서 활성화 시킬 수 있으며, v2.0 API Reference에서 통계 조회 API 설명을 확인할 수 있습니다.
    * 해당 기능은 v1.4이상 SDK가 적용된 곳에서만 사용할 수 있습니다.    
    <a href="/en/Notification/Push/en/sdk-guide/#_4" target="_blank">SDK 수신 및 오픈 여부 적용 가이드 바로 가기</a>
* [API] v2.0 API 추가
    * 토큰 통계 API가 추가되었습니다.
    * 예약 메시지 API가 추가되었습니다.
    * 메시지 수신, 확인 통계 조회 API가 추가되었습니다.
    * v1.3 피드백 API는 v2.0 유효하지 않은 토큰 API로 변경되었습니다.
    * 응답 메시지를 더 자세하게 출력합니다.
    <a href="/en/Notification/Push/en/api-guide" target="_blank">v2.0 API Reference 바로 가기</a>
* [CONSOLE] Dashboard, Setting 탭 추가
    * 메시지 수신, 확인 통계를 확인할 수 있는 [Dashboar]d 탭이 추가되었습니다.
    * 메시지 수신, 확인 데이터 수집 기능을 설정할 수 있는 [Settings] 탭이 추가되었습니다.
* [SDK] v1.4 SDK 추가
    * 메시지 수신, 확인 데이터 수집(Message Delivery Receipt) 기능이 추가되었습니다.
    * 현재 GCM, iOS만 지원하며, Tencent는 추후 지원 예정입니다.
    * iOS는 Notification Service Extension를 사용하기 때문에 iOS 10이상에서만 동작합니다.

### 2017.02.23
#### 버그 수정
* [API] 발송 기간이 한 달 이상인 예약 메시지 발송 안되는 오류 수정
    * 2017년 1월까지 등록된 예약 메시지 중, 발송 종료일이 2월 이상인 예약 메시지가 발송안되는 오류를 수정했습니다.
* [Android SDK] 빌드시 Warning Log 노출되지 않도록 수정
    * 기능상 문제가 없는 것으로, ProGuard 설정 변경을 통해 더 이상 Warning Log가 출력되지 않도록 수정했습니다.
* [iOS SDK] 토큰 리프레쉬 과정에서 크래시나는 현상 수정
    * 앱 알림 설정을 껐다가 다시 켰을 경우 발생하는 오류로 토큰을 재생성하는 코드를 수정했습니다.

#### 기능 개선
* [Android SDK] 안드로이드 Gradle의 play-services 의존을 play-services-gcm로 수정
    * SDK 빌드시 필요한 컴포넌트만 의존하도록 개선했습니다.

### 2017.01.19

#### 기능 개선/변경
* [API] 메시지 조회 API Response Body에 createdDateTime(메시지 생성 시간) 필드 추가
* [Etc] 인증서 만료 안내 메일 계정 변경 (support@cloud.toast.com -> noreply@cloud.toast.com)

### 2016.12.22
#### 버그 수정
* [API] 예약 메시지 등록이 한 달이 지났을 경우 발송 안되는 오류 수정
* [API] 매월 1일 발송될 예약 메시지가 발송 안되는 오류 수정
* [API] 새 버전 FCM API Key가 등록 안되던 오류 수정
* [API] 발송 결과가 'MismatchSenderId', 'NotRegistered'인 경우 토큰이 삭제되지 않던 오류 수정

#### 개발자 가이드 수정
* [Client SDK Developer's Guide] 본문 내 'GCM Push Credentials', 'GCM API Key'로 변경

### 2016.11.24
#### 기능 개선/변경
* [Android SDK] 지원하는 GCM 라이브러리 버전 업데이트(com.google.android.gms:play-services:9.6.0)
* [Android SDK] 오류 로그 세분화

#### 버그 수정
* [Android, iOS SDK] 채널 기본값 null로 변경
* [Android SDK] Appkey가 설정되지 않았을 때 동작안하는 버그 수정
* [Android SDK] AAR 패키징시 텐센트 푸시 설정 제거

#### 개발자 가이드 수정
* [Client SDK Developer's Guide] 토큰 등록시 채널 설정 설명 변경 (SDK v1.3 이하 채널 설정 필수)

### 2016.10.06
#### 기능 개선/변경
* [API, CONSOLE] MPS 단위 1,000개/초에서 100개/초로 변경

### 2016.09.30
#### 개발자 가이드 수정
* [Client SDK Developer's Guide] '토큰 등록 > Android, GCM' 부분, 채널 설정시 'Optional'에서 'Required'로 수정

### 2016.09.29
#### 정책 변경
* 데이터 보관 기간 정책 변경, 최근 30 일까지 저장 (메시지, 예약 메시지, 피드백)

#### 기능 개선/변경
* [CONSOLE] 인증서 삭제 없이 바로 교체할 수 있도록 수정

#### 버그 수정
* [API, CONSOLE] APNS Universal Certificate APNS_SANDBOX(Development)에 등록 안되는 오류 수정
* [API] UID 기준 토큰 조회 API에서 APNS_SANDBOX 토큰이 제외되는 오류 수정
* [API] 토큰 등록 API에서 Empty String("")이 등록 되는 오류 수정

### 2016.08.18
#### 버그 수정
* [CONSOLE] 예약 메시지 수정시 요일이 저장한 내용과 다르게 표시되는 오류 수정
