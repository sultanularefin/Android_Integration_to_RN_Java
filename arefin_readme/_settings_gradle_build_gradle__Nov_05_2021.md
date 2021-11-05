


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



### The Magic: ReactRootView#

## https://reactnative.dev/docs/integration-with-existing-apps#the-magic-reactrootview


Let's add some native code in order to start the **React Native runtime** and tell it **to render our JS component**. To do this, we're going to **create an Activity that creates a ReactRootView, starts a React** application inside it and sets it as the main content view.



### 

```java

public class MyReactActivity extends Activity implements DefaultHardwareBackBtnHandler {
    private ReactRootView mReactRootView;
    private ReactInstanceManager mReactInstanceManager;
```

## Next, we need to pass some activity lifecycle callbacks to the **ReactInstanceManager and ReactRootView**:


## https://github.com/facebook/react-native/issues/28532#issuecomment-624175121

1. https://github.com/facebook/react-native/issues/28532#issuecomment-624175121
2. https://github.com/facebook/react-native/issues/28532#issuecomment-624175121
3. https://github.com/facebook/react-native/issues/28532#issuecomment-624175121
4. https://github.com/facebook/react-native/issues/28532#issuecomment-624175121


6. https://proandroiddev.com/think-before-using-buildconfig-debug-f2e279da7bad?gi=46a1d37a2c2
7. https://proandroiddev.com/think-before-using-buildconfig-debug-f2e279da7bad?gi=46a1d37a2c2
8. https://proandroiddev.com/think-before-using-buildconfig-debug-f2e279da7bad?gi=46a1d37a2c2
9. https://proandroiddev.com/think-before-using-buildconfig-debug-f2e279da7bad?gi=46a1d37a2c2


* .setUseDeveloperSupport(BuildConfig.DEBUG)  ------is linked by this: ::: :: package com.arefin.mytime;




```java

package com.arefin.mytime;
//package com.google.samples.apps.sunflower
//package com.arefin.mytime.Buil
import android.app.Activity;
import android.os.Bundle;

import com.arefin.mytime.MainActivity;
//import com.facebook.react.PackageList;
import com.facebook.react.PackageList;
import com.facebook.react.ReactInstanceManager;
import com.facebook.react.ReactPackage;
import com.facebook.react.ReactRootView;
import com.facebook.react.common.LifecycleState;
import com.facebook.react.modules.core.DefaultHardwareBackBtnHandler;
import com.facebook.soloader.SoLoader;

import java.util.List;

public class MyReactActivity extends Activity implements DefaultHardwareBackBtnHandler {
    private ReactRootView mReactRootView;
    private ReactInstanceManager mReactInstanceManager;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        SoLoader.init(this, false);

        mReactRootView = new ReactRootView(this);
        List<ReactPackage> packages = new PackageList(getApplication()).getPackages();
        // Packages that cannot be autolinked yet can be added manually here, for example:
        // packages.add(new MyReactNativePackage());
        // Remember to include them in `settings.gradle` and `app/build.gradle` too.

        mReactInstanceManager = ReactInstanceManager.builder()
                .setApplication(getApplication())
                .setCurrentActivity(this)
                .setBundleAssetName("index.android.bundle")
                .setJSMainModulePath("index")
                .addPackages(packages)
                .setUseDeveloperSupport(BuildConfig.DEBUG)
                .setInitialLifecycleState(LifecycleState.RESUMED)
                .build();
        // The string here (e.g. "MyReactNativeApp") has to match
        // the string in AppRegistry.registerComponent() in index.js
        mReactRootView.startReactApplication(mReactInstanceManager, "MyReactNativeApp", null);

        setContentView(mReactRootView);
    }

    @Override
    public void invokeDefaultOnBackPressed() {
        super.onBackPressed();
    }
}
```

