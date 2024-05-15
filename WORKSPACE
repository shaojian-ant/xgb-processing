# Copyright 2024 Ant Group Co., Ltd.
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

workspace(name = "xgb-processing")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

### ref yacl ###
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

SECRETFLOW_GIT = "https://github.com/secretflow"

# https://github.com/shaojian-ant/heu/tree/xgb-processing
HEU_COMMIT_ID  = "384ef9a08e249f7156fc10dc89f0ba48a016e81c"

YACL_COMMIT_ID  = "9c3e8fa5d83e673ad74c1f9ba83894876e599a38"

# yacl
git_repository(
    name = "yacl",
    commit = YACL_COMMIT_ID,
    recursive_init_submodules = True,
    remote = "{}/yacl.git".format(SECRETFLOW_GIT),
)

load("@yacl//bazel:repositories.bzl", "yacl_deps")

yacl_deps()

# heu
git_repository(
    name = "com_alipay_sf_heu",
    commit = HEU_COMMIT_ID,
    remote = "{}/heu.git".format(SECRETFLOW_GIT),
)

load("@com_alipay_sf_heu//third_party/bazel_cpp:repositories.bzl", "heu_cpp_deps")

heu_cpp_deps()

#### for cpp ####

load(
    "@rules_foreign_cc//foreign_cc:repositories.bzl",
    "rules_foreign_cc_dependencies",
)

rules_foreign_cc_dependencies(
    register_built_tools = False,
    register_default_tools = False,
    register_preinstalled_tools = True,
)

#### for python ####

load("@rules_python//python:repositories.bzl", "py_repositories")

py_repositories()

#### for cuda ####

http_archive(
    name = "rules_cuda",
    sha256 = "f62baee0150ac91f4cdfcb10df2be0d0e9b941d1d32c8cddf00b16b57bdb1540",
    strip_prefix = "rules_cuda-17ca7f8c04cf746aa4c0a0c3722799278df7ca93",
    urls = [
        # Main branch as of 2023-1-07
        "https://github.com/bazel-contrib/rules_cuda/archive/17ca7f8c04cf746aa4c0a0c3722799278df7ca93.tar.gz",
    ],
)

load("@rules_cuda//cuda:repositories.bzl", "register_detected_cuda_toolchains", "rules_cuda_dependencies")

rules_cuda_dependencies()

register_detected_cuda_toolchains()

#### for other third-party libs ####

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")

protobuf_deps()
