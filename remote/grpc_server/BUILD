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
load("@linux_sgx//:sgx_sdk.bzl", "sgx")

licenses(["notice"])

# Example demonstrating gRPC in Asylo for remote SGX backend.

package(
    default_visibility = ["//visibility:public"],
)

# The driver for the gRPC server enclave.
enclave_loader(
    name = "grpc_server",
    srcs = ["grpc_server_driver.cc"],
    backends = sgx.backend_labels,  # Has SGX loader dependencies
    enclaves = {"enclave": "//grpc_server:grpc_server_enclave.so"},
    loader_args = ["--enclave_path='{enclave}'"],
    remote_proxy = "@com_google_asylo//asylo/util/remote:sgx_remote_proxy",
    deps = [
        "//grpc_server:grpc_server_config_cc_proto",
        "@com_google_absl//absl/flags:flag",
        "@com_google_absl//absl/flags:parse",
        "@com_google_asylo//asylo:enclave_client",
        "@com_google_asylo//asylo/platform/primitives/sgx:loader_cc_proto",
        "@com_google_asylo//asylo/util:logging",
        "@com_google_asylo//asylo/util:status",
        "@com_google_asylo//asylo/util/remote:local_provision",
        "@com_google_asylo//asylo/util/remote:provision",
        "@com_google_asylo//asylo/util/remote:remote_loader_cc_proto",
        "@com_google_asylo//asylo/util/remote:remote_proxy_config",
    ],
)
