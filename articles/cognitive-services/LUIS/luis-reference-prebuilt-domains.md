---
title: 미리 작성된 도메인 참조 - Azure | Microsoft Docs
titleSuffix: Azure
description: LUIS(Language Understanding Intelligent Services)에서 미리 작성된 의도 및 엔터티 컬렉션에 해당하는 미리 작성된 도메인에 대한 참조입니다.
services: cognitive-services
author: diberry
manager: cgronlun
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 11/26/2018
ms.author: diberry
ms.openlocfilehash: 287a0986d921798bc7735e5a75d279f010712b16
ms.sourcegitcommit: 922f7a8b75e9e15a17e904cc941bdfb0f32dc153
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52335626"
---
# <a name="prebuilt-domain-reference"></a>미리 작성된 도메인 참조
이 참조는 LUIS에서 제공하는 의도 및 엔터티의 미리 작성된 컬렉션에 해당하는 [미리 작성된 도메인](luis-how-to-use-prebuilt-domains.md)에 대한 정보를 제공합니다.

반대로, [사용자 지정 도메인](luis-how-to-start-new-app.md)은 의도 및 모델 없이 시작합니다. 사용자 지정 모델에 미리 작성된 도메인 의도 및 엔터티를 추가할 수 있습니다.

## <a name="list-of-prebuilt-domains"></a>미리 작성된 도메인 목록
LUIS는 20가지의 미리 작성된 도메인을 제공합니다. 

| 미리 빌드된 도메인 | 설명 | 지원되는 언어 |
| ---------------- |-----------------------|:------:|
| Calendar | Calendar 도메인은 약속을 추가, 삭제 또는 편집하고, 참가자 가용성을 확인하고, 일정 이벤트에 대한 정보를 찾기 위한 의도 및 엔터티를 제공합니다.| en-US<br/> zh-CN |
| Camera | Camera 도메인은 사진을 촬영하고, 비디오를 녹화하고, 비디오를 응용 프로그램으로 브로드캐스트하기 위한 의도 및 엔터티를 제공합니다.| en-US |
| 통신 | 메시지 전송 및 전화 통화| en-US <br/> zh-CN |
| Entertainment  | 음악, 동영상, TV 관련 쿼리 처리| en-US |
| 이벤트 | 콘서트, 축제, 스포츠 게임 및 코미디 쇼 티켓 예약| en-US |
| Fitness | 피트니스 활동 추적과 관련된 요청 처리| en-US |
| 게임 | 멀티플레이 게임의 게임 파티와 관련된 요청 처리| en-US |
| HomeAutomation | 조명 및 어플라이언스와 같은 스마트 홈 장치 제어| en-US<br/> zh-CN |
| MovieTickets | 영화관의 영화 티켓 예약| en-US |
| 음악 | 뮤직 플레이어에서 음악 재생| en-US<br/> zh-CN |
| 참고 | Note 도메인은 메모 생성, 편집 및 찾기와 관련된 의도 및 엔터티를 제공합니다.| en-US<br/> zh-CN |
| OnDevice | OnDevice 도메인은 장치 제어와 관련된 의도 및 엔터티를 제공합니다.| en-US<br/> zh-CN |
| 장소  | 회사, 기관, 식당, 공용 공간 및 주소와 같은 장소 관련 쿼리 처리| en-US<br/> zh-CN |
| 미리 알림 | 미리 알림 생성, 편집 및 찾기와 관련된 요청 처리| en-US<br/> zh-CN |
| RestaurantReservation | 식당 예약에 대한 관리 요청 처리| en-US<br/> zh-CN |
| Taxi | 택시 예약 처리| en-US<br/> zh-CN |
| 번역 | 텍스트를 대상 언어로 번역| en-US<br/> zh-CN |
| TV | TV 제어| en-US |
| 공공 시설  | "도움말", "반복”, “다시 시작”과 같이 많은 도메인에서 공통되는 요청 처리| en-US |
| Weather | 날씨 보고서 및 예측 가져오기| en-US<br/> zh-CN |
| 웹 | 웹 사이트 탐색| en-US<br/> zh-CN |

각 도메인에 대한 자세한 내용은 다음 섹션을 참조하세요.

## <a name="calendar"></a>Calendar 

Calendar 도메인은 일정 항목과 관련된 의도 및 엔터티를 제공합니다. Calendar 의도에는 약속 추가, 삭제 또는 편집, 가용성 확인, 일정 항목 또는 약속에 대한 정보 찾기가 포함됩니다.

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| 추가 | 일정에 일회용 항목을 새로 추가합니다.| 일요일 오후 2시에 Lisa와 약속을 합니다. <br/><br/>모임을 예약하려고 합니다.<br/><br/>모임을 설정해야 합니다.|
| CheckAvailability | 사용자의 일정 또는 다른 사람의 일정에서 약속 또는 모임에 대한 가용성을 찾습니다.| Jim과 언제 모임을 할 수 있나요? <br/><br/>Carol이 내일 시간이 있다고 표시합니다.<br/><br/>토요일에 Chris는 시간이 있나요?|
| 삭제 | 일정 항목 삭제를 요청합니다.| Carol과의 약속을 취소합니다. <br/><br/>오전 9시 모임을 삭제합니다.<br/>|
| 편집 | 기존 모임 또는 일정 항목을 변경하도록 요청합니다.| 오전 9시 모임을 오전 10시 모임으로 이동합니다.<br/><br/>일정을 업데이트하려고 합니다.<br/><br/>Ryan과의 모임 일정을 다시 예약합니다.|
| 찾기 | 주간 일정을 표시합니다.| 치과 검사 약속을 찾습니다. <br/><br/>내 달력을 표시합니다.<br/>|

### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| 위치 | 일정 항목, 모임 또는 약속의 위치입니다. 주소, 도시 및 지역은 위치의 좋은 예입니다.| 209 Nashville Gym <br/><br/>897 Pancake house<br/><br/>Garage|
| 제목 | 모임 또는 약속의 제목입니다.| 치과 약속 <br/><br/>Julia와의 점심 식사<br/><br/>의사 약속|

