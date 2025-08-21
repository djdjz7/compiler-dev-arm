# compiler-dev

北大编译实践教学用编译器开发环境 (Compiler Development Environment)，但是魔改

## 变更内容

- 需要在容器内拉取的仓库更改为此仓库的 submodule
  - pku-minic/compiler-dev-test-cases
  - pku-minic/sysy-runtime-lib
  - pku-minic/koopa
- 又把 TUNA 源给换回来了
- 是的，你现在可以用 js/ts 写编译器，因为我把 bun 打包进去了

## 使用方法

### 从仓库构建

拉取仓库后，不要忘记执行

```sh
git submodule update --init --recursive
```

```sh
cd docker
make # or `sudo make`
docker run -it --rm compiler-dev-bun bash
```

## 镜像中包含的内容

- 必要的工具: `git`, `flex`, `bison`, `python3` (用于运行测试脚本).
- 构建工具: `make`, `cmake`, `bun`.
- 运行工具: `qemu-user-static`.
- 编译工具链: Rust 工具链, LLVM 工具链.
- Koopa IR 相关工具: `libkoopa`, `koopac`.
- 测试脚本: `autotest`.

## 关于 Bun

> Develop, test, run, and bundle JavaScript & TypeScript projects—all with Bun.
> Bun is an all-in-one JavaScript runtime & toolkit designed for speed,
> complete with a bundler, test runner, and Node.js-compatible package manager.
> Bun aims for 100% Node.js compatibility.（棒读）

我们使用 `bun build --compile --outfile="{compiler_output}" "{repo_dir}"` 构建输出。

总之！你现在就可以用 `bun init` 新建一个项目写编译器了！记得在 `package.json` 的 `module` 下填上入口点

btw, 这个 [issue](https://github.com/oven-sh/bun/issues/8476) 可能会有帮助

## 原仓库变更日志

见 [CHANGELOG.md](CHANGELOG.md).
