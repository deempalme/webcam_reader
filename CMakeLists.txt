#cmake version
cmake_minimum_required(VERSION 3.5...3.15)

if(NOT TARGET ${RamRodWebcamReader_LIBRARIES})
  project(RamRodWebcamReader
    VERSION 1.0.0
    DESCRIPTION "Ram-Rod's Webcam reader library"
    LANGUAGES CXX C
  )

  set(${PROJECT_NAME}_INCLUDE_DIRS
    ${PROJECT_SOURCE_DIR}/include
    CACHE INTERNAL ""
  )

  set(${PROJECT_NAME}_LIBRARIES
    ${PROJECT_NAME}
    CACHE INTERNAL ""
  )

  #add every file to the executable
  add_library(${PROJECT_NAME})

  target_sources(${PROJECT_NAME}
    PRIVATE
    include/ramrod/webcam/constants.h
    include/ramrod/webcam/enumerators.h
    include/ramrod/webcam/types.h
    include/ramrod/webcam/webcam_player.h
    src/ramrod/webcam/webcam_player.cpp
  )

  target_compile_features(${PROJECT_NAME} PUBLIC cxx_std_17)

  set_target_properties(${PROJECT_NAME}
    PROPERTIES
      CXX_STANDARD 17
      CXX_STANDARD_REQUIRED ON
      CXX_EXTENSIONS OFF
  )

  target_include_directories(${PROJECT_NAME}
    PRIVATE
      include
  )

  #indicates which libraries to use in the executable
  target_link_libraries(${PROJECT_NAME}
  )

  if(CMAKE_BUILD_TYPE MATCHES Debug)
    # Allows the program to print in console/terminal detailed error's explanations
    target_compile_definitions(${PROJECT_NAME}
      PRIVATE
        VERBOSE=True
    )

    target_compile_options(${PROJECT_NAME}
      PRIVATE
      -Wall
      -Wextra
      -Wundef
      -pedantic
      -Wconversion
      -Wcast-align
      -Wfloat-equal
      -Wpointer-arith
      -Wsign-conversion
      -Wunreachable-code
      -Wunused-function
      -Wignored-qualifiers
    )
  endif(CMAKE_BUILD_TYPE MATCHES Debug)
endif(NOT TARGET ${RamRodWebcamReader_LIBRARIES})
