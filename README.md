# lompi

**Loment 库的包管理器** —— 库是一个目录，身份是**内容哈希**，依赖就是源码里的 `use`。
用 **Loment 自己写**的，由 Loment 工具链编出来。

**它是独立命令，不是 Loment 的子命令**：`loment help` 里没有它，直接敲 `lompi`。

## 建它

需要先有 Loment 工具链（<https://github.com/FujoJTOP/loment>），然后**在本目录里**：

```
loment build lompi.lomt -o lompi
```

（必须在**本目录**下调用：本工具链按 **CWD** 解析 `use "lpi_cli.lomt"` 这种相对导入。）

```
lompi version
lompi index   <store>
lompi show    <store> <name[@version]>
lompi tree    <store> <name[@version]>
lompi resolve <store> <name[@version]>          # 打锁（按哈希钉住）
lompi check   <dir>                             # 校验一个库目录
```

自检驱动 `lpi_test.lomt`：每个模块一个 `selftest_<模块>()`，汇总后**退出码即结论**。

## 这个仓库是什么

**它是 FujoOS 单仓的发布口，不是开发地。** 开发在主仓里做，这里切出来发布
（主仓的 `tools/loment_publish.py`）。**别在这里直接提交** —— 下次发布会把它盖掉。

指南：`.claude/skills/lompi/SKILL.md`
