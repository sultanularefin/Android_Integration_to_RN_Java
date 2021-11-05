


## __settings.gradle__file:

```java



/*

dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
        jcenter() // Warning: this repository is going to shut down soon
    }
}
*/

rootProject.name = "MyTime"
include ':app'

apply from: file("../node_modules/@react-native-community/cli-platform-android/native_modules.gradle"); applyNativeModulesSettingsGradle(settings)


```

## since I put the code in android> build.gradle file:
-------------------------here-------------- below
-------------------------here-------------- below

```java
// Top-level build file where you can add configuration options common to all sub-projects/modules.
buildscript {
    repositories {
        google()
        mavenCentral()
    }
    dependencies {
        classpath "com.android.tools.build:gradle:7.0.3"

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}
-------------------------here-------------- below
-------------------------here-------------- below
-------------------------here-------------- below
allprojects {
    repositories {

        maven {
            // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
            url("$rootDir/../node_modules/react-native/android")
        }
        maven {
            // Android JSC is installed from npm
            url("$rootDir/../node_modules/jsc-android/dist")
        }


        google()
        mavenCentral()
        //jcenter() // Warning: this repository is going to shut down soon


        // below 4 are from tripzchat...
        /*
               mavenCentral()
               mavenLocal()
               google()
               maven { url 'https://www.jitpack.io' }

       */

    }
}


task clean(type: Delete) {
    delete rootProject.buildDir
}
```
