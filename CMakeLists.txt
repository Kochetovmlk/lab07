cmake_minimum_required(VERSION 3.2) 
 
project (project_hw) 
 
add_executable(hello_world_app 
    hello_world.cpp ) 
 
install(TARGETS hello_world_app hello_world_app RUNTIME DESTINATION /bin)
