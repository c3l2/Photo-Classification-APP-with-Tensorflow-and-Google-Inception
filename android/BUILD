# Description:
#   TensorFlow camera demo app for Android.

package(default_visibility = ["//visibility:public"])

licenses(["notice"])  # Apache 2.0

load("//tensorflow:tensorflow.bzl", "tf_copts")

exports_files(["LICENSE"])

cc_binary(
    name = "libtensorflow_demo.so",
    srcs = glob([
        "jni/**/*.cc",
        "jni/**/*.h",
    ]) + [],
    copts = tf_copts(),
    linkopts = [
        "-landroid",
        "-ljnigraphics",
        "-llog",
        "-lm",
        "-z defs",
        "-s",
        "-Wl,--icf=all",  # Identical Code Folding
        "-Wl,--exclude-libs,ALL",  # Exclude syms in all libs from auto export
    ],
    linkshared = 1,
    linkstatic = 1,
    tags = [
        "manual",
        "notap",
    ],
    deps = ["//tensorflow/core:android_tensorflow_lib"],
)

cc_binary(
    name = "libpthread.so",
    srcs = [],
    linkopts = ["-shared"],
    tags = [
        "manual",
        "notap"
    ],
)


cc_library(
    name = "tensorflow_native_libs",
    srcs = [":libtensorflow_demo.so",
            ":libpthread.so"],
    tags = [
        "manual",
        "notap",
    ],
)

android_binary(
    name = "tensorflow_demo",
    srcs = glob([
        "src/**/*.java",
    ]),
    assets = glob(["assets/**"]),
    assets_dir = "assets",
    custom_package = "org.tensorflow.demo",
    inline_constants = 1,
    manifest = "AndroidManifest.xml",
    resource_files = glob(["res/**"]),
    tags = [
        "manual",
        "notap",
    ],
    deps = [
        ":tensorflow_native_libs",
    ],
)

filegroup(
    name = "all_files",
    srcs = glob(
        ["**/*"],
        exclude = [
            "**/METADATA",
            "**/OWNERS",
            "bin/**",
            "gen/**",
        ],
    ),
    visibility = ["//tensorflow:__subpackages__"],
)

filegroup(
    name = "java_files",
    srcs = glob(["src/**/*.java"]),
)

filegroup(
    name = "jni_files",
    srcs = glob([
        "jni/**/*.cc",
        "jni/**/*.h",
    ]),
)

filegroup(
    name = "resource_files",
    srcs = glob(["res/**"]),
)

exports_files(["AndroidManifest.xml"])
