 # [프로젝트 1] 자동화 도구 비교 구현
주제: 구글 시트에 새 강의를 입력하면 자동으로 캘린더에 등록하고 알림 보내기

1. 워크플로우 설계 (동일 구조)
Trigger: 구글 시트(Google Sheets)에 새로운 행(강의 정보)이 추가될 때

<img width="907" height="319" alt="image" src="https://github.com/user-attachments/assets/3ab1740e-2a06-4ab6-b2f2-d1b39201579e" />

<br>

Filter: 과목 구분(전공 vs 교양) 확인
조건: '구분' 열의 값이 "전공"인 경우만 실행 (또는 전공/교양에 따라 경로 분리)

<img width="743" height="174" alt="image" src="https://github.com/user-attachments/assets/59dad6a6-506a-44a8-b762-8526458cb209" />

<br>

<img width="1080" height="2340" alt="image" src="https://github.com/user-attachments/assets/3317e55c-535c-4c91-ad31-aa465f8bfde7" />


Action 1: 구글 캘린더(Google Calendar)에 일정 생성
Action 2: 구글 알람 또는 카카오톡(나에게 보내기)으로 강의 등록 알림 전송

<img width="400" height="272" alt="image" src="https://github.com/user-attachments/assets/0cd1052d-b014-419d-8637-d61cb8713bf9" />

<br>




2. 비교 도구 선정: Zapier vs Make (구 Integromat)
비교 항목	Zapier	Make (Integromat)
UI/UX	직관적인 리스트 형태, 초보자 친화적	시각적인 캔버스 형태, 흐름 파악 용이

<img width="662" height="814" alt="image" src="https://github.com/user-attachments/assets/0f4f1185-3ee9-4008-8724-529ea8a5c823" />

<br>


 [프로젝트 1] 비교 분석 보고서에 최소 5개 이상의 비교 항목이 포함되어 있는가?
 
1. 설정 난이도	매우 쉬움 (Step-by-step)	중간 (데이터 매핑 방식이 조금 더 복잡함)
2. 연동 서비스	가장 넓은 범위의 앱 지원	Zapier보다는 적지만 핵심 앱 대부분 지원
3. 무료 플랜	월 100회 실행, 필터 사용 제한적	월 1,000회 실행,
4. 복잡한 필터/루터 가능
5. 실행 로그	깔끔한 리스트 형태	각 모듈별 데이터 흐름을 시각적으로 확인



<br>





 
<br>



# [프로젝트 2] 자유 주제 자동화 설계 및 구현
주제: "오늘의 수업 브리핑 자동화"

1. 업무 정의
매일 아침 8시에 그날 들어야 할 수업 목록(과목명, 시간, 강의실)을 확인하여 나에게 요약 메시지를 보내는 반복 업무를 자동화합니다.

<img width="565" height="141" alt="image" src="https://github.com/user-attachments/assets/e72d6378-e15d-4502-9da4-9f2d3ad746aa" />

<br>



2. 도구 선정 및 이유
선정 도구: Make (Integromat)
선정 이유:무료 플랜에서도 'Router(조건 분기)' 기능을 자유롭게 사용할 수 있습니다.
데이터를 가공(날짜 필터링 등)하는 기능이 Zapier보다 강력하여 시간표 관리에 적합합니다.

<br>


3. 워크플로우 설계 (단계별 설명)
Trigger: Schedule 
매일 정해진 시간에 자동 실행되도록 설정합니다.
<img width="406" height="687" alt="image" src="https://github.com/user-attachments/assets/0c4ae292-586c-4708-8fc5-70c06b97e178" />

Action 1: Google Sheets (Search Rows)
시간표가 적힌 구글 시트에서 '요일' 열이 '오늘 요일'과 일치하는 행들을 찾아옵니다.
Filter/Router: 과목 중요도 판별
<img width="751" height="226" alt="image" src="https://github.com/user-attachments/assets/70e3c789-f5de-4504-a091-feb17f173ff1" />

<img width="484" height="303" alt="image" src="https://github.com/user-attachments/assets/5121ec2c-412f-4e6c-8e21-b4ac6b4878e2" />
경로 A (전공): "전공 수업이 있는 날입니다! 집중하세요!"라는 문구 추가.
경로 B (교양/기타): "비교적 여유로운 교양 수업이 있는 날입니다."라는 문구 추가.
<img width="466" height="367" alt="image" src="https://github.com/user-attachments/assets/0ec4f4c0-fbcb-40a3-a0db-64e7df5e4a46" />

<br>








Action 2: Discord 또는 Slack (Send a Message)
최종 정리된 수업 리스트(과목, 시간, 요일)를 메시지로 전송합니다.
1단계: 기초 데이터 만들기 (Google Sheets)
가장 먼저 자동화의 소스가 될 데이터를 만들어야 합니다.
구글 스프레드시트를 하나 만드세요.
첫 번째 행(헤더)에 다음과 같이 입력하세요:
과목명, 요일, 시간, 강의실, 구분(전공/교양)
테스트용 데이터를 3~5개 정도 입력하세요. (예: 데이터구조, 월요일, 09:00, 201호, 전공)




<img width="921" height="386" alt="image" src="https://github.com/user-attachments/assets/457fb5e1-efb5-405f-b5e0-fd65698ec20b" />


<br>


<br>



