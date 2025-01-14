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
