# compiler-dev

北大编译实践教学用编译器开发环境 (Compiler Development Environment)，但是魔改

## 变更内容

- 需要在容器内拉取的仓库更改为此仓库的 submodule
  - pku-minic/compiler-dev-test-cases
  - pku-minic/sysy-runtime-lib
  - pku-minic/koopa
- 又把 TUNA 源给换回来了

## 使用方法

### 从仓库构建

拉取仓库后，不要忘记执行

```sh
git submodule update --init --recursive
```

```sh
cd docker
make # or `sudo make`
docker run -it --rm compiler-dev-arm bash
```

## 镜像中包含的内容

- 必要的工具: `git`, `flex`, `bison`, `python3` (用于运行测试脚本).
- 构建工具: `make`, `cmake`.
- 运行工具: `qemu-user-static`.
- 编译工具链: Rust 工具链, LLVM 工具链.
- Koopa IR 相关工具: `libkoopa`, `koopac`.
- 测试脚本: `autotest`.

## 原仓库变更日志

见 [CHANGELOG.md](CHANGELOG.md).
