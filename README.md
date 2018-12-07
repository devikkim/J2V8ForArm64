# J2V8ForArm64
This repository is extension of J2V8 for support architecture arm64 

go -> [Complie V8 for Android](https://github.com/leibniz55/ComplieV8ForAndroid/blob/master/README.md)

go -> [j2v8](https://github.com/eclipsesource/J2V8)

1. import `include`, `armeabi-v7a`, `arm64-v8a`, `x86`, `include` folder
```
app
-- libs
   -- arm64-v8a
   -- armeabi-v7a
   -- x86
   -- include
```

2. edit CMakeLists.txt file
```
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall")

#import libv8_base.a
add_library( v8_base STATIC IMPORTED )
set_target_properties( v8_base PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/libs/${ANDROID_ABI}/libv8_base.a )

#import libv8_nosnapshot.a
add_library( v8_nosnapshot STATIC IMPORTED )
set_target_properties( v8_nosnapshot PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/libs/${ANDROID_ABI}/libv8_nosnapshot.a )

add_library( j2v8 SHARED src/main/cpp/com_eclipsesource_v8_V8Impl.cpp )
target_include_directories( j2v8 PRIVATE ${CMAKE_SOURCE_DIR}/libs/include )

target_link_libraries( j2v8 v8_base v8_nosnapshot log )
```

3. add cmake option in build.gragle
```
cmake {
    cppFlags "-std=c++11 -frtti -fexceptions"
    abiFilters 'x86', 'armeabi-v7a', 'arm64-v8a'
    arguments "-DANDROID_UNIFIED_HEADERS=ON"
}
```
