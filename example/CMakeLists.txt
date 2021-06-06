cmake_minimum_required(VERSION 3.3 FATAL_ERROR)
add_executable(example example.cpp)

find_package(TensorflowCC REQUIRED)
target_link_libraries(example TensorflowCC::TensorflowCC)

TARGET_LINK_LIBRARIES(example /usr/local/lib/libtensorflow_cc.so) # the final compiled binary demands libtensorflow_cc.so.2 for some reason. creating a symlink of the file "/usr/local/lib/libtensorflow_cc.so." with the linked filename "/usr/local/lib/libtensorflow_cc.so.2" seems to be a quick fix solution

# link cuda if it is available
find_package(CUDA)
if(CUDA_FOUND)
  target_link_libraries(example ${CUDA_LIBRARIES})
endif()
