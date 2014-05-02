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

    ependencies {
        compile 'com.android.support:support-v4:19.0.+'
    }
    
###lint 에러 무시

    android {
        
        lintOptions {
            abortOnError false
        }
        
    }
