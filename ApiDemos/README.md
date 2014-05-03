##ApiDemos 빌드 스크립트 작성

ApiDemos 프로젝트 루트 디렉토리 아래에 build.gradle 파일을 생성하고 아래의 내용을 따라 빌드 스크립트를 작성한다.

###Gradle Android Plugin classpath 설정

    buildscript {
        repositories {
            mavenCentral()
        }
        dependencies {
            classpath 'com.android.tools.build:gradle:0.10.+'
        }
    }

###Android 플러그인 적용

    apply plugin: 'android'
    
주의) buildscript 아래에 위치 해야 한다.

###컴파일 SDK 버전과 Android 빌드툴 버전 설정

    android {
        compileSdkVersion 19
        buildToolsVersion '19.0.3'
    }
    
###매니페스트, 소스코드, 리소스 디렉토리 설정

    android {
        
        sourceSets {
            main {
                manifest.srcFile 'AndroidManifest.xml'
                java.srcDirs = ['src']
                resources.srcDirs = ['src']
                aidl.srcDirs = ['src']
                renderscript.srcDirs = ['src']
                res.srcDirs = ['res']
                assets.srcDirs = ['assets']
            }
        }
        
    }

###Android Support-v4 라이브러리 의존성 설정

    dependencies {
        compile 'com.android.support:support-v4:19.0.+'
    }
    
###lint 에러 무시

    android {
        
        lintOptions {
            abortOnError false
        }
        
    }

###안드로이드 SDK 경로 설정

안드로이드 빌드를 위해 다음 중 한 가지 방법을 사용하여 안드로이드 SDK 경로를 설정해야 합니다. 이 항목을 설정하지 않으면 다음과 같은 에러 메시지가 표시됩니다.

    FAILURE: Build failed with an exception.

    * What went wrong:
    A problem occurred configuring root project 'ApiDemos'.
    > SDK location not found. Define location with sdk.dir in the local.properties file or with an ANDROID_HOME environment variable.

####local.properties 사용
프로젝트 루트 경로에 `local.properties` 를 생성한 후, 아래와 같이 안드로이드 SDK가 설치된 경로를 입력합니다.

    sdk.dir=[안드로이드 SDK가 설치된 경로]

예시 :  
    
    sdk.dir=/Users/kunny/android-sdk-macosx

####ANDROID_HOME 환경변수 설정
위 방법 외에, 환경 변수의 `ANDROID_HOME`에 안드로이드 SDK의 경로를 설정하면 `local.properties` 파일 없이 사용할 수 있습니다.

예시 :

    export ANDROID_HOME=/Users/kunny/android-sdk-macosx


