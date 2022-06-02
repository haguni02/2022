## ROS Workspace 생성하는 방법
```
// 1. my_catkin_ws/src 폴더를 만든다 
$ mkdir -p ~/my_catkin_ws/src 
$ cd ~/my_catkin_ws
// 2. Workspace 초기화 
$ catkin_make 
```
* 새로운 catkin Workspace 가 만들어지고 build, devel 폴더가 만들어진다 
```
// ROS Workspace 사용 : Terminal 창을 열 때마다 실행 
$ source ~/my_catkin_ws/devel/setup.sh
```

## ROS Package 만들기 튜토리얼
```
$ cd ~/my_catkin_ws/src 
// TEST 패키지 생성
$ catkin_create_pkg TEST roscpp 
```
* ~/my_catkin_ws/src/TEST 폴더와 그 안에 CMakeLists.txt, package.xml 파일이 생성된다
```cpp
// ros1_node.cpp
#include <iostream>
 
int main(int argc, char **argv) //c++ 의 기본 함수형태
{
    std::cout << "~~~~ WELCOME TO ROS WORLD ~~~~~~" << std::endl; // Print 

    return 0;
}
```
* CMakeList.txt
```txt
cmake_minimum_required(VERSION 3.0.2)
project(TEST)

find_package(catkin REQUIRED COMPONENTS roscpp)



################################################
## Declare ROS messages, services and actions ##
################################################


################################################
## Declare ROS dynamic reconfigure parameters ##
################################################


###################################
## catkin specific configuration ##
###################################
catkin_package(

)

###########
## Build ##
###########

include_directories(
 include
 ${catkin_INCLUDE_DIRS}
)


add_executable(tmp src/ros1_node.cpp)
#target_link_libraries(tmp ${catkin_LIBRARIES}) # Libraries Link: 


#############
## Install ##
#############


#############
## Testing ##
#############
```
* package.xml
```xml
<?xml version="1.0"?>
<package format="2">
  <name>TEST</name>
  <version>0.0.0</version>
  <description>The TEST package</description>

  <maintainer email="test1804@todo.todo">test1804</maintainer>


  <license>TODO</license>

  <buildtool_depend>catkin</buildtool_depend>


  <!-- The export tag contains other, unspecified, tags -->
  <export>
    <!-- Other tools can request additional information be placed here -->

  </export>
</package>
```
* build 후에 실행하기 
```
$ cd ~/my_catkin_ws
$ catkin_make
// roscore 실행 후 실행 
$ rosrun TEST tmp
```
