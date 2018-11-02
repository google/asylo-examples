workspace(name = "asylo_examples")

# Download and use the Asylo SDK.
http_archive(
    name = "com_google_asylo",
    urls = ["https://github.com/google/asylo/archive/v0.3.1.tar.gz"],
    strip_prefix = "asylo-0.3.1",
    sha256 = "9cde12db341b39df263b501903fab6b93c0d8de87eaf0c0a047b5a8e1ac541f4",
)
load("@com_google_asylo//asylo/bazel:asylo_deps.bzl", "asylo_deps",
     "asylo_testonly_deps")
asylo_deps()
asylo_testonly_deps()

load("@com_google_asylo//asylo/bazel:sgx_deps.bzl", "sgx_deps")
sgx_deps()

load("@com_github_grpc_grpc//bazel:grpc_deps.bzl", "grpc_deps")
grpc_deps()
