cmake_minimum_required(VERSION 3.19)
project(GIVBH LANGUAGES CXX CUDA)
set(CMAKE_CXX_STANDARD 11)
# Set CUDA policy (if using CMake 3.19 or higher)
cmake_policy(SET CMP0146 NEW)
enable_language(CUDA)
set(CMAKE_CUDA_ARCHITECTURES  "80")
# example CMAKE_CUDA_ARCHITECTURES:"60;61;70;75;80"
# 50: Maxwell (e.g., GTX 750 Ti)
# 60: Pascal (e.g., GTX 1080)
# 70: Volta (e.g., Tesla V100)
# 75: Turing (e.g., RTX 2080)
# 80: Ampere (e.g., RTX 3080, RTX 3090)

find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})
find_package(GLEW REQUIRED)
find_package(OpenGL REQUIRED)
find_package(SDL2 REQUIRED)
find_package(glm REQUIRED)
include_directories(${CMAKE_CURRENT_SOURCE_DIR})



add_executable(${PROJECT_NAME} main.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/Camera/vCamera.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/Geometry/Mesh.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/Input/input.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/PixelBuffer/PixelBuffer.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/shaders/Shader.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/Silhouettes/frame.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/Silhouettes/ImageDataArrays.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/Texture/TextureGL.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/Transforms/transform.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/volume/volume.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/Window/Fps.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/Window/Display.cpp
        ${CMAKE_CURRENT_SOURCE_DIR}/cudaKernel/Findsilhouette.cu
        ${CMAKE_CURRENT_SOURCE_DIR}/cudaKernel/render.cu
)
target_link_libraries(${PROJECT_NAME} ${OpenCV_LIBS} ${CUDA_LIBRARIES} freeimage OpenGL::GL GLEW::GLEW SDL2::SDL2 glm::glm)