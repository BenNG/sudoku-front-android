cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_VERBOSE_MAKEFILE on)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++14")
set(CMAKE_BUILD_TYPE "Debug")
set(WITH_OPENCL ON)

set(pathToSudokuLib ../sudoku-recognizer/src/lib) # relative path from the CMakeLists.txt file in app
set(pathToProject /keep/Repo/moulinet-sudoku-front-android)
set(pathToOpenCv /keep/Software/opencv_devlopment_software/opencv-build-android/OpenCV-android-sdk)

include_directories( ${pathToOpenCv}/sdk/native/jni/include )

add_library( lib_opencv SHARED IMPORTED )
add_library( lib_sudoku SHARED IMPORTED )

add_library( native-lib SHARED src/main/cpp/native-lib.cpp ${pathToSudokuLib}/sudoku.cpp )

set_target_properties(lib_opencv PROPERTIES IMPORTED_LOCATION ${pathToProject}/app/src/main/jniLibs/${ANDROID_ABI}/libopencv_java3.so)

find_library( log-lib log )
target_link_libraries( native-lib ${log-lib} lib_opencv android)