## <a name="camera"></a>Camera 
Camera 도메인은 카메라 사용과 관련된 의도 및 엔터티를 제공합니다. 의도에는 사진, 셀피, 스크린샷 또는 비디오 캡처, 응용 프로그램으로 비디오 브로드캐스트가 포함됩니다.

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| CapturePhoto| 사진을 캡처합니다.| 사진 찍기<br/><br/>캡처|
| CaptureScreenshot | 스크린샷을 캡처합니다.| 스크린샷을 만듭니다.<br/><br/>화면을 캡처합니다.|
| CaptureSelfie | 셀피를 캡처합니다.| 셀피 만들기 <br/><br/>내 사진 찍기 |
| CaptureVideo | 비디오 녹화를 시작합니다.| 녹화 시작 <br/><br/>기록 시작|
| StartBroadcasting| 브로드캐스트 비디오를 시작합니다.| Facebook으로의 브로드캐스트 시작|
| StopBroadcasting| 비디오 브로드캐스트를 중지합니다.| 브로드캐스트 중지|
| StopVideoRecording| 비디오 녹화를 중지합니다.| 충분해요.<br/><br/>기록 중지|

### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| AppName | 비디오를 브로드캐스트할 응용 프로그램의 이름입니다.| OneNote<br/><br/>Facebook<br/><br/>Skype|


## <a name="communication"></a>통신 
Communication 도메인은 전자 메일, 메시지 및 전화 통화와 관련된 의도 및 엔터티를 제공합니다.

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| AddContact| 사용자의 연락처 목록에 새 연락처를 추가합니다.|새 연락처 추가 <br/><br/>이 번호를 저장하고 Carol이라고 이름을 지정합니다.|
| AddMore| 단계적 전자 메일 또는 텍스트 구성의 일부로 전자 메일 또는 텍스트에 내용을 더 추가합니다.|텍스트에 내용 더 추가 <br/><br/>전자 메일 본문에 내용 더 추가|
| 응답| 들어오는 전화 통화를 받습니다.|통화 받기 <br/><br/>받기|
| AssignContactNickname| 연락처에 애칭을 할당합니다.|Isaac을 아빠로 변경 <br/>Jim의 애칭 편집<br/>Patti Owens에 애칭 추가|
| CallVoiceMail| 사용자의 음성 메일에 연결합니다.|내 음성 사서함 상자에 연결 <br/>음성 사서함<br/>음성 사서함 연결|
| CheckIMStatus| Skype에서 연락처의 상태를 확인합니다.|Jim의 온라인 상태가 자리 비움으로 설정되어 있나요? <br/>Carol과 채팅할 수 있나요?|
| Confirm| 작업을 확인합니다.|yes<br/>확인<br/>좋습니다.<br/>이 전자 메일을 보내려고 합니다.<br/>|
| Dial| 전화 통화를 합니다.|Jim에게 전화하기<br/>311 번호를 누르세요.<br/>|
| FindContact| 연락처 정보를 이름으로 찾습니다.|Carol의 번호 찾기<br/>Carol의 번호 표시<br/>|
| FindSpeedDial| 전화 번호를 설정할 단축번호와 단축번호를 설정할 전화 번호를 찾습니다.|내 다이얼 번호 5는 무엇인가요?<br/>설정된 단축번호가 있나요?<br/>941-5555-333의 다이얼 번호는 무엇인가요?|
| GetForwardingsStatus| 착신 전환의 현재 상태를 가져옵니다.|내 착신 전환이 켜져 있나요?<br/>내 호출 상태가 설정되었는지 또는 해제되었는지 알아보기<br/>|
| Goback| 이전 단계로 돌아갑니다.|Twitter으로 돌아가기<br/>한 단계 뒤로 이동<br/>뒤로 이동|
| 무시| 수신 전화를 무시합니다.|받지 않음<br/>전화 무시|
| IgnoreWithMessage| 수신 전화를 무시하고, 대신 문자로 회신합니다.|해당 전화를 받지 않고, 대신 메시지를 보냅니다.<br/>무시하고 문자를 다시 보냅니다.|
| PressKey| 단추 또는 키패드의 숫자를 누릅니다.|별표를 누릅니다.<br/>1 2 3을 누릅니다.|
| ReadAloud| 사용자에게 메시지 또는 전자 메일을 읽어줍니다.|텍스트를 읽어줍니다.<br/>메시지에 어떤 내용을 말했나요?|
| TurnForwardingOff| 전화 통화를 합니다.|<br/><br/>|
| Redial| 전화를 다시 겁니다.|다시 전화를 겁니다.<br/>마지막에 걸었던 전화를 다시 겁니다.|
| 거부| 수신 전화를 거부합니다.|전화 거부<br/>지금은 전화를 받을 수 없습니다.<br/>지금은 전화를 받을 수 없으므로 나중에 다시 전화하겠습니다.|
| SendEmail| 전자 메일을 보냅니다. 이 의도는 문메자 시지가 아닌 전자 메일에 적용됩니다.|Mike Waters에게 전자 메일 보내기: Mike, 지난 주에 함께 했던 저녁 식사는 아주 멋졌어요.<br/>Bob에게 전자 메일 보내기<br/>|
| SendMessage| 문자 메시지 또는 인스턴트 메시지를 보냅니다.|Chris 및 Carol에게 문자 보내기|
| SetSpeedDial| 연락처의 전화 번호에 대해 단축번호를 설정합니다.|Carol에 단축번호 1을 설정합니다.<br/>엄마에게 단축번호를 설정합니다.|
| ShowNext| 예를 들어 문자 메시지 또는 전자 메일 목록의 다음 항목을 표시합니다.|다음 항목을 표시합니다.<br/>다음 페이지로 이동합니다.|
| ShowPrevious| 예를 들어 문자 메시지 또는 전자 메일 목록의 이전 항목을 표시합니다.|이전 항목을 표시합니다.<br/>이전<br/>이전으로 이동합니다.|
| StartOver| 시스템 다시 시작하거나 새 세션을 시작합니다.|다시 시작<br/>새 세션<br/>restart|
| TurnForwardingOff| 착신 전환을 해제합니다.|내 통화 착신 전화 중지<br/>착신 전환 끄기|
| TurnForwardingOn| 스피커 폰을 끕니다.|내 통화를 3333으로 착신 전환<br/>3333으로 착신 전환 켜기|
| TurnSpeakerOff| 스피커 폰을 끕니다.|스피커를 끕니다.<br/>스피커 폰을 해제합니다.<br/>|
| TurnSpeakerOn| 스피커 폰을 켭니다.|스피커 폰 모드입니다.<br/>스피커 폰을 설정합니다.<br/>|

### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| AudioDeviceType | 오디오 장치(스피커, 헤드셋, 마이크 등)의 종류입니다.| 발표자<br/>핸즈프리<br/>Bluetooth|
| Category | 메시지 또는 전자 메일의 범주입니다.| 중요<br/>높은 우선 순위|
| ContactAttribute | 사용자가 조회하는 연락처의 특성입니다.| Birthdays<br/>주소<br/>전화 번호|
| ContactName | 연락처 또는 메시지 받는 사람의 이름입니다.| Carol<br/>Jim<br/>Chris|
| EmailSubject | 전자 메일 제목 줄로 사용되는 텍스트입니다.| RE: 흥미로운 이야기|
| 꺾은선형 | 사용자가 전화를 걸거나 문자/전자 메일을 전송하려는 회선입니다.| 회사 회선<br/>영국 휴대폰<br/>Skype|
| Message | 전자 메일 또는 문자로 보낼 메시지입니다.| 오늘 만나서 즐거웠습니다. 곧 다시 만나요!|
| MessageType | 연락처 또는 메시지 받는 사람의 이름입니다.| 텍스트<br/>Email|
| OrderReference | 검색할 항목을 식별하는 목록의 서수 또는 상대 위치입니다. 예를 들어 "내가 보낸 마지막 메시지는 무엇이었나요?"에서 "마지막" 또는 "최근"을 나타냅니다.| 마지막<br/>최근|
| SenderName | 보낸 사람의 이름입니다.| Patti Owens|

## <a name="entertainment"></a>Entertainment  
Entertainment 도메인은 영화, 음악, 게임 및 TV 쇼 검색과 관련된 의도 및 엔터티를 제공합니다.

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| 검색| 영화, 음악, 앱, 게임 및 TV 쇼를 검색합니다.|스토어에서 Halo를 검색합니다.<br/>Avatar를 검색합니다.|

### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| ContentRating | 영화에 대한 G 또는 R과 같은 미디어 콘텐츠 등급입니다.|어린이 비디오입니다.<br/>PG 등급입니다.|
| Genre | 영화, 게임, 앱 또는 노래의 장르입니다.|코미디<br/>드라마<br/>오락용|
| 키워드| 특성을 지정하는 제네릭 검색 키워드는 좀 더 구체적인 미디어 슬롯에 존재하지 않습니다.|사운드 트랙<br/>문리버<br/>Amelia Earhart|
| 언어 | 영화 또는 노래의 음성 언어와 같이 미디어에서 사용되는 언어입니다.|프랑스어<br/>영어<br/>한국어|
| MediaFormat | 미디어 형식을 지정하는 추가적인 특별 기술 유형입니다.|HD 동영상<br/>3D 동영상<br/>다운로드 가능|
| MediaSource | 미디어 획득을 위한 스토어 또는 마켓플레이스입니다.|Netflix<br/>Prime|
| MediaSubTypes| 영화 및 게임보다 작은 미디어 유형입니다.|데모<br/>Dlc<br/>트레일러|
| Nationality| 영화, 쇼 또는 노래가 만들어진 국가입니다.|프랑스어<br/>독일어<br/>한국어|
| 사람| 영화, 앱, 게임 또는 TV 쇼와 관련된 배우, 감독, 프로듀서, 음악가 또는 예술가입니다.|Madonna<br/>Stanley Kubrick|
| 역할| 미디어 제작에서 사람이 맡은 역할입니다.|노래<br/>감독<br/>기준|
| 제목| 영화, 앱, 게임, TV 쇼 또는 노래의 이름입니다.|Friends<br/>Minecraft|
| type| 영화, 앱, 게임, TV 쇼 또는 노래의 종류 또는 미디어 형식입니다.|Music<br/>MovieTV <br/>쇼|
| UserRating| 사용자 별 또는 엄지척 등급입니다.|별 5개<br/>별 3개<br/>별 4개|

## <a name="events"></a>이벤트 
Events 도메인은 콘서트, 축제, 스포츠 게임 및 코미디 쇼와 같은 이벤트 티켓의 예약과 관련된 의도 및 엔터티를 제공합니다.

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| Book| 이벤트 티켓을 구입합니다.|이번 주말에 심포니 티켓을 구입하고 싶습니다.|


### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| 주소 | 이벤트 위치 또는 주소입니다. |Palo Alto<br/>300 112th Ave SE <br/> 시애틀 |
| 이름 | 이벤트의 이름입니다.|Shakespeare in the Park|
| PlaceName| 이벤트 위치 이름입니다.|루브르<br/>오페라 하우스<br/>브로드웨이|
| PlaceType | 이벤트가 열릴 위치의 유형입니다.|카페<br/>극장<br/>라이브러리|
| type | 이벤트의 유형입니다.|콘서트<br/>스포츠 게임|

## <a name="fitness"></a>Fitness 
Fitness 도메인은 피트니스 활동 추적과 관련된 의도 및 엔터티를 제공합니다. 의도에는 메모 저장, 남은 시간이나 거리, 활동 결과 저장이 포함됩니다.

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| AddNote| 추적된 활동에 보충 메모를 추가합니다.|이 달리기의 어려움은 6/10이었습니다.<br/>달리고 있는 지형은 아스팔트 길입니다.<br/>3단 변속 자전거를 사용하고 있습니다.|
|GetRemaining| 활동에 대해 남은 시간 또는 거리를 가져옵니다.|다음 랩까지 몇 시간이 남았나요?<br/>달리기에서 남은 마일 수는 얼마인가요? 스플릿 시간은 얼마나 되나요?|
| LogActivity| 완료된 활동 결과를 저장하거나 기록합니다.|마지막 달리기 저장<br/>내 토요일 오전 도보 기록<br/>내 이전 수영 저장|
| LogWeight| 사용자의 현재 체중을 저장하거나 기록합니다.|내 현재 체중 저장<br/>지금 내 체중 기록<br/>내 현재 체중 저장|

### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| ActivityType | 추적할 활동의 유형입니다. |실행<br/>도보<br/>수영<br/>주기 |
| Food | 피트니스 앱에서 추적할 음식 유형입니다. |Banana<br/>연어<br/>단백질 셰이크|
| MealType| 건상 또는 피트니스 앱에서 추적할 식사 유형입니다.|아침<br/>저녁<br/>점심<br/>간단한 저녁|
| 측정| 피트니스 또는 건강 앱에 사용하기 위한 시간, 거리 또는 체중 측정 유형입니다.|킬로미터<br/>마일<br/>분<br/>킬로그램|
| Number | 피트니스 또는 건강 앱에 사용할 수치 수량입니다.|19<br/>three<br/>200<br/>one|
| StatType | 피트니스 또는 상태 앱에 사용할 집계된 데이터에 대한 통계 유형입니다.|합계<br/>평균<br/>최대<br/>최소|

