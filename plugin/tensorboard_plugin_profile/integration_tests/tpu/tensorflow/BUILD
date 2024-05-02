load("@org_xprof//plugin/tensorboard_plugin_profile/build_utils:profiler_test.bzl", "profiler_test")
load("//plugin/tensorboard_plugin_profile/build_utils:strict.default.bzl", "py_strict_library", "py_strict_test")
load("@python_deps//:requirements.bzl", "requirement")

# NOTE: need blaze test --define='with_tpu_support=true' for these tests.
profiler_test(
    name = "tpu_tf2_keras_xla_test",
    srcs = ["tpu_tf2_keras_test.py"],
    main = "tpu_tf2_keras_test.py",
    platforms = [
        "v2",
        "v3",
        "v4",
    ],
    deps = [
	    "@org_tensorflow//tensorflow/python/profiler/internal:_pywrap_profiler",
	"//plugin/tensorboard_plugin_profile/convert:raw_to_tool_data",
        "//plugin/tensorboard_plugin_profile/integration_tests:tf_mnist",
        "//plugin/tensorboard_plugin_profile/integration_tests:tf_profiler_session",
        "@com_google_absl_py//absl/flags",
        "@com_google_absl_py//absl/logging",
        "@com_google_absl_py//absl/testing:absltest",
    ],
)

py_strict_library(
    name = "tpu_tf2_keras_xla",
    srcs = ["tpu_tf2_keras_test.py"],
    visibility = ["//plugin:__pkg__"],
    deps = [
	    "@org_tensorflow//tensorflow/python/profiler/internal:_pywrap_profiler",
        "//plugin/tensorboard_plugin_profile/convert:raw_to_tool_data",
        "//plugin/tensorboard_plugin_profile/integration_tests:tf_mnist",
        "//plugin/tensorboard_plugin_profile/integration_tests:tf_profiler_session",
        "@com_google_absl_py//absl/flags",
        "@com_google_absl_py//absl/logging",
        "@com_google_absl_py//absl/testing:absltest",
    ],
)
