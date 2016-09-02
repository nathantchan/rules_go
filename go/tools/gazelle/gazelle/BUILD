load("@io_bazel_rules_go//go:def.bzl", "go_library", "go_binary", "go_test")
load("@bazel_tools//tools/build_defs/pkg:pkg.bzl", "pkg_deb", "pkg_tar")

go_library(
    name = "go_default_library",
    srcs = [
        "diff.go",
        "fix.go",
        "main.go",
        "print.go",
    ],
    deps = [
        "@io_bazel_buildifier//core:go_default_library",
        "@io_bazel_buildifier//differ:go_default_library",
        "//go/tools/gazelle/generator:go_default_library",
    ],
)

go_binary(
    name = "gazelle",
    library = ":go_default_library",
)

go_test(
    name = "gazelle_test",
    srcs = ["fix_test.go"],
    library = ":go_default_library",
)

pkg_tar(
    name = "gazelle-debian-data",
    extension = "tar.gz",
    deps = [
        ":gazelle",
    ],
    mode = "0755",
    package_dir = "/usr/bin",
    strip_prefix = ".",
)

pkg_deb(
    name = "gazelle-debian",
    architecture = "amd64",
    built_using = "bazel (HEAD)",
    data = ":gazelle-debian-data",
    depends = [
        "pkg-config",
        "zip",
        "g++",
        "zlib1g-dev",
        "unzip",
        "bash-completion",
    ],
    description = "Gazel is a BUILD file generator for Go projects",
    homepage = "http://bazel.io",
    maintainer = "The Bazel Authors <bazel-dev@googlegroups.com>",
    package = "gazelle",
)
