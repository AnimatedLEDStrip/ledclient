#  Copyright (c) 2020 AnimatedLEDStrip
#
#  of this software and associated documentation files (the "Software"), to deal
#  in the Software without restriction, including without limitation the rights
#  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
#  copies of the Software, and to permit persons to whom the Software is
#  furnished to do so, subject to the following conditions:
#
#  The above copyright notice and this permission notice shall be included in
#  all copies or substantial portions of the Software.
#
#  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
#  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
#  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
#  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
#  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
#  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
#  THE SOFTWARE.

cmake_minimum_required(VERSION 3.10)
project(ledclient)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(THREADS_PREFER_PTHREAD_FLAG_ON)

set(CMAKE_CXX_FLAGS="-g -O0 -Wall -fprofile-arcs -ftest-coverage")
set(CMAKE_EXE_LINKER_FLAGS="-lgcov")
find_package(Threads REQUIRED)

set(ALS_SRC_DIR ${CMAKE_CURRENT_SOURCE_DIR}/animatedledstrip)
file(DOWNLOAD https://github.com/animatedledstrip/client-cpp/raw/master/src/AnimationData.hpp ${ALS_SRC_DIR}/AnimationData.hpp)
file(DOWNLOAD https://github.com/animatedledstrip/client-cpp/raw/master/src/AnimationInfo.hpp ${ALS_SRC_DIR}/AnimationInfo.hpp)
file(DOWNLOAD https://github.com/animatedledstrip/client-cpp/raw/master/src/AnimationSender.hpp ${ALS_SRC_DIR}/AnimationSender.hpp)
file(DOWNLOAD https://github.com/animatedledstrip/client-cpp/raw/master/src/ColorContainer.hpp ${ALS_SRC_DIR}/ColorContainer.hpp)
file(DOWNLOAD https://github.com/animatedledstrip/client-cpp/raw/master/src/EndAnimation.hpp ${ALS_SRC_DIR}/EndAnimation.hpp)
file(DOWNLOAD https://github.com/animatedledstrip/client-cpp/raw/master/src/Section.hpp ${ALS_SRC_DIR}/Section.hpp)
file(DOWNLOAD https://github.com/animatedledstrip/client-cpp/raw/master/src/StripInfo.hpp ${ALS_SRC_DIR}/StripInfo.hpp)

set(JSON_VERSION v3.7.3)
set(JSON_SRC_DIR ${CMAKE_CURRENT_SOURCE_DIR}/nlohmann)
set(JSON_HEADER ${JSON_SRC_DIR}/json.hpp)
file(DOWNLOAD https://github.com/nlohmann/json/releases/download/${JSON_VERSION}/json.hpp ${JSON_HEADER})

set(SAFE_MAP_DIR ${CMAKE_CURRENT_SOURCE_DIR}/safe-map)
file(DOWNLOAD https://github.com/KarenRei/safe-map/raw/master/safemap.h ${SAFE_MAP_DIR}/safemap.h)
file(DOWNLOAD https://github.com/KarenRei/safe-map/raw/master/number.h ${SAFE_MAP_DIR}/number.h)
set_source_files_properties(${CMAKE_CURRENT_SOURCE_DIR}/safe-map PROPERTIES COMPILE_FLAGS "-w")

add_executable(ledclient main.cpp)
target_include_directories(ledclient PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_link_libraries(ledclient PUBLIC Threads::Threads)
