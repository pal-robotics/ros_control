cmake_minimum_required(VERSION 2.8.3)
project(joint_limits_interface)

  find_package(urdfdom REQUIRED)

  find_package(catkin REQUIRED COMPONENTS
    roscpp
    rostest
    hardware_interface    
  )

  include_directories(
    SYSTEM 
    include
    ${catkin_INCLUDE_DIRS}
    ${urdfdom_INCLUDE_DIRS}
  )

  # Declare catkin package
  catkin_package(
    CATKIN_DEPENDS 
      roscpp
      hardware_interface
    INCLUDE_DIRS
      include
    DEPENDS
        urdfdom
  )

  if(CATKIN_ENABLE_TESTING)
    catkin_add_gtest(joint_limits_interface_test test/joint_limits_interface_test.cpp)
    target_link_libraries(joint_limits_interface_test ${catkin_LIBRARIES})

    catkin_add_gtest(joint_limits_urdf_test      test/joint_limits_urdf_test.cpp)
    target_link_libraries(joint_limits_urdf_test ${catkin_LIBRARIES})

    catkin_add_gtest(joint_limits_rosparam_test  test/joint_limits_urdf_test.cpp)
    target_link_libraries(joint_limits_rosparam_test ${catkin_LIBRARIES})

    add_rostest(test/joint_limits_rosparam.test)
  endif()

  # Install
  install(DIRECTORY include/${PROJECT_NAME}/
    DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION})

