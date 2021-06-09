workspace(name = "asylo_examples")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# Download and use the Asylo SDK.
http_archive(
    name = "com_google_asylo",
    sha256 = "21e2798a345d4d508c4f09c4b92c7cdc06a445d8fca4094e3751cde48d1d27c9",
    strip_prefix = "asylo-0.6.3",
    urls = ["https://github.com/google/asylo/archive/v0.6.3.tar.gz"],
)

load(
    "@com_google_asylo//asylo/bazel:asylo_deps.bzl",
    "asylo_deps",
    "asylo_testonly_deps",
)

asylo_deps()

asylo_testonly_deps()

# sgx_deps is only needed if @linux_sgx is used.
load("@com_google_asylo//asylo/bazel:sgx_deps.bzl", "sgx_deps")

sgx_deps()

# remote_deps is only needed if remote backend is used.
load("@com_google_asylo//asylo/bazel:remote_deps.bzl", "remote_deps")

remote_deps()

# grpc_deps is only needed if gRPC is used. Projects using gRPC as an external
# dependency must call both grpc_deps() and grpc_extra_deps().
load("@com_github_grpc_grpc//bazel:grpc_deps.bzl", "grpc_deps")

grpc_deps()

load("@com_github_grpc_grpc//bazel:grpc_extra_deps.bzl", "grpc_extra_deps")

grpc_extra_deps()
