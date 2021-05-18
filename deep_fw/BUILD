load("//tensorflow/lite:build_def.bzl", "tflite_custom_c_library", "tflite_cc_shared_object")
load("//tensorflow/lite/delegates/flex:build_def.bzl", "tflite_flex_cc_library")

tflite_custom_c_library(
    name = "tflite_c_api",
)


tflite_flex_cc_library(
    name = "tflite_flex",
)


tflite_cc_shared_object(
    name = "deep_fw",
    # Until we have more granular symbol export for the C++ API on Windows,
    # export all symbols.
    linkopts = select({
        "//tensorflow:macos": [
            "-Wl,-exported_symbols_list,$(location //tensorflow/lite/delegates/flex:exported_symbols.lds)",
        ],
        "//tensorflow:windows": [],
        "//conditions:default": [
            "-Wl,-z,defs",
            "-Wl,--version-script,$(location //tensorflow/lite/delegates/flex:version_script.lds)",
        ],
    }),
    deps = [
        "tflite_flex",
        "tflite_c_api",
    ],
)
