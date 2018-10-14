#  Installation Process in mac machine

- Download Flutter.
    - Get the latest flutter build from [archive page](https://flutter.io/sdk-archive/#macos).
    - Download the latest build from the archive page.
    - Unzip the flutter file.
        - execute following command :
        ```
            $ cd ~/development
            $ unzip ~/Downloads/flutter_macos_v0.9.4-beta.zip
        ```
        - Add the flutter tool to your path:
        ```
            $ export PATH=`pwd`/flutter/bin:$PATH
        ```
- Run flutter doctor
    ```
        $ flutter doctor
    ```
    - If you get error like this : ✗ Unable to locate Android SDK.
        - This might mean that that the Android Studio is not installed. See the process of Android Studio installation below.




- Download Android Studio.
    - Download the latest android studio from this [link](https://developer.android.com/studio/index.html).

- Download Xcode.
    - Download the lastest Xcode from this [link](https://developer.apple.com/xcode/).
    - if flutter doctor gives error :
        - libimobiledevice and ideviceinstaller are not installed. 
            - To install, run:
            ```
                brew install --HEAD libimobiledevice
                brew install ideviceinstaller
            ```
        - ios-deploy not installed.
            - To install, run:
            ```
                brew install ios-deploy
            ```
        

- Installing libimobiledevice.
    - While Executing this command :
    ```
        brew install --HEAD libimobiledevice
    ```
        - If you get an error like : 
        ```
            configure: error: Package requirements (libusbmuxd >= 1.1.0) were not met:
            Requested 'libusbmuxd >= 1.1.0' but version of libusbmuxd is 1.0.10
        ```
            To fix this, run following commands:
            ```
                brew update
                brew uninstall --ignore-dependencies libimobiledevice
                brew uninstall --ignore-dependencies usbmuxd
                brew install --HEAD usbmuxd
                brew unlink usbmuxd
                brew link usbmuxd
                brew install --HEAD libimobiledevice
            ```

- If you get this issue while running "flutter doctor" command that "Android licenses not accepted." To resolve this run following command :
    ```
        flutter doctor --android-licenses
    ```
    - Or you can go to the sdk folder : /Users/YOUR_MAC_USER/Library/Android/sdk/tools/bin   and run :
    ```
        ./sdkmanager --licenses
    ```
    - follow the instaructions and accept the licenses.