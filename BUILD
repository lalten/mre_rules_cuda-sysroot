load("@rules_cuda//cuda:defs.bzl", "cuda_library")

cc_binary(
    name = "main",
    srcs = ["main.cpp"],
    deps = [":hello"],
)

cuda_library(
    name = "hello",
    srcs = ["hello.cu"],
    hdrs = ["hello.h"],
)
