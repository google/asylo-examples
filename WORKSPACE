workspace(name = "asylo_examples")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# Download and use the Asylo SDK.
http_archive(
    name = "com_google_asylo",
    urls = ["https://github.com/google/asylo/archive/v0.5.1.tar.gz"],
    strip_prefix = "asylo-0.5.1",
    sha256 = "944c7634f5fa00f3a074ab63442083b16272a57436820bc779f3305187d263d9",
)
load("@com_google_asylo//asylo/bazel:asylo_deps.bzl", "asylo_deps",
     "asylo_testonly_deps")
asylo_deps()
asylo_testonly_deps()

# sgx_deps is only needed if --config=sgx or sgx-sim is used.
load("@com_google_asylo//asylo/bazel:sgx_deps.bzl", "sgx_deps")
sgx_deps()

# remote_deps is only needed if remote backend is used.
load("@com_google_asylo//asylo/bazel:remote_deps.bzl", "remote_deps")
remote_deps()

# grpc_deps is only needed if gRPC is used.
load("@com_github_grpc_grpc//bazel:grpc_deps.bzl", "grpc_deps")
grpc_deps()
