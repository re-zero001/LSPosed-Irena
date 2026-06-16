project(external)

if (ANDROID_ABI STREQUAL "riscv64")
	set(ANDROID_PLATFORM "android-35")
endif ()

macro(SET_OPTION option value)
    set(${option} ${value} CACHE INTERNAL "" FORCE)
endmacro()

SET_OPTION(DOBBY_GENERATE_SHARED OFF)
SET_OPTION(Plugin.SymbolResolver OFF)
SET_OPTION(FMT_INSTALL OFF)

set(LIBCXX_SOURCES
        algorithm.cpp
#        any.cpp
        atomic.cpp
        barrier.cpp
#        bind.cpp
        charconv.cpp
        chrono.cpp
        condition_variable.cpp
        condition_variable_destructor.cpp
#        debug.cpp
        exception.cpp
#        filesystem/directory_iterator.cpp
#        filesystem/int128_builtins.cpp
#        filesystem/operations.cpp
        functional.cpp
        future.cpp
        hash.cpp
#        ios.cpp
#        ios.instantiations.cpp
#        iostream.cpp
#        locale.cpp
        memory.cpp
        mutex.cpp
        mutex_destructor.cpp
        new.cpp
        optional.cpp
        random.cpp
#        regex.cpp
#        ryu/d2fixed.cpp
#        ryu/d2s.cpp
#        ryu/f2s.cpp
        shared_mutex.cpp
        stdexcept.cpp
        string.cpp
#        strstream.cpp
        system_error.cpp
        thread.cpp
#        typeinfo.cpp
        utility.cpp
        valarray.cpp
        variant.cpp
        vector.cpp
        )

list(TRANSFORM LIBCXX_SOURCES PREPEND cxx/src/)

set(LIBCXX_EXPORT_FLAGS
        -DLIBCXX_BUILDING_LIBCXXABI
        -D_LIBCPP_NO_EXCEPTIONS
        -D_LIBCPP_NO_RTTI
        -D_LIBCPP_BUILDING_LIBRARY
        -D_LIBCPP_DISABLE_VISIBILITY_ANNOTATIONS
        -D_LIBCXXABI_NO_EXCEPTIONS
        -D_LIBCPP_HAS_NO_LOCALIZATION
        )
set(LIBCXX_FLAGS
        -fvisibility-global-new-delete=force-hidden
        -fvisibility=hidden
        -fvisibility-inlines-hidden
        )
set(LIBCXX_EXPORT_INCLUDES cxx/include)
set(LIBCXX_INCLUDES cxx/src)

set(LIBCXXABI_SOURCES
        abort_message.cpp
        cxa_aux_runtime.cpp
        cxa_default_handlers.cpp
        cxa_exception_storage.cpp
        cxa_guard.cpp
        cxa_handlers.cpp
        cxa_noexception.cpp
        cxa_thread_atexit.cpp
        cxa_vector.cpp
        cxa_virtual.cpp
        stdlib_exception.cpp
        stdlib_new_delete.cpp
        stdlib_stdexcept.cpp
        stdlib_typeinfo.cpp
        )
list(TRANSFORM LIBCXXABI_SOURCES PREPEND cxx/src/abi/)
set(LIBCXXABI_FLAGS
        -Wno-macro-redefined
        -Wno-unknown-attributes
        -DHAS_THREAD_LOCAL)
set(LIBCXXABI_INCLUDES cxx/include/abi)

add_library(cxx STATIC ${LIBCXX_SOURCES} ${LIBCXXABI_SOURCES})
target_compile_options(cxx PUBLIC ${LIBCXX_EXPORT_FLAGS})
target_compile_options(cxx PRIVATE ${LIBCXX_FLAGS} ${LIBCXXABI_FLAGS} -ffunction-sections -fdata-sections)
target_include_directories(cxx PUBLIC ${LIBCXX_EXPORT_INCLUDES})
target_include_directories(cxx PRIVATE ${LIBCXX_INCLUDES} ${LIBCXXABI_INCLUDES})

link_libraries(cxx)

set(SYSTEM_PROPERTIES_SOURCES
        context_node.cpp
        contexts_serialized.cpp
        contexts_split.cpp
        prop_area.cpp
        prop_info.cpp
        system_properties.cpp
        system_property_api.cpp
        system_property_set.cpp
        property_info_parser.cpp
)

list(TRANSFORM SYSTEM_PROPERTIES_SOURCES PREPEND system_properties/)

set(SYSTEM_PROPERTIES_FLAGS
        --std=c++17
        -Wno-unused-function
)
set(SYSTEM_PROPERTIES_INCLUDES system_properties/include)
set(SYSTEM_PROPERTIES_EXPORT_INCLUDES ${SYSTEM_PROPERTIES_INCLUDES})

add_library(system_properties STATIC ${SYSTEM_PROPERTIES_SOURCES})
target_compile_options(system_properties PRIVATE ${SYSTEM_PROPERTIES_FLAGS})
target_include_directories(system_properties PUBLIC ${SYSTEM_PROPERTIES_EXPORT_INCLUDES})
target_include_directories(system_properties PRIVATE ${SYSTEM_PROPERTIES_INCLUDES})

link_libraries(system_properties)

set(XZ_EMBEDDED_SOURCES
        xz/xz_crc32.c
        xz/xz_crc64.c
        xz/xz_dec_bcj.c
        xz/xz_dec_lzma2.c
        xz/xz_dec_stream.c
)

list(TRANSFORM XZ_EMBEDDED_SOURCES PREPEND xz-embedded/linux/lib/)

set(XZ_EMBEDDED_FLAGS
        -std=c89
        -DXZ_INTERNAL_CRC32=1
        -DXZ_USE_CRC64=1
        -DXZ_INTERNAL_CRC64=1
)
set(XZ_EMBEDDED_EXPORT_INCLUDES xz-embedded/linux/include/linux)
set(XZ_EMBEDDED_INCLUDES ${XZ_EMBEDDED_EXPORT_INCLUDES} xz-embedded/userspace)

add_library(xz_embedded STATIC ${XZ_EMBEDDED_SOURCES})
target_compile_options(xz_embedded PRIVATE)
target_include_directories(xz_embedded PUBLIC ${XZ_EMBEDDED_EXPORT_INCLUDES})
target_include_directories(xz_embedded PRIVATE ${XZ_EMBEDDED_INCLUDES})

link_libraries(xz_embedded)

OPTION(LSPLANT_BUILD_SHARED OFF)
add_subdirectory(lsplant/lsplant/src/main/jni)
if (ANDROID_ABI STREQUAL "riscv64")
	add_subdirectory(riscv64-inline-hook)
else ()
	add_subdirectory(dobby)
endif ()
add_subdirectory(fmt)
target_compile_definitions(fmt-header-only INTERFACE FMT_STATIC_THOUSANDS_SEPARATOR=1 FMT_USE_FLOAT=0 FMT_USE_DOUBLE=0 FMT_USE_LONG_DOUBLE=0)
