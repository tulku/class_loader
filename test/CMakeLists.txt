cmake_minimum_required(VERSION 2.8)

find_package(Boost REQUIRED COMPONENTS thread)
find_package(catkin REQUIRED COMPONENTS class_loader)

include_directories(${catkin_INCLUDE_DIRS})

add_library(${PROJECT_NAME}_TestPlugins1 EXCLUDE_FROM_ALL plugins1.cpp)
target_link_libraries(${PROJECT_NAME}_TestPlugins1 ${PROJECT_NAME})
class_loader_hide_library_symbols(${PROJECT_NAME}_TestPlugins1)
add_library(${PROJECT_NAME}_TestPlugins2 EXCLUDE_FROM_ALL plugins2.cpp)
target_link_libraries(${PROJECT_NAME}_TestPlugins2 ${PROJECT_NAME})
class_loader_hide_library_symbols(${PROJECT_NAME}_TestPlugins2)

catkin_add_gtest(${PROJECT_NAME}_utest utest.cpp)
target_link_libraries(${PROJECT_NAME}_utest ${Boost_LIBRARIES} ${class_loader_LIBRARIES})
add_dependencies(${PROJECT_NAME}_utest ${PROJECT_NAME}_TestPlugins1 ${PROJECT_NAME}_TestPlugins2)
