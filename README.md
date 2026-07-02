# apache-commons-codec-shaded
This is a "shaded" version of [Apache Commons Codec](https://commons.apache.org/codec) for use by Android app developers.

## The problem
Android includes an outdated version (v1.3) of commons-codec as an internal library. This library is not exposed in the Android SDK so app developers who want to rely on commons-codec need to treat it as an addition dependency and include it in the APK of their app. However, at runtime Android will always favour its internal version of the library which causes trouble when app code tries to call methods that don't exist in v1.3 but do exist in the version the developer expected to be using.

## The solution
Build your Android application with this "shaded" version of the commons-codec, which can be produced by running the gradle build script in this repository. In the resulting `jar` file the commons-codec package has been renamed from `org.apache.commons.codec` to `shaded.org.apache.commons.codec`, thereby avoiding the clash with Android's built-in version of commons-codec.

## How does it work?
The `build.gradle` file fetches the latest version of commons-codec (currently 1.11), applies the package relocation (using johnrengelman's [Gradle Shadow plug-in](https://github.com/johnrengelman/shadow)) and installs the resulting `jar` to the local Maven repository.

## How do I use this in my app project?
### Hand-built
 - Download or clone this repository
 - Run `gradle` in the root directory. This will install `commons-codec-shaded` to your local Maven repository.
 - In the `build.gradle` file of your own project, add `mavenLocal()` to the `repositories` and add `compile 'commons-codec:commons-codec-shaded:1.10'` to the `dependencies`.

### JitPack
Alternatively you can do all of this in one step by relying on [JitPack.io](https://jitpack.io):
 - In your `build.gradle` file, add `maven { url 'https://jitpack.io' }` to the list of `repositories` and add `compile 'com.github.ExCiteS:apache-commons-codec-shaded:1.11'` to the `dependencies`.


## Credits
By [Matthias Stevens](https://github.com/mstevens83) for UCL ExCiteS.
