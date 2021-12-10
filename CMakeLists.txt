cmake_minimum_required(VERSION 3.2)
project(resample)

# 先生成动态库
add_library(resample SHARED src/filterkit.c src/resample.c src/resamplesubs.c)
target_include_directories(resample PUBLIC ${PROJECT_SOURCE_DIR}/include)
target_include_directories(resample PRIVATE ${PROJECT_SOURCE_DIR}/src)


# 生成测试目标文件 仅仅使用target_include_directories保持以来关系清晰
add_executable(resamle_file tests/resample-sndfile.c)
target_include_directories(resamle_file PRIVATE ${PROJECT_SOURCE_DIR}/include)
target_include_directories(resamle_file PRIVATE ${PROJECT_SOURCE_DIR}/src)
target_link_libraries(resamle_file PRIVATE resample)
target_link_libraries(resamle_file PRIVATE sndfile)