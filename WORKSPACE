load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "debian_bullseye_amd64_sysroot",
    build_file_content = 'filegroup(name="sysroot", srcs=glob(["*/**"]), visibility=["//visibility:public"])',
    sha256 = "47c02efd920c7f9c6b98b1498443170aa6102507d0672af5e794070833ef7454",
    url = "https://commondatastorage.googleapis.com/chrome-linux-sysroot/toolchain/4c00ba2ad61ca7cc39392f192aa39420e086777c/debian_bullseye_amd64_sysroot.tar.xz",
)

http_archive(
    name = "toolchains_llvm",
    canonical_id = "0.10.3",
    sha256 = "b7cd301ef7b0ece28d20d3e778697a5e3b81828393150bed04838c0c52963a01",
    strip_prefix = "toolchains_llvm-0.10.3",
    url = "https://github.com/grailbio/bazel-toolchain/releases/download/0.10.3/toolchains_llvm-0.10.3.tar.gz",
)

load("@toolchains_llvm//toolchain:deps.bzl", "bazel_toolchain_dependencies")

bazel_toolchain_dependencies()

load("@toolchains_llvm//toolchain:rules.bzl", "llvm_toolchain")

llvm_toolchain(
    name = "llvm_toolchain",
    llvm_version = "15.0.6",
    sysroot = {"linux-x86_64": "@debian_bullseye_amd64_sysroot//:sysroot"},
)

load("@llvm_toolchain//:toolchains.bzl", "llvm_register_toolchains")

llvm_register_toolchains()

http_archive(
    name = "rules_cuda",
    patches = ["//:sysroot-includes.patch"],
    sha256 = "2f8c8c8c85f727bec4423efecec12d3b751cb0a98bda99f0f9d351608a23b858",
    strip_prefix = "rules_cuda-v0.2.1",
    url = "https://github.com/bazel-contrib/rules_cuda/releases/download/v0.2.1/rules_cuda-v0.2.1.tar.gz",
)

load("@rules_cuda//cuda:repositories.bzl", "register_detected_cuda_toolchains", "rules_cuda_dependencies")

rules_cuda_dependencies()

register_detected_cuda_toolchains()
