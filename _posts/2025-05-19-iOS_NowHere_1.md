---
title: "iOS 앱 개발 해보기: 지금여기(NowHere) 1"
date: 2025-05-19 14:38 +09:00
categories: [iOS, 지금여기]
tags:
  [
    iOS,
    앱개발,
    지금여기,
    .
    .
    .
  ]
---

# iOS 앱 개발 해보기: 지금여기(NowHere) 1

## 앱 개발을 하게 된 계기

예전부터 앱 개발을 해보고 싶다고 막연히 생각하기만 했다.

이렇게 생각만 하다가 못 할 거 같아서 일단 저질러보았다.

![한번 해보죠](https://github.com/jungi0531/images/blob/main/blog_images/iOS_NowHere_1/Lets_Try.jpeg?raw=true)


## 왜 iOS 앱 개발?

앱 개발 중 iOS 앱 개발을 하게 된 이유는 다음과 같다

- 크로스 플랫폼도 가능하나 Swift를 사용해보고 싶었음
- iOS 환경에 최적화된 앱을 만들고 싶었음
- 내가 쓸 수 있는 앱 만들기

이러한 이유로 iOS쪽으로 시작해보았다.

## 어떤 앱을 개발?

그런 다음 이제 어떤 앱을 만들까인데, 사실 내가 엄청 기술적으로 훌륭한 앱을 만들어 경쟁성을 확보하기란 지금 앱 시장에서 힘들 거 같다고 생각했다.

나는 그런 쪽보다는 사람들이 감성적으로 공감 할 수 있는 앱을 만들어 사람들이 흥미를 느끼고 앱에 정이 들게 하고 싶었다.

그래서 명상 기록 앱을 만들려고 한다.

내가 생각한 앱은 명상 기록 앱이다.

명상 기록 앱으로 정하게 된 이유는 내가 이런 필요성을 느꼈고 만들어보면 어떨까 싶어서이다. 내가 흥미를 가지는 분야이기에 더욱 몰입해서 만들 수 있을 것 같았다. 또 아무도 안 쓰면 나라도 쓰면 되니까!

앱의 이름은 '지금여기(NowHere)'로 정했다.

내가 만들 앱의 주요 기능

- 명상 수행 앱
- 명상 수행을 기록
- 명상 기록을 저장 및 통계내어 명상 진척도 파악 

또한 내가 앱을 만들어 중요하게 볼 부분은

- 귀여운 마스코트 캐릭터 디자인하기
- 컴팩트한 UI
- 사용자가 매일 사용할 수 있는 앱

사실 이런 느낌으로 한 일주일 정도 앱을 만들어보았다.

### 앱 아이콘

![앱 아이콘](https://github.com/jungi0531/images/blob/main/blog_images/iOS_NowHere_1/App_Icon.png?raw=true)

이런 식으로 귀여운 캐릭터를 내세운 앱을 만들고 싶었고 약 일주일간 만들어 보았다.

현재 앱은 아래와 같은 기능을 가지고 있다.

- 타이머 설정 후 명상 수행
- 명상 수행 후 기록
- 지금까지 명상 기록을 확인하는 통계 기능

### 홈 화면

![홈 화면](https://github.com/jungi0531/images/blob/main/blog_images/iOS_NowHere_1/Home_View.png?raw=true)

### 명상 타이머 설정 화면

![명상 타이머 설정 화면](https://github.com/jungi0531/images/blob/main/blog_images/iOS_NowHere_1/Timer_View.png?raw=true)

### 명상 수행 후 기록 화면

![명상 수행 후 기록 화면](https://github.com/jungi0531/images/blob/main/blog_images/iOS_NowHere_1/Record_View.png?raw=true)

### 출석 캘린더 뷰

![출석 캘린더 뷰](https://github.com/jungi0531/images/blob/main/blog_images/iOS_NowHere_1/Calendar_View.png?raw=true)

### 통계 뷰

![통계 뷰](https://github.com/jungi0531/images/blob/main/blog_images/iOS_NowHere_1/Statistic_View.png?raw=true)

### 기록 뷰

![기록 뷰](https://github.com/jungi0531/images/blob/main/blog_images/iOS_NowHere_1/History_View.png?raw=true)

아직까지는 UI도 어설프고 특별한 기능도 없지만, 계속해서 개발해보고 앱 배포까지 해보는 게 내 목표다.

## 앱 개발 하며 느낀점

약 일주일 간 앱을 만들고 느낀점은 코드 구조화가 상당히 중요한 거 같다.

스위프트에 대해 잘 몰라 그냥 짜는대로 코드를 짜고 폴더 분류도 안 하고 하다보니 나중에 뭘 수정하려고 하면 생각해보고 손 봐야할 부분이 많아져서 힘들었다.

### 현재 코드 구조 상황

![현재 코드 구조](https://github.com/jungi0531/images/blob/main/blog_images/iOS_NowHere_1/Code_Structure.png?raw=true)

마냥 코드 구조화가 중요하다고 하기에 그렇구나라고 생각했는데, 실제로 해보니 정말 중요하다고 느꼈다.

그렇기에 지금까지 코드들을 구조화부터 한 후에 추가적으로 발전시키려고 한다.

이후 더 추가시키고 싶은 기능은

- 애플 로그인 + 아이클라우드 연동 기능 
- 기록 쪽 UI 이쁘게 다듬기
- 명상 종료 시 소리로 알리기
- 설정 창 만들기
- 알람 설정 기능

이런 것들이다.

우선 코드 구조화부터 하고 나서 추가적으로 기능을 넣어보려고 한다.

> Apple Developer Program 가입비 연간 129,000원... 당분간 밥은 공식당 돈까스다.