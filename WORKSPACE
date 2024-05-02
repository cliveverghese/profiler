workspace(name = "org_xprof")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
        name = "bazel_skylib",
        sha256 = "74d544d96f4a5bb630d465ca8bbcfe231e3594e5aae57e1edbf17a6eb3ca2506",
        urls = [
            "https://storage.googleapis.com/mirror.tensorflow.org/github.com/bazelbuild/bazel-skylib/releases/download/1.3.0/bazel-skylib-1.3.0.tar.gz",
            "https://github.com/bazelbuild/bazel-skylib/releases/download/1.3.0/bazel-skylib-1.3.0.tar.gz",
        ],
)

load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")
bazel_skylib_workspace()

http_archive(
    name = "rules_python",
    sha256 = "8272287b125a23bfc79650ecbbc045ebcaee4d632338b1a50aad34357bcbadce",
    strip_prefix = "rules_python-0.23.0",
    url = "https://github.com/bazelbuild/rules_python/releases/download/0.23.0/rules_python-0.23.0.tar.gz",
)

load("@rules_python//python:repositories.bzl", "py_repositories")

py_repositories()

load("@rules_python//python:repositories.bzl", "python_register_toolchains")

python_register_toolchains(
    name = "python",
    ignore_root_user_error = True,
    python_version = "3.9",
)


load("@rules_python//python:pip.bzl", "pip_parse")

pip_parse(
    name = "python_deps",
    requirements_lock = "//:requirements.txt"
)

load("@python_deps//:requirements.bzl","install_deps")
install_deps()

http_archive(
    name = "six_archive",
    build_file = "//:six.BUILD",
    sha256 = "1e61c37477a1626458e36f7b1d82aa5c9b094fa4802892072e49de9c60c4c926",
    strip_prefix = "six-1.16.0",
    urls = [
      "https://pypi.python.org/packages/source/s/six/six-1.16.0.tar.gz"
    ]
)

bind(
    name = "six",
    actual = "@six_archive//:six"
)

http_archive(
    name = "com_google_absl_py",
    sha256 = "5b476479811ed0b8c57bc0b3f517bc379c31e2fd13e12743ba0984de0e3f254a",
    strip_prefix = "abseil-py-127c98870edf5f03395ce9cf886266fa5f24455e",
    urls = [
        "https://github.com/abseil/abseil-py/archive/127c98870edf5f03395ce9cf886266fa5f24455e.tar.gz",
    ],
)

http_archive(
    name = "rules_rust",
    sha256 = "08109dccfa5bbf674ff4dba82b15d40d85b07436b02e62ab27e0b894f45bb4a3",
    strip_prefix = "rules_rust-d5ab4143245af8b33d1947813d411a6cae838409",
    urls = [
        # Master branch as of 2022-01-31
        "http://mirror.tensorflow.org/github.com/bazelbuild/rules_rust/archive/d5ab4143245af8b33d1947813d411a6cae838409.tar.gz",
        "https://github.com/bazelbuild/rules_rust/archive/d5ab4143245af8b33d1947813d411a6cae838409.tar.gz",
    ],
)

http_archive(
    name = "io_bazel_rules_webtesting",
    sha256 = "f89ca8e91ac53b3c61da356c685bf03e927f23b97b086cc593db8edc088c143f",
    urls = [
        # tag 0.3.1 resolves to commit afa8c4435ed8fd832046dab807ef998a26779ecb (2019-04-03 14:10:32 -0700)
        "http://mirror.tensorflow.org/github.com/bazelbuild/rules_webtesting/releases/download/0.3.1/rules_webtesting.tar.gz",
        "https://github.com/bazelbuild/rules_webtesting/releases/download/0.3.1/rules_webtesting.tar.gz",
    ],
)

http_archive(
        name = "io_bazel_rules_closure",
        sha256 = "5b00383d08dd71f28503736db0500b6fb4dda47489ff5fc6bed42557c07c6ba9",
        strip_prefix = "rules_closure-308b05b2419edb5c8ee0471b67a40403df940149",
        urls = [
            "https://storage.googleapis.com/mirror.tensorflow.org/github.com/bazelbuild/rules_closure/archive/308b05b2419edb5c8ee0471b67a40403df940149.tar.gz",
            "https://github.com/bazelbuild/rules_closure/archive/308b05b2419edb5c8ee0471b67a40403df940149.tar.gz",  # 2019-06-13
        ],
)

