# Copyright 2016 Husky Team
# 
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
# 
# http://www.apache.org/licenses/LICENSE-2.0
# 
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.


include_directories(${PROJECT_SOURCE_DIR} ${HUSKY_EXTERNAL_INCLUDE})

add_subdirectory(input)
add_subdirectory(output)

add_library(hdfs-objs OBJECT hdfs_manager.cpp)
husky_default_properties(hdfs-objs)

# Combine io_objs
set(io-objs $<TARGET_OBJECTS:hdfs-objs> $<TARGET_OBJECTS:input-objs> $<TARGET_OBJECTS:output-objs>)

# Visible to parent directory
set(io-objs ${io-objs} PARENT_SCOPE)

add_library(husky-io STATIC ${io-objs})
