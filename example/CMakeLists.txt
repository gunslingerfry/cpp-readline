#    /cpp-readline/example/CMakeLists.txt
#
#    @author zmij
#    @auther gunslingerfry
#    @date 2021

cmake_minimum_required(VERSION 3.10)

add_executable(cpp-readline-example main.cpp)
target_link_libraries(cpp-readline-example
    PRIVATE
        cpp-readline::cpp-readline
)
