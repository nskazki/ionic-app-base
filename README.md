# Example project for issue 

[cordova-plugin-google-analytics](https://github.com/danwilson/google-analytics-plugin) conflict with [AppsFlyerSDK/PhoneGap](https://github.com/AppsFlyerSDK/PhoneGap/tree/310b91c30c643168e1144ea7dd0153a790b476b3)  

```diff
-  }
+  },
+  "cordovaPlugins": [
+    "cordova-plugin-google-analytics@~0.8.1",
+    {
+      "locator": "https://github.com/AppsFlyerSDK/PhoneGap.git#310b91c30c643168e1144ea7dd0153a790b476b3"
+    }
+  ],
+  "cordovaPlatforms": [
+    "android"
+  ]
 }
```

```
npm i
ionic state restore
ionic build android
```

```
Running command: /home/nskazki/node.js/claritasmind-work-projects/ionic-app-base/hooks/after_prepare/010_add_platform_class.js /home/nskazki/node.js/claritasmind-work-projects/ionic-app-base
add to body class: platform-android
ANDROID_HOME=/home/nskazki/.apps/android-sdk-linux
JAVA_HOME=/home/nskazki/.apps/jdk1.7.0_79

...
...
...

:compileDebugNdk UP-TO-DATE
:compileDebugSources UP-TO-DATE
:transformClassesWithDexForDebug
UNEXPECTED TOP-LEVEL EXCEPTION:
com.android.dex.DexException: Multiple dex files define Lcom/google/android/gms/ads/identifier/AdvertisingIdClient$Info;
    at com.android.dx.merge.DexMerger.readSortableTypes(DexMerger.java:579)
    at com.android.dx.merge.DexMerger.getSortedTypes(DexMerger.java:535)
    at com.android.dx.merge.DexMerger.mergeClassDefs(DexMerger.java:517)
    at com.android.dx.merge.DexMerger.mergeDexes(DexMerger.java:164)
    at com.android.dx.merge.DexMerger.merge(DexMerger.java:188)
    at com.android.dx.command.dexer.Main.mergeLibraryDexBuffers(Main.java:504)
    at com.android.dx.command.dexer.Main.runMonoDex(Main.java:334)
    at com.android.dx.command.dexer.Main.run(Main.java:277)
    at com.android.dx.command.dexer.Main.main(Main.java:245)
    at com.android.dx.command.Main.main(Main.java:106)


 FAILED

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':transformClassesWithDexForDebug'.
> com.android.build.api.transform.TransformException: com.android.ide.common.process.ProcessException: org.gradle.process.internal.ExecException: Process 'command '/home/nskazki/Загрузки/jdk1.7.0_79/bin/java'' finished with non-zero exit value 2

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output.

BUILD FAILED

Total time: 34.011 secs
Error: Error code 1 for command: /home/nskazki/node.js/claritasmind-work-projects/ionic-app-base/platforms/android/gradlew with args: cdvBuildDebug,-b,/home/nskazki/node.js/claritasmind-work-projects/ionic-app-base/platforms/android/build.gradle,-Dorg.gradle.daemon=true,-Pandroid.useDeprecatedNdk=true
```

# Notes

It's not a [>65k methods problem](https://developer.android.com/intl/ko/tools/building/multidex.html)
Because: 

 * build only with `cordova-plugin-google-analytics` contains 17616 methods.
 * build only with `AppsFlyerSDK` contains 21514 methods
 * build without plugins contains 1064 methods

# Related issues 

 * https://github.com/kraihn/cordova-plugin-tag-manager/issues/19
