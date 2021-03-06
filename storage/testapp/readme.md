Firebase Storage Quickstart
========================

The Firebase Storage Test Application (testapp) demonstrates Firebase Storage
operations with the Firebase Storage C++ SDK. The application has no user
interface and simply logs actions it's performing to the console.

The testapp performs the following:
  - Creates a firebase::App in a platform-specific way. The App holds
    platform-specific context that's used by other Firebase APIs, and is a
    central point for communication between the Firebase Storage C++ and
    Firebase Auth C++ libraries.
  - Gets a pointer to firebase::Auth, and signs in anonymously. This allows the
    testapp to access a Firebase Storage instance with authentication rules
    enabled, which is the default setting in Firebase Console.
  - Gets a StorageReference to the root node's "test_app_data" child, uses
    StorageReference::Child() to create a child with a unique key based on the
    current time in microseconds to work in, and gets a reference to that child,
    which the testapp will use for the remainder of its actions.
  - Uploads some sample files and reads them back to ensure the storage can be
    read from and written to.
  - Checks the Metadata of the uploaded and downloaded files to ensure they
    return the expected values for things like size and date modified.
  - Disconnects and then reconnects and verifies it still has access to the
    files uploaded.
  - Shuts down the Firebase Storage, Firebase Auth, and Firebase App systems.

Introduction
------------

- [Read more about Firebase Storage](https://firebase.google.com/docs/storage/)

Building and Running the testapp
--------------------------------

### iOS
  - Link your iOS app to the Firebase libraries.
    - Get CocoaPods version 1 or later by running,
        ```
        $ sudo gem install CocoaPods --pre
        ```
    - From the testapp directory, install the CocoaPods listed in the Podfile
      by running,
        ```
        $ pod install
        ```
    - Open the generated Xcode workspace (which now has the CocoaPods),
        ```
        $ open testapp.xcworkspace
        ```
    - For further details please refer to the
      [general instructions for setting up an iOS app with Firebase](https://firebase.google.com/docs/ios/setup).
  - Register your iOS app with Firebase.
    - Create a new app on the [Firebase console](https://firebase.google.com/console/), and attach
      your iOS app to it.
      - You can use "com.google.firebase.cpp.storage.testapp" as the iOS Bundle
        ID while you're testing. You can omit App Store ID while testing.
    - Add the GoogleService-Info.plist that you downloaded from Firebase
      console to the testapp root directory. This file identifies your iOS app
      to the Firebase backend.
    - In the Firebase console for your app, select "Auth", then enable
      "Anonymous". This will allow the testapp to use anonymous sign-in to
      authenticate with Firebase Storage, which requires a signed-in user by
      default (an anonymous user will suffice).
  - Download the Firebase C++ SDK linked from
    https://firebase.google.com/docs/cpp/setup and unzip it to a
    directory of your choice.
  - Add the following frameworks from the Firebase C++ SDK to the project:
    - frameworks/ios/universal/firebase.framework
    - frameworks/ios/universal/firebase_auth.framework
    - frameworks/ios/universal/firebase_storage.framework
    - You will need to either,
       1. Check "Copy items if needed" when adding the frameworks, or
       2. Add the framework path in "Framework Search Paths"
          - e.g. If you downloaded the Firebase C++ SDK to
            `/Users/me/firebase_cpp_sdk`,
            then you would add the path
            `/Users/me/firebase_cpp_sdk/frameworks/ios/universal`.
          - To add the path, in XCode, select your project in the project
            navigator, then select your target in the main window.
            Select the "Build Settings" tab, and click "All" to see all
            the build settings. Scroll down to "Search Paths", and add
            your path to "Framework Search Paths".
  - In XCode, build & run the sample on an iOS device or simulator.
  - The testapp has no interative interface. The output of the app can be viewed
    via the console or on the device's display.  In Xcode, select
    "View --> Debug Area --> Activate Console" from the menu to view the console.

### Android
  - Register your Android app with Firebase.
    - Create a new app on
      the [Firebase console](https://firebase.google.com/console/), and attach
      your Android app to it.
      - You can use "com.google.firebase.cpp.storage.testapp" as the Package
        Name while you're testing.
      - To
        [generate a SHA1](https://developers.google.com/android/guides/client-auth)
        run this command on Mac and Linux,
        ```
        keytool -exportcert -list -v -alias androiddebugkey -keystore ~/.android/debug.keystore
        ```
        or this command on Windows,
        ```
        keytool -exportcert -list -v -alias androiddebugkey -keystore %USERPROFILE%\.android\debug.keystore
        ```
      - If keytool reports that you do not have a debug.keystore, you can
        [create one with](http://developer.android.com/tools/publishing/app-signing.html#signing-manually),
        ```
        keytool -genkey -v -keystore ~/.android/debug.keystore -storepass android -alias androiddebugkey -keypass android -dname "CN=Android Debug,O=Android,C=US"
        ```
    - Add the `google-services.json` file that you downloaded from Firebase
      console to the root directory of testapp. This file identifies your
      Android app to the Firebase backend.
    - In the Firebase console for your app, select "Auth", then enable
      "Anonymous". This will allow the testapp to use anonymous sign-in to
      authenticate with Firebase Storage, which requires a signed-in user by
      default (an anonymous user will suffice).
    - For further details please refer to the
      [general instructions for setting up an Android app with Firebase](https://firebase.google.com/docs/android/setup).
  - Download the Firebase C++ SDK linked from
    https://firebase.google.com/docs/cpp/setup and unzip it to a
    directory of your choice.
  - Configure the location of the Firebase C++ SDK by setting the
    firebase\_cpp\_sdk.dir Gradle property to the SDK install directory.
    For example, in the project directory:
      ```
      > echo "systemProp.firebase\_cpp\_sdk.dir=/User/$USER/firebase\_cpp\_sdk" >> gradle.properties
      ```
  - Ensure the Android SDK and NDK locations are set in Android Studio.
    - From the Android Studio launch menu, go to
      Configure/Project Defaults/Project Structure and download the SDK and NDK if
      the locations are not yet set.
  - Open *build.gradle* in Android Studio.
    - From the Android Studio launch menu, "Open an existing Android Studio
      project", and select `build.gradle`.
  - Install the SDK Platforms that Android Studio reports missing.
  - Build the testapp and run it on an Android device or emulator.
  - The testapp has no interactive interface. The output of the app can be
    viewed on the device's display, or in the logcat output of Android studio or
    by running "adb logcat *:W android_main firebase" from the command line.

Support
-------

https://firebase.google.com/support/

License
-------

Copyright 2016 Google, Inc.

Licensed to the Apache Software Foundation (ASF) under one or more contributor
license agreements.  See the NOTICE file distributed with this work for
additional information regarding copyright ownership.  The ASF licenses this
file to you under the Apache License, Version 2.0 (the "License"); you may not
use this file except in compliance with the License.  You may obtain a copy of
the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  See the
License for the specific language governing permissions and limitations under
the License.

