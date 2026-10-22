# Lua 5.4 构建入口（框架侧 glue，上游仓库保持原样）。
#
# 源文件清单与 modules/lua/lua.clayer.yml 一致：改这里就要同步改 clayer，
# 反之亦然（后续可用生成器统一，见 omni/cmake/README.md）。

add_library(omni_module_lua OBJECT
    "${OMNI_MODULE_LUA_SRC}/src/lapi.c"
    "${OMNI_MODULE_LUA_SRC}/src/lauxlib.c"
    "${OMNI_MODULE_LUA_SRC}/src/lbaselib.c"
    "${OMNI_MODULE_LUA_SRC}/src/lcode.c"
    "${OMNI_MODULE_LUA_SRC}/src/lcorolib.c"
    "${OMNI_MODULE_LUA_SRC}/src/lctype.c"
    "${OMNI_MODULE_LUA_SRC}/src/ldblib.c"
    "${OMNI_MODULE_LUA_SRC}/src/ldebug.c"
    "${OMNI_MODULE_LUA_SRC}/src/ldo.c"
    "${OMNI_MODULE_LUA_SRC}/src/ldump.c"
    "${OMNI_MODULE_LUA_SRC}/src/lfunc.c"
    "${OMNI_MODULE_LUA_SRC}/src/lgc.c"
    "${OMNI_MODULE_LUA_SRC}/src/linit.c"
    "${OMNI_MODULE_LUA_SRC}/src/liolib.c"
    "${OMNI_MODULE_LUA_SRC}/src/llex.c"
    "${OMNI_MODULE_LUA_SRC}/src/lmathlib.c"
    "${OMNI_MODULE_LUA_SRC}/src/lmem.c"
    "${OMNI_MODULE_LUA_SRC}/src/loadlib.c"
    "${OMNI_MODULE_LUA_SRC}/src/lobject.c"
    "${OMNI_MODULE_LUA_SRC}/src/lopcodes.c"
    "${OMNI_MODULE_LUA_SRC}/src/loslib.c"
    "${OMNI_MODULE_LUA_SRC}/src/lparser.c"
    "${OMNI_MODULE_LUA_SRC}/src/lstate.c"
    "${OMNI_MODULE_LUA_SRC}/src/lstring.c"
    "${OMNI_MODULE_LUA_SRC}/src/lstrlib.c"
    "${OMNI_MODULE_LUA_SRC}/src/ltable.c"
    "${OMNI_MODULE_LUA_SRC}/src/ltablib.c"
    "${OMNI_MODULE_LUA_SRC}/src/ltm.c"
    "${OMNI_MODULE_LUA_SRC}/src/lundump.c"
    "${OMNI_MODULE_LUA_SRC}/src/lutf8lib.c"
    "${OMNI_MODULE_LUA_SRC}/src/lvm.c"
    "${OMNI_MODULE_LUA_SRC}/src/lzio.c")

target_include_directories(omni_module_lua PUBLIC
    "${OMNI_MODULE_LUA_SRC}/src")
target_link_libraries(omni_module_lua PUBLIC
    omni::framework omni::config omni::hal)

omni_apply_arch(omni_module_lua)
omni_apply_warnings(omni_module_lua)
# 上游 Lua 源码的告警不作为本项目的质量门槛。
target_compile_options(omni_module_lua PRIVATE
    -Wno-nan-infinity-disabled)
