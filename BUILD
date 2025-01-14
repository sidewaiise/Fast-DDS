load("@rules_foreign_cc//foreign_cc:defs.bzl", "cmake")

package(default_visibility = ["//visibility:public"])

licenses(["notice"])

filegroup(
    name = "fastdds_srcs",
    srcs = glob(
        ["**"],
        exclude = [
            "bazel-bin/**",
            "bazel-Fast-DDS/**",
            "bazel-out/**",
            "bazel-testlogs/**",
            "bazel-qnx/**",
            "*.log"
        ]),
    visibility = ["//visibility:public"],
)

cmake(
    name = "fastdds",
    cache_entries = {
        "CMAKE_C_FLAGS": "-fPIC",
        "COMPILE_TOOLS": "OFF",
        "BUILD_SHARED_LIBS": "OFF"
    },
    lib_source = "//:fastdds_srcs",
    out_static_libs = select({
        "@bazel_tools//src/conditions:linux": [
            "libfastdds.a"
        ],
        "@bazel_tools//src/conditions:linux_x86_64": [
            "libfastdds.a"
        ],
        "@bazel_tools//src/conditions:darwin": [
            "libfastdds.a"
        ],
        "//conditions:default": [],
    }),
    deps = [
        "@fastcdr//:fastcdr",
        "@asio//:asio",
        "@tinyxml2//:tinyxml2",
        "@openssl//:openssl",
        "@foonathan_memory//:foonathan_memory"
    ]
)

# cmake_configure_file(
#     name = "configure_file",
#     src = "include/fastdds/config.hpp.in",
#     out = "include/fastdds/config.hpp",
#     cmakelists = [
#        "CMakeLists.txt",
#     ],
#     defines = [
#         "HAVE_CXX17",
#         "FASTDDS_IS_BIG_ENDIAN_TARGET=1",
#         "HAVE_SECURITY=0",
#         "HAVE_STRICT_REALTIME=1",
#         "HAVE_SQLITE3=0",
#         "ENABLE_OLD_LOG_MACROS_=1",
#         "HAVE_LOG_NO_ERROR=1",
#         "HAVE_LOG_NO_INFO=1",
#         "HAVE_LOG_NO_WARNING=1",
#         "TLS_FOUND=0",
#         "PROJECT_VERSION_MAJOR=3",
#         "PROJECT_VERSION_MINOR=1",
#         "PROJECT_VERSION_PATCH=0",
#         "PROJECT_VERSION=3.1.0"
#     ],
#     undefines = [
#         "HAVE_CXX20",
#         "HAVE_CXX14",
#         "HAVE_CXX1Y",
#         "HAVE_CXX11",
#     ],
#     visibility = ["//visibility:private"],
# )

# genrule(
#     name = "fastdds",
#     srcs = glob(["**/*.*"]) + [":configure_file"],
#     outs = ["fastdds"],
#     cmd = "ls -lah && mkdir build && cd build && cmake .. && cmake . --build && ls -lah",
#     tools = [
#         "@fastcdr//:fastcdr"
#         # "@foonathan_memory",
#         # "@tinyxml2",
#         # "@asio//:asio"
#     ]
# )

# cc_library(
#     name = "fastdds",
#     hdrs = glob([
#         "include/**/*.h",
#         "include/**/*.hpp",
#         "include/**/*.ipp",
#         "src/cpp/**/*.h",
#         "src/cpp/**/*.hpp",
#         "src/cpp/**/*.ipp",
#         "thirdparty/**/*.h",
#         "thirdparty/**/*.hpp",
#         "thirdparty/**/*.ipp"
#     ], allow_empty=True) + [
#         ":configure_file",
#     ],
#     srcs = glob([
#         "src/cpp/**/*.cpp",
#         "src/cpp/**/*.c"
#     ], allow_empty=True),
#     includes = [
#         "include",
#         "src/cpp",
#         "thirdparty",
#         "thirdparty/filewatch",
#         "thirdparty/nlohmann-json",
#         "thirdparty/boost/include",
#         "thirdparty/taocpp-pegtl",
#         "thirdparty/taocpp-pegtl/pegtl",
#         "thirdparty/taocpp-pegtl/pegtl/contrib",
#         "thirdparty/taocpp-pegtl/pegtl/internal"
#     ],
#     deps = [
#         "@fastcdr//:fastcdr",
#         "@foonathan_memory",
#         "@tinyxml2",
#         "@asio//:asio"
#     ]
# )
