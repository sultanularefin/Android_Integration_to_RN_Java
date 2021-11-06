


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


## run output::

```java

Executing tasks: [:app:assembleDebug] in project /home/arefin/Programs/eazm__/Android_Integration_to_RN_Java/android

> Task :app:generatePackageList
> Task :app:preBuild
> Task :app:preDebugBuild
> Task :app:compileDebugAidl NO-SOURCE
> Task :app:compileDebugRenderscript NO-SOURCE
> Task :app:dataBindingMergeDependencyArtifactsDebug
> Task :app:dataBindingMergeGenClassesDebug
> Task :app:generateDebugResValues
> Task :app:generateDebugResources
> Task :app:generateDebugBuildConfig
> Task :app:javaPreCompileDebug
> Task :app:createDebugCompatibleScreenManifests
> Task :app:checkDebugAarMetadata
> Task :app:extractDeepLinksDebug
> Task :app:processDebugMainManifest
> Task :app:mergeDebugResources
> Task :app:processDebugManifest
> Task :app:dataBindingGenBaseClassesDebug
> Task :app:mergeDebugNativeDebugMetadata NO-SOURCE
> Task :app:mergeDebugShaders
> Task :app:compileDebugShaders NO-SOURCE
> Task :app:generateDebugAssets UP-TO-DATE
> Task :app:mergeDebugAssets
> Task :app:processDebugManifestForPackage
> Task :app:compressDebugAssets
> Task :app:processDebugJavaRes NO-SOURCE
> Task :app:desugarDebugFileDependencies
> Task :app:mergeDebugJniLibFolders
> Task :app:checkDebugDuplicateClasses
> Task :app:mergeDebugJavaResource
> Task :app:mergeLibDexDebug
> Task :app:mergeDebugNativeLibs
> Task :app:validateSigningDebug
> Task :app:processDebugResources

> Task :app:stripDebugDebugSymbols
Unable to strip the following libraries, packaging them as they are: libbetter.so, libc++_shared.so, libfabricjni.so, libfb.so, libfbjni.so, libfolly_futures.so, libfolly_json.so, libglog.so, libglog_init.so, libhermes-executor-common-debug.so, libhermes-executor-common-release.so, libhermes-executor-debug.so, libhermes-executor-release.so, libhermes-inspector.so, libimagepipeline.so, libjsc.so, libjscexecutor.so, libjsi.so, libjsijniprofiler.so, libjsinspector.so, liblogger.so, libmapbufferjni.so, libnative-filters.so, libnative-imagetranscoder.so, libreact_codegen_rncore.so, libreact_debug.so, libreact_nativemodule_core.so, libreact_render_animations.so, libreact_render_attributedstring.so, libreact_render_componentregistry.so, libreact_render_core.so, libreact_render_debug.so, libreact_render_graphics.so, libreact_render_imagemanager.so, libreact_render_leakchecker.so, libreact_render_mapbuffer.so, libreact_render_mounting.so, libreact_render_runtimescheduler.so, libreact_render_scheduler.so, libreact_render_telemetry.so, libreact_render_templateprocessor.so, libreact_render_textlayoutmanager.so, libreact_render_uimanager.so, libreact_utils.so, libreactconfig.so, libreactnativeblob.so, libreactnativejni.so, libreactnativeutilsjni.so, libreactperfloggerjni.so, librrc_image.so, librrc_modal.so, librrc_progressbar.so, librrc_root.so, librrc_scrollview.so, librrc_slider.so, librrc_switch.so, librrc_text.so, librrc_textinput.so, librrc_unimplementedview.so, librrc_view.so, libturbomodulejsijni.so, libyoga.so.

> Task :app:compileDebugJavaWithJavac
Note: /home/arefin/Programs/eazm__/Android_Integration_to_RN_Java/android/app/src/main/java/com/arefin/mytime/MainActivity.java uses or overrides a deprecated API.
Note: Recompile with -Xlint:deprecation for details.

> Task :app:compileDebugSources
> Task :app:dexBuilderDebug
> Task :app:writeDebugAppMetadata
> Task :app:writeDebugSigningConfigVersions
> Task :app:mergeExtDexDebug
> Task :app:mergeProjectDexDebug
> Task :app:packageDebug
> Task :app:assembleDebug

BUILD SUCCESSFUL in 25s
33 actionable tasks: 33 executed

Build Analyzer results available

```



