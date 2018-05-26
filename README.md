# RN Firebase install and config
#### npm install 
`npm install --save react-native-firebase`

create a project in **firebase** and download the **google-services.json** and keep it in `android/app`

>change the package name in google-services.json matching the project's package name
---
#### android/build.gradle
```
buildscript {
    repositories {
        jcenter()
        google()  // <-- Check this line exists
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.1.2' <-- the version should be
        classpath 'com.google.gms:google-services:3.2.1'
    } 
    
}

allprojects {
    repositories {
        mavenLocal()
        jcenter()
        maven {
            url "$rootDir/../node_modules/react-native/android"
	    }
        google()   // <-- Check this line exists 
    }
}
```
---
#### android/app/build.gradle 
>update all your **compile** statements to be **implementation**

add `apply plugin: 'com.google.gms.google-services'` at **very bottom of the file**
  
  `dependencies {`
  > // RNfirebase

   `implementation project(':react-native-firebase')`
>   // RNfirebase dependencies

   ```
   implementation "com.google.android.gms:play-services-base:15.0.0" 
   implementation "com.google.firebase:firebase-core:15.0.2"
   ```
   
  > //RNfirebase other plugin dependencies
  
  ```
implementation "com.google.firebase:firebase-ads:15.0.0"
implementation "com.google.firebase:firebase-auth:15.1.0"
implementation "com.google.firebase:firebase-config:15.0.0"
implementation "com.google.firebase:firebase-database:15.0.0"
implementation "com.google.firebase:firebase-invites:15.0.1"
implementation "com.google.firebase:firebase-firestore:16.0.0"
implementation "com.google.firebase:firebase-messaging:15.0.2"
implementation "com.google.firebase:firebase-perf:15.1.0"
implementation "com.google.firebase:firebase-storage:15.0.2" 
```
---
#### android/gradle/wrapper/gradle-wrapper.properties
  >update the gradle URL to gradle-4.4-all.zip
---
#### android/settings.gradle
```
//...
include ':react-native-firebase'
project(':react-native-firebase').projectDir =  new  File(rootProject.projectDir, '../node_modules/react-native-firebase/android')
include ':app'
```
---
#### android/app/src/main/java/com/.../MainApplication.java
>main package
```
import  io.invertase.firebase.RNFirebasePackage; 
``` 
>optional packages - add/remove as appropriate

```
import  io.invertase.firebase.admob.RNFirebaseAdMobPackage;  //Firebase AdMob
import  io.invertase.firebase.analytics.RNFirebaseAnalyticsPackage;  // Firebase Analytics
import  io.invertase.firebase.auth.RNFirebaseAuthPackage;  // Firebase Auth
import  io.invertase.firebase.config.RNFirebaseRemoteConfigPackage;  // Firebase Remote Config
import  io.invertase.firebase.database.RNFirebaseDatabasePackage;  // Firebase Realtime Database
import  io.invertase.firebase.firestore.RNFirebaseFirestorePackage;  // Firebase Firestore
import  io.invertase.firebase.instanceid.RNFirebaseInstanceIdPackage;  // Firebase Instance ID
import  io.invertase.firebase.links.RNFirebaseLinksPackage;  // Firebase Dynamic Links
import  io.invertase.firebase.messaging.RNFirebaseMessagingPackage;  // Firebase Cloud Messaging
import  io.invertase.firebase.notifications.RNFirebaseNotificationsPackage;  // Firebase Notifications
import  io.invertase.firebase.perf.RNFirebasePerformancePackage;  // Firebase Performance
import  io.invertase.firebase.storage.RNFirebaseStoragePackage;  // Firebase Storage
import  io.invertase.firebase.fabric.crashlytics.RNFirebaseCrashlyticsPackage;  // Crashlytics
```
```
@Override
protected  List<ReactPackage>  getPackages()  {
	return Arrays.<ReactPackage>asList(
		new MainReactPackage(),
		new RNFirebasePackage(), //main firebase package
```

>// add/remove these packages as appropriate

```
		new RNFirebaseAdMobPackage(),
		new RNFirebaseAnalyticsPackage(),
		new RNFirebaseAuthPackage(),
		new RNFirebaseCrashlyticsPackage(),
		new RNFirebaseDatabasePackage(),
		new RNFirebaseFirestorePackage(),
		new RNFirebaseInstanceIdPackage(),
		new RNFirebaseLinksPackage(),
		new RNFirebaseMessagingPackage(),
		new RNFirebaseNotificationsPackage(),
		new RNFirebasePerformancePackage(),
		new RNFirebaseRemoteConfigPackage(),
		new RNFirebaseStoragePackage()
	);
}
```

---
#### import
`import firebase from 'react-native-firebase'`