## <a name="gaming"></a>게임 
Gaming 도메인은 멀티플레이어 게임의 게임 파티 관리와 관련된 의도 및 엔터티를 제공합니다.

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| InviteParty| 게임 파티에 조인하도록 대화 상대를 초대합니다.|이 플레이어를 내 파티에 초대<br/>내 파티에 참석해줘<br/>내 클랜에 가입해줘|
|LeaveParty| 활동에 대해 남은 시간 또는 거리를 가져옵니다.|나는 나갈게<br/>다른 사람을 위해 이 파티에서 나갈게<br/>종료 중이야|
| StartParty| 멀티플레이 게임에서 게임 파티를 시작합니다.|파티를 시작해 봅시다.<br/>파티를 시작하자<br/>오늘 클랜을 시작해야 해|

### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| 연락처| 멀티플레이 게임에서 사용할 대화 상대 이름입니다.|Carol<br/>Jim|


## <a name="homeautomation"></a>HomeAutomation 
HomeAutomation 도메인은 조명 및 어플라이언스와 같은 스마트 홈 장치 제어와 관련된 의도 및 엔터티를 제공합니다.

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| TurnOff| 장치를 끄거나, 닫거나, 잠금을 해제합니다.|조명 끄기<br/>커피 메이커 중지<br/>차고 문 닫기|
|TurnOn| 장치를 켜거나 장치를 특정 설정 또는 모드로 지정합니다.|커피 메이커 켜기<br/>내 커피 메이커를 켤 수 있나요?<br/>자동 온도 조절기를 72도로 설정합니다.|


### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| 장치 | 켜거나 끌 수 있는 장치 유형입니다.|커피 메이커<br/>자동 온도 조절기<br/>조명|
| 작업(Operation) | 장치의 설정 상태입니다.|lock<br/>open<br/>on<br/>끄기|
| 공간 | 장치가 있는 위치 또는 방입니다.|거실<br/>침실<br/>주방|

## <a name="movietickets"></a>MovieTickets 
MovieTickets 도메인은 영화관의 영화 티켓 예약과 관련된 의도 및 엔터티를 제공합니다.

### <a name="examples"></a>예
```
Book me two tickets for Captain Omar and the two Musketeers
Cancel tickets
When is Captain Omar showing?
```

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| Book | 영화 티켓을 구입합니다.|Captain Omar 티켓 2장과 musketeer 티켓 2장을 예약해주세요.<br/>내일 볼 영화 티켓을 구입하려고 합니다.<br/>다음 수요일에 상영하는 Captian Omar Part 2 티켓을 원합니다.|
|GetShowTime| 영화 상영 시간을 알아봅니다.|Captain Omar 상영 시간은 언제인가요?|


### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| 주소 | 영화관의 주소입니다.|Palo Alto<br/>300 112th Ave SE<br/>시애틀|
| MovieTitle | 영화 제목입니다.|Life of Pi<br/>Hunger Games<br/>Inception|
| PlaceName | 영화관 또는 시네마의 이름입니다.|Cinema Amir<br/>Alexandria Theatre<br/>New York Theater|
| PlaceType | 영화가 상영되는 위치의 유형입니다.|영화<br/>극장<br/>IMAX cinema|

## <a name="music"></a>Music 
Music 도메인은 뮤직 플레이어의 음악 재생과관 련된 의도 및 엔터티를 제공합니다.

### <a name="examples"></a>예
```
play Beethoven
Increase track volume
Skip to the next song
```

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| DecreaseVolume | 장치 볼륨을 줄입니다.|트랙 볼륨 낮추기<br/>볼륨 작게|
| IncreaseVolume | 장치 볼륨을 높입니다.|트랙 볼륨 높이기<br/>볼륨 크게|
| Mute |재생 음악을 음소거합니다.|노래 음소거<br/>트랙 음소거<br/>음악 음소거 |
| 일시 중지 | 음악 재생을 일시 중지합니다.|일시 중지<br/>음악 일시 중지<br/>트랙 일시 중지|
| PlayMusic | 장치에서 음악을 재생합니다.|Kevin Durant 재생<br/>Coldplay의 Paradise 재생<br/>Adele의 Hello 재생|
| Repeat |음악 재생을 반복합니다.|노래 반복<br/>트랙 다시 재생<br/>음악 반복|
| 다시 시작 | 음악 재생을 다시 시작합니다.|노래 다시 시작<br/>음악 다시 시작<br/>일시 중지 해제|
| SkipBack | 한 트랙 뒤로 건너뜁니다.|다음 노래로 이동<br/>다음 곡 재생|
| SkipForward |한 트랙 앞으로 건너뜁니다.|이전 곡 재생<br/>이전 트랙으로 돌아가기 |
| 중지 | 음악 재생에 관련된 작업을 중지합니다. |이 앨범 재생을 중지합니다.|
| Unmute | 음악 재생 장치의 음소거를 해제합니다.| 음소거를 해제합니다.|

### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| ArtistName | 장치에서 재생할 미디어와 관련된 배우, 감독, 프로듀서, 작가, 음악가 또는 예술가입니다.|Elvis Presley<br/>Taylor Swift<br/>Adele<br/>Mozart|
| Genre | 요청된 음악의 장르입니다.|컨트리 음악<br/>브로드웨이 클래식<br/>바로크 시대의 고전 음악 재생|

## <a name="note"></a>참고 
Note 도메인은 메모 생성, 편집 및 찾기와 관련된 의도 및 엔터티를 제공합니다.

