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

## ROS 한줄 설치 
* Ubuntu 버전에 따라서 지원하는 ROS 버전이 다르다 .
> * Ubuntu 16.04 -> ROS Kinetic, Ubuntu 18.04 -> ROS Melodic, Ubuntu20.04 -> ROS Noetic
* 환경 : Ubuntu 18.04 
* ROS 한줄 설치 
```
$ wget https://raw.githubusercontent.com/orocapangyo/meetup/master/190830/install_ros_melodic.sh && chmod 755 ./install_ros_melodic.sh && bash ./install_ros_melodic.sh
```
* home/사용자계정이름에 가보면 catkin_ws 폴더와 install_ros_melodic.sh 가 추가되어 있다. 
* .bashrc를 열어보면 단축키 설정 및 환경변수 설정 및 네트워크 설정이 자동으로 되어있다.
* 설치과정에서 필요한 환경설정을 자동으로 해주긴 하지만 시스템에는 따로 반영시켜야 한다.
```
$ source .bashrc
```

## ROS 동작 테스트 
* turtlesim 패키지 
```
$ roscore
$ rosrun turtlesim turtlesim_node
$ rosrun turtlesim turtle_teleop_key
$ rqt_graph
```
