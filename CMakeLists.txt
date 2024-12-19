# Copyright (c) 2024 LuckkMaker
# All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

set(LUA_CFG_SOURCE_FILE ${CMAKE_CURRENT_LIST_DIR}/src/luaconf_template.h)
set(LUA_RTT_CFG_TARGET_FILE ${OMNI_LUA_CFG_DIR}/luaconf.h)
omni_add_configure_file(${LUA_CFG_SOURCE_FILE} ${LUA_RTT_CFG_TARGET_FILE})

add_library(omni-lua INTERFACE)

file(GLOB OMNI_LUA_SOURCES
    "src/*.c"
)

list(REMOVE_ITEM OMNI_LUA_SOURCES
    ${CMAKE_CURRENT_LIST_DIR}/src/lua.c
    ${CMAKE_CURRENT_LIST_DIR}/src/luac.c
)

target_sources(omni-lua INTERFACE
    ${OMNI_LUA_SOURCES}
)

target_include_directories(omni-lua INTERFACE
    src
)