### <a name="examples"></a>예
```
Add to my groceries note lettuce tomato bread coffee
Check off bananas from my grocery list
Remove all items from my vacation list
```

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| AddToNote | 메모에 정보를 추가합니다.|내 식료품 메모에 양배추, 토마토, 빵, 커피 추가<br/>할 일 목록에 추가<br/>내 Wunderlist에 컵 케이크 추가|
| CheckOffItem | 기존 노트에서 항목에 표시합니다.|식료품 목록에서 바나나에 표시<br/>휴일 쇼핑 목록에서 치즈 케이크를 완료로 표시|
| 지우기 | 기존 메모에서 모든 항목의 선택을 취소합니다.|내 휴가 목록에서 모든 항목 제거<br/>내 읽기 목록에서 모두 지우기|
| Confirm | 메모와 관련된 작업을 확인합니다.|모두 괜찮음<br/>예<br/>목록에 모든 항목이 있는지 확인함|
| 생성 | 새 메모를 만듭니다. | 목록 만들기<br/>Jason이 5월의 첫째 주에 마을에 있을 것임을 미리 알려주는 메모|
| 삭제 | 전체 메모를 삭제합니다. |내 휴가 목록 삭제 <br/>내 식료품 메모 삭제|
| DeleteNoteItem | 기존 메모에서 항목을 삭제합니다.| 내 식료품 목록에서 감자튀김 삭제<br/>내 학교 쇼핑 목록에서 펜 제거|
| ReadAloud | 목록을 소리내어 읽습니다.|첫 번째 항목 읽어주기<br/>세부 정보 읽어주기|
| ShowNext | 메모 목록의 다음 항목을 봅니다.|다음 항목 표시<br/>다음 페이지<br/>다음|

### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| AppName | 메모 기록 응용 프로그램 이름입니다.|Wunderlist<br/>OneNote|
| ContactName | 메모에 있는 연락처의 이름입니다.|Carol<br/>Jim<br/>Chris|
| DataSource | 메모의 위치입니다.|OneDrive<br/>Google 문서<br/>내 컴퓨터|
| DataType | 일반적으로 특정 소프트웨어 프로그램과 관련된 파일 또는 문서의 형식입니다.|슬라이드<br/>스프레드시트<br/>워크시트|
| 텍스트 | 메모 또는 미리 알림의 텍스트입니다.|도보 전에 스트레칭<br/>내일 오래 달리기|
| 제목 | 메모의 제목입니다.|식료품<br/>통화할 사람<br/>할 일|

## <a name="ondevice"></a>OnDevice 
OnDevice 도메인은 장치 제어와 관련된 의도 및 엔터티를 제공합니다.

### <a name="examples"></a>예
```
Close video player
Cancel playback
Can you make the screen brighter?
```

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| AreYouListening | 장치가 수신 대기 중인지 문의합니다.|켜져 있나요?<br/>수신 증인가요?|
|CloseApplication|장치 응용 프로그램을 닫습니다.|비디오 플레이어 닫기|
|FileBug|장치의 버그를 정리합니다.|버그를 정리하세요.<br/>버그를 정리해줄 수 있나요?<br/>이 버그를 보고하겠습니다.|
|GoBack|한 단계 뒤로 돌아가거나 이전 단계로 돌아가도록 요청합니다.|돌아가세요.<br/>이전 화면으로 이동<br/>돌아가서 수신 중지|
|도움말| 도움을 요청합니다.|도와주세요.<br/>안녕하세요.<br/>어떻게 해야 합니까?<br/>도움이 필요합니다.| 
|LocateDevice|장치를 찾습니다.|내 휴대폰을 찾을 수 있나요?<br/>Tom의 iphone 찾기<br/>내 휴대폰 찾기|
|LogIn|장치를 사용하여 서비스에 로그인합니다.|로그인하세요.<br/>Facebook 로그인<br/>LinkedIn에 로그인|
|LogOut|장치를 사용하여 서비스에서 로그아웃합니다.|내 휴대폰에서 로그오프<br/>Twitter에 로그온<br/>로그아웃|
|MainMenu|장치의 주 메뉴를 표시합니다.|보기 메뉴|
|OpenApplication|장치에서 응용 프로그램을 엽니다.|경보를 여세요.<br/>카메라 켜기<br/>일정 시작|
|OpenSetting|장치에서 설정을 엽니다.|네트워크 설정을 엽니다.|
|PairDevice|장치와 쌍으로 연결합니다.|Bluetooth 신호를 휴대폰에 연결하는 데 도움을 줄 수 있나요?<br/>Bluetooth를 켜고 랩톱에 연결<br/>Bluetooth 신호를 랩톱에 연결|
|PowerOff | 장치를 끕니다.|내 컴퓨터를 종료할 수 있나요?<br/>Shutdown<br/>내 휴대폰 끄기|
|QueryBattery|배터리 수명에 대한 정보를 얻습니다.|배터리 수명을 표시합니다.<br/>내 배터리 상태<br/>남아 있는 배터리 용량은 얼마나 되나요?<br/>배터리 표시|
|QueryWifi|WiFi에 대한 정보를 얻습니다.|WiFi 정보를 얻습니다.|
|다시 시작|장치를 다시 시작합니다.|다시 시작하세요.|
|RingDevice| 장치를 분실한 경우 찾기 위해 벨소리를 내도록 요청합니다.|휴대폰이 울리도록 합니다.| 
|SetBrightness|장치 밝기를 설정합니다.|밝기를 중간으로 설정<br/>밝기를 높음으로 설정<br/>밝기를 낮음으로 설정|
|SetupDevice|장치 설치를 시작합니다.|OS 설치 프로그램을 설치합니다.<br/>설치하세요.<br/>자동으로 설치|
|ShowAppBar|앱 바를 표시합니다.|응용 프로그램 표시줄 표시<br/>응용 프로그램 표시줄<br/>응용 프로그램 표시줄을 표시하겠습니다.|
|ShowContextMenu|상황에 맞는 메뉴를 표시합니다.|상황에 맞는 메뉴를 표시하겠습니다.<br/>상황에 맞는 메뉴<br/>상황에 맞는 메뉴는 표시할 수 있나요?|
|절전|장치를 절전 모드로 전환합니다.|절전 모드로 전환<br/>절전<br/>내 컴퓨터 절전 모드|
|SwitchApplication|장치에서 사용하도록 응용 프로그램을 전환합니다.|내 미디어 플레이어로 전환합니다.|
|TurnDownBrightness|장치 밝기를 줄입니다.|화면을 흐리게 표시합니다.|
|TurnOffSetting|장치 설정을 해제합니다.|Bluetooth 비활성화<br/>데이터 사용 안 함<br/>Bluetooth 연결 끊기|
|TurnOnSetting|장치 설정을 켭니다.|다른 <br/> 꺼짐|
|TurnUpBrightness|장치 밝기를 높입니다.|화면을 더 밝게 만들 수 있나요?|

### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| AppName | 장치의 응용 프로그램 이름입니다.|SoundCloud<br/>YouTube|
| BrightnessLevel | 장치의 밝기 수준을 설정합니다.|100%<br/>50<br/>40%|
| ContactName | 장치에 있는 연락처의 이름입니다.|Paul<br/>Marlen Max|
| DeviceType | 장치의 유형입니다. |Phone<br/>Kindle<br/>랩톱|
| MediaType | 장치에서 처리하는 미디어 유형입니다.|음악<br/>영화<br/>TV 쇼|
| SettingType | 사용자가 편집하려는 설정 또는 설정 패널의 유형입니다.|WiFi<br/>무선 네트워크<br/>색 구성표<br/>알림 센터|

## <a name="places"></a>Places  
Places 도메인은 회사, 기관, 식당, 공용 공간 및 주소와 같은 장소 관련 쿼리 처리를 위한 의도를 제공합니다.

### <a name="examples"></a>예
```
Save this location to my favorites
How far away is Holiday Inn?
At what time does Safeway close?
```

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| AddFavoritePlace | 사용자의 즐겨찾기 목록에 위치를 추가합니다.|이 위치를 내 즐겨찾기에 저장<br/>이 주소를 내 즐겨찾기에 추가|
|CheckAccident|지정된 도로에 사고가 있었는지를 문의합니다.|880 도로에 사고가 있었나요?<br/>사고 정보 표시|
|CheckAreaTraffic|지정된 경로가 아닌 일반 영역 또는 고속도로에 대한 교통량을 확인합니다.|시애틀의 교통량<br/>시애틀의 교통량은 어떤가요?|
|CheckIntoPlace|소셜 미디어를 사용하여 장소에 체크 인합니다.|Foursquare에 체크인<br/>여기에 체크 인|
|CheckRouteTraffic| 사용자가 지정한 특정 경로의 교통량을 확인합니다.|마시코 교통량은 어떤가요?<br/>커클랜드 교통량 표시<br/>시애틀 교통량은 어떤가요?| 
|Confirm|장소와 관련된 작업을 확인합니다.|내 식당 예약을 확인합니다.|
|끝내기|장소와 관련된 작업을 종료하는 동작입니다.|종료하세요.<br/>지침 제시 중단|
|FindPlace|장소(회사, 기관, 식당, 공용 공간, 주소)를 검색합니다.|가장 가까운 도서관은 어디에 있나요?<br/>산 경치가 보이는 이탈리안 식당 찾기|
|GetAddress| 장소의 주소를 요청합니다.|Robson street의 Guu 주소 표시<br/>가장 가까운 스타벅스 주소는 무엇인가요?| 
|GetDistance|특정 장소까지의 대략적인 거리를 요청합니다.|Holiday Inn은 얼마나 멀리 떨어져 있나요?<br/>여기에서 벨브 광장까지 얼마나 먼가요?<br/>타호까지의 거리|
|GetHours|장소의 운영 시간을 문의합니다.|Safeway는 몇 시에 문을 닫나요?<br/>Home Depot 시간은 얼마나 되나요?<br/>스타벅스는 아직 열려 있나요?|
|GetMenu|식당의 메뉴 항목을 문의합니다.|Zucca에서 채식주의자에게 음식을 제공하나요?<br/>Sizzler의 메뉴에 포함된 음식<br/>Applebee 메뉴 표시|
|GetPhoneNumber| 장소의 전화 번호를 요청합니다.|가장 가까운 스타벅스 전화 번호는 무엇인가요?<br/>Home Depot의 번호 가져오기| 
|GetPriceRange| 장소의 가격 범위를 문의합니다.|Zucca는 저렴한가요?<br/>수요일마다 Cineplex를 절반 가격으로 이용할 수 있나요?<br/>Sizzler에서 랍스터 1마리 저녁 식사 비용은 얼마나 되나요?|
|GetReviews|장소에 대한 검토를 요청합니다.|Cheesecase Factory에 대한 검토 내용 표시<br/>Yelp에서 Cineplex 검토 읽기|
|GetRoute|장소로 가는 길을 요청합니다.|도보로 벨브 광장까지 이동하는 방법<br/>여기에서 8번가 및 59번가까지 가는 최단 경로 표시<br/>Mountain View CA로 가는 길 보기|
|GetStarRating|장소의 별 등급을 요청합니다.|Yelp에 따르면 Zucca 등급은 어떤가요?<br/>French Laundry의 별 등급은 무엇인가요?<br/>몬테레이의 아쿠아리움은 좋은가요?|
|GetTransportationSchedule|장소의 버스 스케줄을 가져옵니다.|시내로 가는 다음 버스는 몇 시에 오나요?<br/>킹 카운티의 버스 표시|
|GetTravelTime|지정된 목적지까지의 여행 시간을 문의합니다.|여기에서 샌프란시스코까지 가려면 얼마나 걸리나요?<br/>SF에서 덴버까지 주행 시간은 얼마나 되나요?|
|MakeCall|장소로 전화를 겁니다.|엄마에게 전화하기<br/>Skype로 Anna와 통화하고 싶습니다.<br/>Jim에게 전화하기|
|MakeReservation|식당 또는 기타 비즈니스석 예약을 요청합니다.|야간 시간에 Zucca에서 2명 예약<br/>내일을 위해 테이블 예약<br/>Palo Alto에서 8시에 3인용 테이블 예약|
|MapQuestions|목적지로 가는 길 또는 지정된 도로를 통해 목적지까지 갈 수 있는지 여부에 대한 정보를 요청합니다.|13번이 시내를 통과하나요?<br/>880번을 타고 오클랜드까지 갈 수 있나요?|
|등급|식당 또는 장소에 대한 등급 설명을 확인합니다.|Contoso Inn의 별 등급은 무엇인가요?|
|ReadAloud|장소 목록을 소리내어 읽습니다.|첫 번째 항목 읽어주기<br/>세부 정보 읽어주기|
|SelectItem|장소와 관련된 선택 옵션 목록에서 항목을 선택합니다.|두 번째 선택<br/>첫 번째 선택|
|ShowMap|영역의 지도를 표시합니다.|두 번째에 대한 지도 표시<br/>지도 표시<br/>지도에서 샌프란시스코 찾기|
|ShowNext|시리즈의 다음 항목을 표시합니다.|다음 항목 표시<br/>다음 페이지로 이동|
|ShowPrevious|시리즈의 이전 항목을 표시합니다.|이전 항목 표시<br/>previous<br/>이전으로 이동|
|StartOver|앱을 다시 시작하거나 새 세션을 시작합니다.|다시 시작<br/>새 세션<br/>
restart|
|TakesReservations|장소가 예약을 받는지 문의합니다.|아트 갤러리에서 예약을 받나요?<br/>Olive Garden에서 예약을 할 수 있나요?

### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| AbsoluteLocation | 장소의 위치 또는 주소입니다.|Palo Alto<br/>300 112th Ave SE<br/>시애틀|
| Amenities | 장소의 목표 특성/이점입니다.|어린이 식사 무료<br/>해변가<br/>무료 주차|
| Atmosphere | 장소의 분위기입니다.|어린이에게 친숙<br/>일반 식당<br/>경쾌함|
| Cuisine | 장소의 요리 방식입니다. |지중해식<br/>이탈리아어<br/>인도식|
| DestinationAddress| 목적지 위치 또는 주소입니다.|Palo Alto<br/>300 112th Ave SE<br/>시애틀|
| DestinationPlaceName| 회사, 식당, 공공 명소 또는 기관에 해당하는 목적지의 이름입니다.|중앙 공원<br/>세이프웨이<br/>월마트|
| DestinationPlaceType | 현지 회사, 식당, 공공 명소 또는 기관에 해당하는 목적지의 유형입니다. |식당<br/>Opera<br/>영화관|
| Distance | 장소까지의 거리입니다.|15마일<br/>5마일<br/>10마일 떨어짐|
| MealType | 아침 식사 또는 점심 식사와 같은 식사 유형입니다. |아침<br/>저녁<br/>점심<br/>간단한 저녁|
| OpenStatus | 장소가 열려 있는지 또는 닫혀 있는지를 나타냅니다.|열기<br/>closed<br/>열려 있음|
| PlaceName | 장소의 이름입니다.|Cheesecake Factory|
| PlaceType | 장소의 유형입니다.|카페<br/>극장<br/>라이브러리|
| PreferredRoute | 사용자가 지정한 기본 경로입니다. | 101 <br/>202 <br/>Route 401|
| 제품 | 장소가 제공하는 제품입니다. | 의류<br/>디지털 ASR 카메라<br/>신선한 생선 | 
| PublicTransportationRoute | 사용자가 검색하는 대중 교통 수단 경로 이름입니다. | Northeast corridor 열차<br/>버스 노선 3X |
| 등급 | 장소의 등급입니다. | 별 5개<br/>별 3개<br/>별 4개|
| RouteAvoidanceCriteria | 특정 경로를 피하는 기준(예: 사고, 건설 또는 통행료) | 통행료 <br/>건설<br/>Route 11|
| ServiceProvided | 회사 또는 장소가 제공하는 서비스(예: 헤어컷, 제설기, 경치)입니다. | 헤어컷<br/>정비<br/>배관공|
| TransportationCompany | 전송 공급업체의 이름입니다.|Amtrak<br/>Acela<br/>Greyhound|
| TransportationType | 교통 유형입니다.|버스<br/>학습<br/>Driving|

## <a name="reminder"></a>미리 알림 
reminder 도메인은 미리 알림 생성, 편집 및 찾기에 대한 의도 및 엔터티를 제공합니다.

### <a name="examples"></a>예
```
Change my interview to 9 am tomorrow
Remind me to buy milk on my way back home
Can you check if I have a reminder about Christine's birthday?
```

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| 변경| 미리 알림을 변경합니다.|내 인터뷰를 내일 오전 9시로 변경<br/>과제 미리 알림을 내일로 전환|
| 생성| 새 미리 알림을 만듭니다.|미리 알림 만들기<br/>우유를 구매하도록 미리 알림<br/>집에 있을 때 Rebecca와 통화할 것을 잊지 않고 싶습니다.|
| 삭제 | 미리 알림을 삭제합니다.|내 사진 미리 알림 삭제<br/>이 미리 알림 삭제|
| 찾기 | 미리 알림을 찾습니다.|내 기념일에 대한 미리 알림이 있나요?<br/>Christine의 생일에 대한 미리 알림이 있는지 확인할 수 있나요?|

### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| 텍스트 | 미리 알림의 텍스트 설명입니다.|드라이 클리닝 선택<br/>자동차를 서비스 센터에 두기|

## <a name="restaurantreservation"></a>RestaurantReservation 
RestaurantReservation 도메인은 식당 예약 관리와 관련된 의도 및 엔터티를 제공합니다.

### <a name="examples"></a>예
```
Reserve at Zucca for two for tonight
Book a table at BJ's for tomorrow
Table for 3 in Palo Alto at 7
```

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| Reserve | 식당에 대한 예약을 요청합니다. |야간 시간에 Zucca에서 2명 예약<br/>내일을 위해 테이블 예약<br/>Palo Alto에서 7시에 3인용 테이블 예약|

### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| 주소| 예약의 이벤트 위치 또는 주소입니다.|Palo Alto<br/>300 112th Ave SE<br/>시애틀|
| Amenities | 장소의 부대 시설을 설명하는 특성입니다.|바다 전망<br/>금연|
| AppName | 예약하기 위한 응용 프로그램의 이름입니다.|OpenTable<br/>Yelp<br/>TripAdvisor|
| Atmosphere | 식당 또는 다른 장소의 분위기에 대한 설명입니다.|로맨틱<br/>일반<br/>그룹에 적합|
| Cuisine | 음식의 유형, 요리 방식 또는 어느 나라 요리인지를 나타냅니다. |중국어<br/>이탈리아어<br/>멕시칸|
| MealType | 예약과 연결된 식사 유형입니다.|아침<br/>저녁<br/>점심<br/>간단한 저녁|
| PlaceName | 현지 회사, 식당, 공공 명소 또는 기관의 이름입니다.|IHOP<br/>Cheesecake Factory<br/>루브르|
| PlaceType | 현지 회사, 식당, 공공 명소 또는 기관의 유형입니다.|식당<br/>오페라<br/>영화|
| 등급 | 장소나 식당의 등급입니다.|별 5개<br/>별 3개<br/>별 4개|

## <a name="taxi"></a>Taxi 
 
Taxi 도메인은 택시 예약을 만들고 관리하기 위한 의도 및 엔터티를 제공합니다.

