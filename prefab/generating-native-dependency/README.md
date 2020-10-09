# Generating Native Dependency AAR

This sample shows how to export native libraries in an AAR
using the [Prefab] format. The sample builds a trivial library called `mylibrary` (libmylibrary.so),
packs it into a native depdency AAR. From here you could distribute the AAR via Maven center or other ways.
Refer to the sample using-native-dependency sample for how to use the generated dependency AAR.

To export native libraries in an AAR with Android Gradle Plugin 4.1+, make the
following changes to your Android Library project's [build.gradle]:

* Enable the `prefabPublishing` build feature
```
    android.buildFeatures.prefabPublising true
```

* Declare the libraries and headers you wish to export in the `android.prefab`
  block
```
    android.prefab.mylibrary {
        headers "src/main/cpp/include"
    }
```
[Prefab]:https://google.github.io/prefab/
[build.gradle]:https://github.com/android/ndk-samples/blob/master/prefab/prefab-publishing/mylibrary/build.gradle#L64

* (Optional)If the exported native modules are NOT used by local Kotlin/Java modules in this AAR,
  avoid the exported libs get duplicated inside AAR to optimize the AAR download time 
```
    packagingOptions {
        exclude("**/libmylibrary.so")
        exclude("**/libc++_shared.so")
    }
```
Refer to [the official native dependency documentation](https://developer.android.com/studio/build/native-dependencies?buildsystem=cmake&agpversion=4.1) for details.
 
## Pre-requisites

* Android Gradle Plugin 4.1+
* The [Android NDK](https://developer.android.com/ndk/).

## Getting Started

The C++ code in this sample is built with CMake, but the concepts demonstrated
here work identically when using ndk-build.

To build:

1. Navigate to this directory in your terminal.
2. Run `./gradlew build` (or `gradlew.bat build` on Windows).

Note that there is no runnable application in this sample. The output is the
AAR.

## Support

If you've found an error in these samples, please [file an
issue](https://github.com/android/ndk-samples/issues/new).

Patches are encouraged, and may be submitted by submitting a pull request
through GitHub. Please see [CONTRIBUTING.md](../../CONTRIBUTING.md) for more
details.
