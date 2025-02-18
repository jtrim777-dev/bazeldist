#
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.
#

load("@bazel_skylib//:bzl_library.bzl", "bzl_library")
load("@io_bazel_rules_kotlin//kotlin:kotlin.bzl", "kt_jvm_library")

exports_files(["deploy.sh.template"])

bzl_library(
    name = "lib",
    srcs = [
        "rules.bzl",
    ],
    visibility = ["//visibility:public"]
)

kt_jvm_library(
    name = "deployer-lib",
    srcs = glob(["*.kt"]),
    deps = [
        "@bazeldist//common",
        "@bazeldist//common/shell",
        "@bazeldist//common/util",

        "@maven//:info_picocli_picocli",
        "@maven//:org_zeroturnaround_zt_exec",
    ],
)

java_binary(
    name = "deployer-bin",
    runtime_deps = [":deployer-lib"],
    main_class = "com.vaticle.bazel.distribution.npm.deploy.DeployNPMKt",
    visibility = ["//visibility:public"],
)

filegroup(
  name = "pkg_content",
  srcs = glob(["*"]),
  visibility = ["//npm:__pkg__"]
)