### <a name="examples"></a>예
```
Get me a cab at 3 pm
How much longer do I have to wait for my taxi?
Cancel my Uber
```

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| Book | 택시를 부릅니다. |내게 택시 불러주기<br/>택시 찾기<br/>우버 x에서 예약|
| 취소 | 택시 예약와 관련된 작업을 취소합니다.|내 택시 취소<br/>내 우버 취소|
| Track | 택시 경로를 추적합니다.|택시가 올 때까지 얼마나 더 기다려야 하나요?<br/>내 우버는 어디에 있나요?|

### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| 주소| 택시 예약과 관련된 주소입니다. |Palo Alto<br/>300 112th Ave SE<br/>시애틀|
| DestinationAddress| 목적지 위치 또는 주소입니다. |Palo Alto<br/>300 112th Ave SE<br/>시애틀|
| DestinationPlaceName | 현지 회사, 식당, 공공 명소 또는 기관에 해당하는 목적지의 이름입니다. |중앙 공원<br/>세이프웨이<br/>월마트|
| DestinationPlaceType | 현지 회사, 식당, 공공 명소 또는 기관에 해당하는 목적지의 유형입니다. |식당<br/>Opera<br/>영화관|
| PlaceName | 현지 회사, 식당, 공공 명소 또는 기관의 이름입니다. |중앙 공원<br/>세이프웨이<br/>월마트|
| PlaceType| 택시 예약을 요청할 장소 유형입니다.|식당<br/>Opera<br/>영화관|
| TransportationCompany | 전송 공급업체의 이름입니다.|Amtrak<br/>Acela<br/>Greyhound|
| TransportationType | 교통 유형입니다.|버스<br/>학습<br/>Driving|

## <a name="translate"></a>번역 
Translate 도메인은 텍스트를 대상 언어로 번역하는 것과 관련된 의도 및 엔터티를 제공합니다.

### <a name="examples"></a>예
```
Translate to French
Translate hello to German
Translate this sentence to English
```

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| 번역| 텍스트를 다른 언어로 번역합니다.|프랑스어로 번역<br/>Hello를 독일어로 번역|


### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| TargetLanguage | 번역의 대상 언어입니다.|프랑스어<br/>독일어<br/>한국어|
| 텍스트 | 번역할 텍스트입니다.|Hello World<br/>안녕하세요.<br/>안녕하세요.|

## <a name="tv"></a>TV 
 
TV 도메인은 TV를 제어하기 위한 의도 및 엔터티를 제공합니다.

### <a name="examples"></a>예
```
Switch channel to BBC
Show TV guide
Watch National Geographic
```

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| ChangeChannel| TV 채널을 변경합니다.|채널을 CNN으로 변경<br/>BBC로 채널 전환<br/>채널 4로 이동|
| ShowGuide| TV 가이드를 표시합니다.|TV 가이드 표시<br/>지금 영화 채널에는 어떤 영화가 제공되나요?<br/>내 프로그램 목록 표시|
| WatchTV| TV 채널을 시청할 것을 요청합니다.|Disney 채널을 시청하려고 합니다.<br/>TV로 이동하세요.<br/>내셔널 지오그래픽 시청|

### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| ChannelName | TV 채널의 이름입니다.|CNN<br/>BBC<br/>영화 채널|

## <a name="utilities"></a>공공 시설  
Utilities 도메인은 인사말, 취소, 확인, 도움말, 반복, 탐색, 시작 및 중지 등과 같이 여러 작업에서 공통적으로 진행되는 작업에 대한 의도를 제공합니다.

### <a name="examples"></a>예
```
Go back to Twitter
Please help
Repeat last question please
```

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| 취소 | 작업을 취소합니다.|메시지 취소<br/>전자 메일을 더 이상 전송하지 않으려고 합니다.|
| Confirm | 작업을 확인합니다.|내가 확인합니다.<br/>좋습니다. 제가 확인해보겠습니다.<br/>잘 알겠습니다. 제가 확인해보겠습니다.|
| FinishTask | 사용자가 시작한 작업을 완료합니다.|완료했습니다.<br/>끝냈습니다.<br/>완료되었습니다.|
| GoBack | 한 단계 뒤로 돌아가거나 이전 단계로 돌아갑니다.|Twitter로 돌아가기<br/>한 단계 뒤로 이동<br/>뒤로 이동|
| 도움말 | 도움말을 요청합니다.|도와주세요.<br/>도움말 열기<br/>help|
| Repeat | 작업을 반복합니다.|마지막 질문을 반복하세요.<br/>마지막 노래 반복|
| ShowNext | 시리즈의 다음 항목을 표시합니다. |다음 항목 표시<br/>다음 페이지로 이동|
| ShowPrevious | 시리즈의 이전 항목을 표시합니다.|이전 항목 표시|
| StartOver | 앱을 다시 시작하거나 새 세션을 시작합니다.|다시 시작<br/>새 세션<br/>restart|
| 중지 | 작업을 중지합니다.| 말하기 중지<br/>입 좀 다물어요<br/>중지하세요.|

## <a name="weather"></a>Weather 
Weather 도메인은 날씨 보고서 및 예측을 가져오기 위한 의도 및 엔터티를 제공합니다.

### <a name="examples"></a>예
```
weather in London in september
What?s the 10 day forecast?
What's the average temperature in India in september?
```

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| GetCondition | 날씨와 관련된 기록 정보를 가져옵니다. |9월의 런던 날씨<br/>9월에 인도 평균 온도는 얼마나 되나요?|
| GetForecast | 현재 날씨와 향후 며칠 동안의 날씨 예측을 얻습니다. |오늘 날씨는 어떤가요?<br/>10일 예측은 무엇인가요?<br/>이번 주말의 날씨는 어떨까요?|

### <a name="entities"></a>엔터티
| 엔터티 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| 위치| 날씨 요청에 대한 절대 위치입니다.|시애틀<br/>파리<br/>Palo Alto|

## <a name="web"></a>웹 
Web 도메인은 웹 사이트를 탐색하기 위한 의도를 제공합니다.

### <a name="examples"></a>예
```
Navigate to facebook.com
Go to www.twitter.com
Navigate to www.bing.com
```

### <a name="intents"></a>의도
| 의도 이름 | 설명 | 예 |
| ---------------- |-----------------------|----|
| 이동 | 지정된 웹 사이트를 탐색하기 위한 요청입니다. |facebook.com으로 이동<br/>www.twitter.com으로 이동|