load("@io_bazel_rules_closure//closure:repositories.bzl", "closure_repositories")
closure_repositories()
http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "94070eff79305be05b7699207fbac5d2608054dd53e6109f7d00d923919ff45a",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/5.8.2/rules_nodejs-5.8.2.tar.gz"],
)

load("@build_bazel_rules_nodejs//:repositories.bzl", "build_bazel_rules_nodejs_dependencies")
build_bazel_rules_nodejs_dependencies()
load("@build_bazel_rules_nodejs//:index.bzl", "yarn_install")

yarn_install(
    name = "npm",
    # "Some rules only work by referencing labels nested inside npm packages
    # and therefore require turning off exports_directories_only."
    # This includes "ts_library".
    # See: https://github.com/bazelbuild/rules_nodejs/wiki/Migrating-to-5.0#exports_directories_only
    exports_directories_only = False,
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
)

http_archive(
    name = "org_tensorflow_tensorboard",
    sha256 = "7ec7ea4e7e5922968f98822af08a175c783c253072e143a20511b59509ec9634",
    strip_prefix = "tensorboard-2.16.2",
    urls = ["https://github.com/tensorflow/tensorboard/archive/refs/tags/2.16.2.tar.gz"], # 2021-03-08
)

load("@org_tensorflow_tensorboard//third_party:workspace.bzl", "tensorboard_workspace")

# rules_sass release information is difficult to find but it does seem to
# regularly release with same cadence and version as core sass.
# We typically upgrade this library whenever we upgrade rules_nodejs.
#
# rules_sass 1.55.0: https://github.com/bazelbuild/rules_sass/tree/1.55.0
http_archive(
    name = "io_bazel_rules_sass",
    sha256 = "1ea0103fa6adcb7d43ff26373b5082efe1d4b2e09c4f34f8a8f8b351e9a8a9b0",
    strip_prefix = "rules_sass-1.55.0",
    urls = [
        "http://mirror.tensorflow.org/github.com/bazelbuild/rules_sass/archive/1.55.0.zip",
        "https://github.com/bazelbuild/rules_sass/archive/1.55.0.zip",
    ],
)

load("@io_bazel_rules_sass//:defs.bzl", "sass_repositories")
sass_repositories()


http_archive(
    name = "org_tensorflow",
    # NOTE: when updating this, MAKE SURE to also update the protobuf_js runtime version
    # in third_party/workspace.bzl to >= the protobuf/protoc version provided by TF.
    sha256 = "c729e56efc945c6df08efe5c9f5b8b89329c7c91b8f40ad2bb3e13900bd4876d",
    strip_prefix = "tensorflow-2.16.1",
    urls = [
        "https://github.com/tensorflow/tensorflow/archive/refs/tags/v2.16.1.tar.gz",  # 2020-01-06
    ],
)

# Initialize TensorFlow's external dependencies.
load("@org_tensorflow//tensorflow:workspace3.bzl", "workspace")
workspace()
load("@org_tensorflow//tensorflow:workspace2.bzl", "workspace")
workspace()
load("@org_tensorflow//tensorflow:workspace1.bzl", "workspace")
workspace()
load("@org_tensorflow//tensorflow:workspace0.bzl", "workspace")
workspace()

# Initialize bazel package rules' external dependencies.
load("@rules_pkg//:deps.bzl", "rules_pkg_dependencies")
rules_pkg_dependencies()

http_archive(
    name = "com_google_protobuf",
    sha256 = "f66073dee0bc159157b0bd7f502d7d1ee0bc76b3c1eac9836927511bdc4b3fc1",
    strip_prefix = "protobuf-3.21.9",
    urls = [
        "https://github.com/protocolbuffers/protobuf/archive/v3.21.9.zip"
    ],
)

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")
protobuf_deps()

load("@rules_python//python:pip.bzl", "package_annotation", "pip_parse", "pip_install")

pip_install(
    name = "python_deps",
    requirements = "//:requirements.txt",
)

load("@python_deps//:requirements.bzl", "install_deps")

install_deps()

NUMPY_ANNOTATIONS = {
    "numpy": package_annotation(
        additive_build_content = """\
filegroup(
    name = "includes",
    srcs = glob(["site-packages/numpy/core/include/**/*.h"]),
)
cc_library(
    name = "numpy_headers",
    hdrs = [":includes"],
    strip_include_prefix="site-packages/numpy/core/include/",
)
""",
    ),
}

pip_parse(
    name = "pypi",
    annotations = NUMPY_ANNOTATIONS,
    requirements = "//:requirements_lock_pypi.txt",
)

load("@pypi//:requirements.bzl", "install_deps")

install_deps()
