cmake_minimum_required(VERSION 3.23)

project(Hadrons VERSION 1.0)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

find_package(Geant4 REQUIRED)

foreach(dsname ${Geant4_DATASETS})            # Iterate over dataset names
    message("checking for ${dsname}")
  if(NOT EXISTS ${Geant4_DATASET_${dsname}_PATH})  # Check existence
    message(WARNING "${dsname} not located at ${Geant4_DATASET_${dsname}_PATH}")
  endif()
endforeach()

file(GLOB sources ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cc)
add_executable(HadronPhysics main.cpp ${sources})

target_include_directories(HadronPhysics
    PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include
)

target_link_libraries(HadronPhysics ${Geant4_LIBRARIES})
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
