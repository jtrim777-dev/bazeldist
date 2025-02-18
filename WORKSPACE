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

workspace(name="bazeldist")

load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

# Load @rules_python, @io_bazel_rules_kotlin and @rules_jvm_external
load("//common:deps.bzl", "rules_python", "rules_kotlin", "rules_jvm_external", "rules_rust")
rules_python()
rules_kotlin()
rules_jvm_external()
rules_rust()

# Load @io_bazel_rules_kotlin
load("@io_bazel_rules_kotlin//kotlin:kotlin.bzl", "kotlin_repositories", "kt_register_toolchains")
kotlin_repositories()
kt_register_toolchains()

load("@bazeldist//maven:deps.bzl", "maven_artifacts_with_versions")
load("@rules_jvm_external//:defs.bzl", "maven_install")
maven_install(
    artifacts = maven_artifacts_with_versions,
    repositories = [
        "https://repo1.maven.org/maven2",
    ],
    strict_visibility = True,
    version_conflict_policy = "pinned",
    fetch_sources = True,
)


# Load @bazeldist_pip
load("//pip:deps.bzl", pip_deps = "deps")
pip_deps()

# Load @rules_pkg
load("//common:deps.bzl", "rules_pkg")
rules_pkg()
load("@rules_pkg//:deps.bzl", "rules_pkg_dependencies")
rules_pkg_dependencies()

# TODO: remove this declaration once we upgrade to @io_bazel_stardoc with Bazel 5 support
# Load @bazel_skylib
git_repository(
    name = "bazel_skylib",
    remote = "https://github.com/bazelbuild/bazel-skylib",
    commit = "6abad3de5fd9c001f67b17fe8c7242b3cc3b8851",
)
load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")
bazel_skylib_workspace()

# Load @io_bazel_stardoc
git_repository(
    name = "io_bazel_stardoc",
    remote = "https://github.com/bazelbuild/stardoc",
    tag = "0.5.1",
)
load("@io_bazel_stardoc//:setup.bzl", "stardoc_repositories")
stardoc_repositories()
