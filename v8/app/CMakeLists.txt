cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall")

add_library( v8_base STATIC IMPORTED )
set_target_properties( v8_base PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/libs/${ANDROID_ABI}/libv8_base.a )

add_library( v8_nosnapshot STATIC IMPORTED )
set_target_properties( v8_nosnapshot PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/libs/${ANDROID_ABI}/libv8_nosnapshot.a )

add_library( j2v8 SHARED src/main/cpp/com_eclipsesource_v8_V8Impl.cpp )
target_include_directories( j2v8 PRIVATE ${CMAKE_SOURCE_DIR}/libs/include )

target_link_libraries( j2v8 v8_base v8_nosnapshot log )