2단계: [프로젝트 1] 구현하기 (Zapier & Make)
동일한 흐름을 두 도구에서 각각 만듭니다.


<br>


Zapier(재피어) 접속:
Trigger: Google Sheets - New Spreadsheet Row
Filter: '구분'이 '전공'인 경우만 통과
<img width="409" height="711" alt="image" src="https://github.com/user-attachments/assets/a55300d4-f8d8-4760-a64c-a087545390a8" />

Action 1: Google Calendar - Create Detailed Event


<img width="1080" height="2340" alt="image" src="https://github.com/user-attachments/assets/1ece9a47-eadf-4e04-b5d7-403a59fbb149" />




Action 2:  Gmail - 나에게 알림 보내기



<br>


Make(메이크) 접속:
위와 동일한 순서로 모듈을 배치하여 연결합니다.
📸 캡처 필수:
전체 워크플로우 화면 (연결된 모습)

<img width="850" height="248" alt="image" src="https://github.com/user-attachments/assets/89f31d2e-6ab9-455b-91e0-90078f2e37d3" />

<br>


필터(Filter) 설정창 화면
<img width="429" height="905" alt="image" src="https://github.com/user-attachments/assets/8ffe9fb7-e84f-4c05-9701-f5a842cad624" />

<br>


<br>


<br>
📋 [프로젝트 2] 요구 사항 점검 결과
1. 자동화할 반복 업무 1개 정의

현황: ✅ 완료
내용: "오늘의 수업 브리핑 자동화" (매일 아침 8시 수업 목록 요약 메시지 전송)라고 명확하게 정의하셨습니다.
2. 도구 1개를 선정하고 선정 이유 작성

현황: ✅ 완료
내용: 'Make'를 선정하셨고, 이유로 '무료 플랜의 Router 기능'과 '강력한 데이터 가공 기능'을 구체적으로 작성하셨습니다.
3. 자동 실행 구조 구현 (Trigger/Action/Router)



4. 워크플로우 흐름 설명 포함

현황: ✅ 완료
내용: 1단계(기초 데이터)부터 3단계(Router 설정)까지 단계별로 상세히 설명되어 있어 충분합니다.



# 3단계: [프로젝트 2] 구현하기 (자유 주제)

[프로젝트 1]에서 만든 것을 조금 더 발전시키거나, 새로운 시나리오를 만듭니다. **'조건 분기(Router)'**가 핵심입니다.
Trigger: 구글 시트 새 행 추가
<img width="938" height="607" alt="image" src="https://github.com/user-attachments/assets/078fae68-9e8b-4b2e-81ae-f32797246c07" />

Router 설치: 경로를 두 개로 나눕니다.
경로 1 (전공): 필터 설정 후 전공 전용 액션 수행
경로 2 (교양): 필터 설정 후 교양 전용 액션 수행

📸 캡처 필수:
실제로 실행된 후, 두 경로 모두 초록색 체크 표시가 뜬 결과 화면 (각각 한 번씩 실행해봐야 함)
4단계: 보고서 작성 (Markdown 또는 PDF)
캡처한 사진들을 넣고 아래 내용을 텍스트로 정리합니다.
<img width="666" height="260" alt="image" src="https://github.com/user-attachments/assets/1eb95396-32f5-439a-b51c-e0e778eb7307" />


<br>


1. 도구 비교표
항목	Zapier	Make	나의 의견
사용 난이도	쉬움	조금 어려움	Zapier는 처음 사용하기 편했고, Make는 익숙해지는 데 시간이 조금 걸렸다.
인터페이스	단순	시각적	Make는 모듈 연결이 한눈에 보여 흐름을 이해하기 쉬웠다.
조건 분기	제한적	Router 제공	Router를 이용해 전공과 교양을 쉽게 구분할 수 있어서 편리했다.
데이터 가공	기본 수준	다양함	Make는 Filter와 Router를 함께 사용할 수 있어 다양한 자동화가 가능했다.
무료 플랜	제한 있음	비교적 자유	과제를 수행하기에는 Make의 무료 기능이 더 충분하다고 느꼈다.


<br>



2. 프로젝트 2에서 Make를 선택한 이유

프로젝트 2에서는 Make를 사용하였다. Make는 Router 기능을 이용하여 전공과 교양을 쉽게 분기할 수 있었고, 시각적으로 모듈이 연결되어 있어 자동화 과정을 이해하기 쉬웠다. 
또한 Discord와 연동하여 조건에 맞는 메시지를 자동으로 전송하는 기능을 구현하기 편리하다고 생각하였다.

<br>


3. 용어 설명

Trigger
**'방아쇠'**라고 생각하면 이해하기 쉽습니다. 방아쇠를 당기면 총알이 자동으로 발사되듯이, [어떤 사건(Event)이 발생했을 때 정해진 동작이 자동으로 실행되는 것을 의미해요.

Action
액션(Action)은 '무엇을(What)' 할지를 결정한다."

Filter
'구분' 값을 확인하여 각각 다른 경로로 데이터를 보내는 역할을 한다.

트리거: "만약 ~하면?" (조건/시점)
액션: "그럼 이걸 해!" (실행 내용)

EX>
Trigger: Google Sheets Watch New Rows
Action: Discord Send a Message
Filter: 전공/교양 구분
Router: 전공과 교양을 각각 다른 메시지로 분기



