# gazelle:exclude testdata
package(default_visibility = ["//visibility:public"])

load(
    "@io_bazel_rules_go//go:def.bzl",
    "go_binary",
    "go_library",
    "go_test",
)

go_binary(
    name = "list",
    embed = [":go_default_library"],
)

go_library(
    name = "go_default_library",
    srcs = ["main.go"],
    importpath = "k8s.io/kubernetes/test/typecheck",
    deps = ["//vendor/golang.org/x/tools/go/packages:go_default_library"],
)

filegroup(
    name = "package-srcs",
    srcs = glob(["**"]),
    tags = ["automanaged"],
    visibility = ["//visibility:private"],
)

filegroup(
    name = "all-srcs",
    srcs = [":package-srcs"],
    tags = ["automanaged"],
)

go_binary(
    name = "typecheck",
    embed = [":go_default_library"],
)

go_test(
    name = "go_default_test",
    srcs = ["main_test.go"],
    # The "../../" is because $(location) gives a relative path, but
    # relative to some root for which I can't find a variable.  Empirically
    # this is 2 levels up (since this file is 2 levels down from the repo
    # root).  Hack.
    args = ["--go=../../$(location @go_sdk//:bin/go)"],
    data = ["@go_sdk//:bin/go"] + glob(["testdata/**"]),
    embed = [":go_default_library"],
    deps = ["//vendor/golang.org/x/tools/go/packages:go_default_library"],
)
