# Bazel 7.6.1 + Rust 最简示例

本项目演示了如何使用 Bazel 7.6.1 编译 Rust 应用程序。

## 项目结构

```
rerun_sample/
├── BUILD               # Bazel 构建配置
├── MODULE.bazel        # Bazel 模块配置 (bzlmod)
├── WORKSPACE           # Bazel 工作区标记文件
├── Cargo.toml          # Rust 项目配置
├── Cargo.lock          # 锁定的依赖版本
└── src/
    └── main.rs         # Rust 源代码
```

## 关键配置文件

### MODULE.bazel
使用 bzlmod 现代依赖管理方式：
```bazel
module(
    name = "rerun_sample",
    version = "1.0.0",
)

bazel_dep(name = "rules_rust", version = "0.49.3")

rust = use_extension("@rules_rust//rust:extensions.bzl", "rust")
rust.toolchain(edition = "2021")
use_repo(rust, "rust_toolchains")

register_toolchains("@rust_toolchains//:all")
```

### BUILD
定义构建目标：
```bazel
load("@rules_rust//rust:defs.bzl", "rust_binary")

rust_binary(
    name = "hello_rerun",
    srcs = ["src/main.rs"],
    edition = "2021",
)
```

## 编译和运行

1. **编译**：
   ```bash
   bazel build //:hello_rerun
   ```

2. **运行**：
   ```bash
   ./bazel-bin/hello_rerun
   ```

## 环境要求

- Bazel 7.6.1
- Linux x86_64 系统
- 网络连接（用于下载 Rust 工具链和依赖）

## 特点

- ✅ 使用最新的 Bazel 7.6.1
- ✅ 采用 bzlmod 现代模块系统
- ✅ rules_rust 0.49.3 最新版本
- ✅ Rust 2021 edition
- ✅ 自动管理 Rust 工具链
- ✅ 完全可重复的构建

这个示例提供了 Bazel + Rust 的最小化配置，可以作为更复杂项目的起点。
