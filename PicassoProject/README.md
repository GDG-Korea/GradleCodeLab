##Picasso 샘플 프로젝트 빌드 스크립트 작성

###의존성 설정
    
support-v4 라이브러리의 경우 Android SDK 디렉토리의 안드로이드 저장소를 사용하기 때문에 repositories 설정이 필요 없지만 picasso 와 okhttp 라이브러리는 메이븐 중앙 저장소에서 받아오기 떄문에 저장소 설정을 mavenCentral() 로 해준다.
    
    repositories {
        mavenCentral()
    }
    
    dependencies {
        compile 'com.android.support:support-v4:19.0.+'
        compile 'com.squareup.picasso:picasso:2.2.0'
        compile 'com.squareup.okhttp:okhttp:1.5.4'
    }
    
###Product Flavor 디렉토리 구조 만들어주기

Picasso Samples 앱을 약간 변형하여 고흐의 작품이 나오게 하는 Gogh 앱을 flavor 로 생성한다.

공통된 부분은 main 으로 그대로 두고 바뀌는 부분만 각각 picasso, gogh 로 추출한다.

우선 아래와 같이 src 디렉토리내에 3가지 디렉토리가 나타날 수 있도록 picasso 와 gogh 디렉토리를 생성해준다.

    PicassoProject/Picasso/src/main
    PicassoProject/Picasso/src/picasso
    PicassoProject/Picasso/src/gogh
    
PicassoProject/gogh_flavor_files 안에 미리 마련해둔 파일들이 있으니 각각을 아래와 같이 gogh 에 디렉토리를 생성하여 복사한다.

    gogh/java/com/example/picasso/Data.java
    gogh/res/drawable-xhdpi/icon.png
    gogh/res/values/strings.xml
    
main/java/com/example/picasso/Data.java 을 picasso/java/com/example/picasso/Data.java 로 이동한다.

###build.gradle 에 Product Flavor 작성

    android {

        productFlavors {
            picasso {
            }
    
            gogh {
                packageName "org.gdgkoradandroid.gogh"
                versionCode 1
                versionName "1.0.0"
            }
        }

    }
    
### 앱 실행하기

    gradle assemblePicasso
    gradle assembleGogh

###앱 서명 하기

build.gradle 에 바로 입력

    android {

        signingConfigs {
            codelabConfig {
                storeFile file("../keystore/codelab.jks")
                storePassword "********"
                keyAlias "codelab"
                keyPassword "********"
            }
        }
        
    }
    
gradle.properties 를 만들어 속성 참조

    store_file=../keystore/codelab.jks
    store_password=codelab
    key_alias=codelab
    key_password=codelab
    
이런 형태로 gradle.properties 를 생성하고 build.gradle 에서 속성명으로 참조

    android {

        signingConfigs {
            codelabConfig {
                storeFile file(store_file)
                storePassword store_password
                keyAlias key_alias
                keyPassword key_password
            }
        }
    
    }
    
또는 빌드 도중 직접 입력할 수도 있다

    android {

        signingConfigs {
            codelabConfig {
                storeFile file(System.console().readLine('storeFile: '))
                storePassword new String(System.console().readPassword('storePassword: '))
                keyAlias System.console().readLine('keyAlias: ')
                keyPassword new String(System.console().readPassword('keyPassword: '))
            }
        }
        
    }

적용은 각 flavor 에 아래와 같이 signingConfig 에 넣어준다

    android {
    
        productFlavors {
            picasso {
                signingConfig signingConfigs.codelabConfig
            }
    
            gogh {
                packageName "org.gdgkoradandroid.gogh"
                versionCode 1
                versionName "1.0.0"
                signingConfig signingConfigs.codelabConfig
            }
        }
        
    }
