workspace(name = "asylo_examples")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# Download and use the Asylo SDK.
http_archive(
    name = "com_google_asylo",
    urls = ["https://github.com/google/asylo/archive/v0.4.0.tar.gz"],
    strip_prefix = "asylo-0.4.0",
    sha256 = "9dd8063d1a8002f6cc729f0115e2140a2eb1b14a10c111411f6b554e14ee739c",
)
load("@com_google_asylo//asylo/bazel:asylo_deps.bzl", "asylo_deps",
     "asylo_testonly_deps")
asylo_deps()
asylo_testonly_deps()

load("@com_google_asylo//asylo/bazel:sgx_deps.bzl", "sgx_deps")
sgx_deps()

load("@com_github_grpc_grpc//bazel:grpc_deps.bzl", "grpc_deps")
grpc_deps()
