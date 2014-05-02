##코드랩 환경 설정

AndroidStudio 를 사용한다면 Gradle Wrapper 를 이용하고 자동으로 local.properties 에 Android SDK 디렉토리를 자동으로 설정하여 환경변수를 설정할 필요가 없지만 코드랩 진행에 터미널을 이용할 계획이기 때문에 환경변수들을 설정하고 Gradle 을 설치해 주시기 바랍니다.

###환경변수 설정(Java, Android SDK 까지 설치 되어있다고 가정)
- JAVA_HOME 환경변수 설정 JAVA_HOME/bin 을 PATH 에 추가
- Android SDK 설치 디렉토리를 ANDROID_HOME 으로 환경 변수 설정 ANDROID_HOME/tools 를 PATH 에 추가

###Gradle 설치 및 환경변수 설정
1. Gradle 다운로드 [http://www.gradle.org/downloads](http://www.gradle.org/downloads)
2. 압축을 해제 하고 해제한 디렉토리를 GRADLE_HOME 으로 환경변수 설정 PATH 에 GRADLE_HOME/bin 추가

====
####도움이 될만한 곳들

- [Android New Build System - http://tools.android.com/tech-docs/new-build-system](http://tools.android.com/tech-docs/new-build-system)
- [Gradle Android Plugin User Guide - http://tools.android.com/tech-docs/new-build-system/user-guide](http://tools.android.com/tech-docs/new-build-system/user-guide)
- [권남 Gradle - http://kwonnam.pe.kr/wiki/gradle](http://kwonnam.pe.kr/wiki/gradle)
