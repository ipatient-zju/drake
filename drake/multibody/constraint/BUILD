# -*- python -*-
# This file contains rules for Bazel; see drake/doc/bazel.rst.

load(
    "//tools:drake.bzl",
    "drake_cc_googletest",
    "drake_cc_library",
    "drake_cc_binary",
)
load("//tools:lint.bzl", "add_lint_tests")

package(default_visibility = ["//visibility:public"])

drake_cc_library(
    name = "constraint",
    hdrs = [
        "constraint_problem_data.h",
    ],
    deps = [
        "//drake/common",
    ],
)

drake_cc_library(
    name = "constraint_solver",
    srcs = ["constraint_solver.cc"],
    hdrs = [
        "constraint_solver.h",
    ],
    deps = [
        ":constraint",
        "//drake/solvers:mathematical_program",
    ],
)

# === test/ ===

drake_cc_googletest(
    name = "constraint_solver_test",
    deps = [
        ":constraint_solver",
        "//drake/examples/rod2d",
    ],
)

add_lint_tests()