## yarn android output:


```java

ctionable tasks: 1 executed, 1 up-to-date
Done in 15.22s.
arefin@arefin-HP-ProBook-450-G0:~/Programs/eazm__/Android_Integration_to_RN_Java$ yarn android
yarn run v1.22.5
$ react-native run-android
info Running jetifier to migrate libraries to AndroidX. You can disable it using "--no-jetifier" flag.
Jetifier found 870 file(s) to forward-jetify. Using 4 workers...
info JS server already running.
info Installing the app...

> Task :app:compileDebugJavaWithJavac

> Task :app:installDebug
Installing APK 'app-debug.apk' on 'Redmi Note 7 - 10' for app:debug
Installed on 1 device.

BUILD SUCCESSFUL in 1m 31s
34 actionable tasks: 14 executed, 20 up-to-date
info Connecting to the development server...
8081
info Starting the app on "68efca1a"...
Starting: Intent { cmp=com.arefin.mytime/.MainActivity }
Error type 3
Error: Activity class {com.arefin.mytime/com.arefin.mytime.MainActivity} does not exist.
Done in 98.22s.
arefin@arefin-HP-ProBook-450-G0:~/Programs/eazm__/Android_Integration_to_RN_Java$ 


```

# For tripzchat 

```java

> Task :app:installDebug
Installing APK 'app-debug.apk' on 'Redmi Note 7 - 10' for app:debug
Installed on 1 device.
w: Detected multiple Kotlin daemon sessions at build/kotlin/sessions

Deprecated Gradle features were used in this build, making it incompatible with Gradle 8.0.
Use '--warning-mode all' to show the individual deprecation warnings.
See https://docs.gradle.org/7.0.2/userguide/command_line_interface.html#sec:command_line_warnings

Execution optimizations have been disabled for 9 invalid unit(s) of work during this build to ensure correctness.
Please consult deprecation warnings for more details.

BUILD SUCCESSFUL in 2m 3s
483 actionable tasks: 479 executed, 4 up-to-date
info Connecting to the development server...
8081
info Starting the app on "68efca1a"...
Starting: Intent { cmp=com.byvl.tripzchat/.MainActivity }
Done in 131.77s.
arefin@arefin-HP-ProBook-450-G0:~/Programs/byvl/tripzChatHook$ 


```

```java



arefin@arefin-HP-ProBook-450-G0:~/Programs/byvl/tripzChatHook$ cd android
## arefin@arefin-HP-ProBook-450-G0:~/Programs/byvl/tripzChatHook/android$ grep -inrIH ".MainActivity"
app/src/main/java/com/tripzchat/MainActivity.java:13:public class MainActivity extends ReactActivity {
app/src/main/java/com/tripzchat/MainActivity.java:30:      return new RNGestureHandlerEnabledRootView(MainActivity.this);
app/src/main/java/com/tripzchat/MainActivity.java:36:// android/app/.../MainActivity.java
app/src/main/AndroidManifest.xml:35:                android:name=".MainActivity"
arefin@arefin-HP-ProBook-450-G0:~/Programs/byvl/tripzChatHook/android$ 


app/src/main/java/com/arefin/mytime/MyReactActivity.java:8:import com.arefin.mytime.MainActivity;
app/src/main/java/com/arefin/mytime/MainActivity.java:24:public class MainActivity extends AppCompatActivity {
app/src/main/res/layout/app_bar_main.xml:7:    tools:context=".MainActivity">
app/src/main/AndroidManifest.xml:28:        <!-- android:name=".MainActivity"
arefin@arefin-HP-ProBook-450-G0:~/Programs/eazm__/Android_Integration_to_RN_Java/android$ 






```