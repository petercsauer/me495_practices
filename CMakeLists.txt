cmake_minimum_required(VERSION 3.0.8)
project(me495_practices)

find_package(catkin REQUIRED COMPONENTS message_generation)

add_message_files(
  FILES
  OneInt.msg
)

add_service_files(
   FILES
   TwoResult.srv
)

# use the setup.py to install python modules
catkin_python_setup()

generate_messages()


catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES practice
  CATKIN_DEPENDS message_runtime
#  DEPENDS system_lib
)

catkin_install_python(PROGRAMS
   nodes/add_numbers
   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
   )

#############
## Testing ##
#############


# Add rostest files
if (CATKIN_ENABLE_TESTING)
    find_package(rostest REQUIRED)
    add_rostest(test/client_test.test)
    ## Add folders to be run by python nosetests
    catkin_add_nosetests(test)
endif()
