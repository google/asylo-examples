#
# Copyright 2019 Asylo authors
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

load(
    "@com_google_asylo//asylo/bazel:asylo.bzl",
    "enclave_loader",
)
load(
    "@linux_sgx//:sgx_sdk.bzl",
    "sgx",
)

licenses(["notice"])  # Apache v2.0

# Example demonstrating gRPC in Asylo for remote SGX backend.

package(
    default_visibility = ["//visibility:public"],
)

# The enclave hosting gRPC server.
sgx.unsigned_enclave(
    name = "grpc_server_enclave_unsigned.so",
    srcs = ["grpc_server_enclave.cc"],
    deps = [
        "@com_github_grpc_grpc//:grpc++",
        "@com_github_grpc_grpc//:grpc++_reflection",
        "@com_google_absl//absl/base:core_headers",
        "@com_google_absl//absl/memory",
        "@com_google_absl//absl/strings",
        "@com_google_absl//absl/synchronization",
        "@com_google_absl//absl/time",
        "@com_google_asylo//asylo:enclave_runtime",
        "@com_google_asylo//asylo/examples/grpc_server:grpc_server_config_cc_proto",
        "@com_google_asylo//asylo/examples/grpc_server:translator_server_impl",
        "@com_google_asylo//asylo/util:status",
    ],
)

sgx.debug_enclave(
    name = "grpc_server_enclave.so",
    unsigned = "grpc_server_enclave_unsigned.so",
    config = "@com_google_asylo//asylo/grpc/util:grpc_enclave_config",
)

# The driver for the gRPC server enclave.
enclave_loader(
    name = "grpc_server",
    srcs = ["grpc_server_driver.cc"],
    enclaves = {"enclave": ":grpc_server_enclave.so"},
    loader_args = ["--enclave_path='{enclave}'"],
    remote_proxy = "@com_google_asylo//asylo/util/remote:sgx_remote_proxy",
    deps = [
        "@com_google_absl//absl/flags:flag",
        "@com_google_absl//absl/flags:parse",
        "@com_google_asylo//asylo:enclave_client",
        "@com_google_asylo//asylo/examples/grpc_server:grpc_server_config_cc_proto",
        "@com_google_asylo//asylo/platform/primitives/sgx:loader_cc_proto",
        "@com_google_asylo//asylo/util:logging",
        "@com_google_asylo//asylo/util:status",
        "@com_google_asylo//asylo/util/remote:local_provision",
        "@com_google_asylo//asylo/util/remote:provision",
        "@com_google_asylo//asylo/util/remote:remote_loader_cc_proto",
        "@com_google_asylo//asylo/util/remote:remote_proxy_config",
    ],
)
