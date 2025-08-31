---
layout: framework
title: Rust 程序设计语言
permalink: /doc/trpl/index.html
---

# Rust 程序设计语言

<!-- https://github.com/rust-lang/book/blob/main/src/title-page.md -->
<!-- commit 56ec353290429e6547109e88afea4de027b0f1a9 -->

**本书的英文原版作者为 Steve Klabnik 和 Carol Nichols，并由 Rust 社区补充完善。本简体中文译本由 Rust 中文社区翻译。**

本书的当前版本假设你使用 Rust 1.85.0（2025-02-17 发布）或更高版本并在所有项目的 Cargo.toml 文件中通过 `edition = "2024"`将其配置为使用 Rust 2024 edition 惯用法。请查看[第一章的 “安装” 部分][install]了解如何安装和升级 Rust。

本书的英文原版 HTML 格式可以在 [https://doc.rust-lang.org/stable/book/](https://doc.rust-lang.org/stable/book/) 在线阅读；使用 `rustup` 安装的 Rust 也包含一份英文离线版，运行 `rustup docs --book` 即可打开。

本书还有一些社区 [翻译版本][translations]。（译者注：简体中文译本可以在 [https://kaisery.github.io/trpl-zh-cn/](https://kaisery.github.io/trpl-zh-cn/) 在线阅读，PDF 版本请下载 [Rust 程序设计语言 简体中文版.pdf](https://kaisery.github.io/trpl-zh-cn/Rust%20%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1%E8%AF%AD%E8%A8%80%20%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87%E7%89%88.pdf)）

本书也有[由 No Starch Press 出版的纸质版和电子版][nsprust]。

[install]: ch01-01-installation.html
[nsprust]: https://nostarch.com/rust-programming-language-2nd-edition
[translations]: appendix-06-translation.html

> **🚨 想要具有互动性的学习体验吗？试试 Rust Book 的另一个版本，其中包括测验、高亮、可视化等功能**：<https://rust-book.cs.brown.edu>

目录

- [前言](foreword.md)
- [简介](ch00-00-introduction.md)
- 第一部分 入门指南
  - [1 入门指南](ch01-00-getting-started.md)
    - [1.1 安装](ch01-01-installation.md)
    - [1.2 Hello, World!](ch01-02-hello-world.md)
    - [1.3Hello, Cargo!](ch01-03-hello-cargo.md)
  - [2 编写一个猜数字游戏](ch02-00-guessing-game-tutorial.md)
  - [3 常见编程概念](ch03-00-common-programming-concepts.md)
    - [3.1 变量与可变性](ch03-01-variables-and-mutability.md)
    - [3.2 数据类型](ch03-02-data-types.md)
    - [3.3 函数](ch03-03-how-functions-work.md)
    - [3.4 注释](ch03-04-comments.md)
    - [3.5 控制流](ch03-05-control-flow.md)
  - [4 认识所有权](ch04-00-understanding-ownership.md)
    - [4.1 什么是所有权？](ch04-01-what-is-ownership.md)
    - [4.2 引用与借用](ch04-02-references-and-borrowing.md)
    - [4.3 Slice 类型](ch04-03-slices.md)
  - [5 使用结构体组织相关联的数据](ch05-00-structs.md)
    - [5.1 结构体的定义和实例化](ch05-01-defining-structs.md)
    - [5.2 结构体示例程序](ch05-02-example-structs.md)
    - [5.3 方法语法](ch05-03-method-syntax.md)
  - [6 枚举和模式匹配](ch06-00-enums.md)
    - [6.1枚举的定义](ch06-01-defining-an-enum.md)
    - [6.2 `match` 控制流结构](ch06-02-match.md)
    - [6.3 `if let` 和 `let else` 简洁控制流](ch06-03-if-let.md)
- 基本 Rust 技能
  - [7 使用包、Crate 和模块管理不断增长的项目](ch07-00-managing-growing-projects-with-packages-crates-and-modules.md)
    - [7.1 包和 Crate](ch07-01-packages-and-crates.md)
    - [7.2 定义模块来控制作用域与私有性](ch07-02-defining-modules-to-control-scope-and-privacy.md)
    - [7.3 引用模块树中项的路径](ch07-03-paths-for-referring-to-an-item-in-the-module-tree.md)
    - [7.4 使用 `use` 关键字将路径引入作用域](ch07-04-bringing-paths-into-scope-with-the-use-keyword.md)
    - [7.5 将模块拆分成多个文件](ch07-05-separating-modules-into-different-files.md)
  - [8 常见集合](ch08-00-common-collections.md)
    - [8.1 使用 Vector 储存列表](ch08-01-vectors.md)
    - [8.2 使用字符串储存 UTF-8 编码的文本](ch08-02-strings.md)
    - [8.3 使用 Hash Map 储存键值对](ch08-03-hash-maps.md)
  - [9 错误处理](ch09-00-error-handling.md)
    - [9.1 用 `panic!` 处理不可恢复的错误](ch09-01-unrecoverable-errors-with-panic.md)
    - [9.2 用 `Result` 处理可恢复的错误](ch09-02-recoverable-errors-with-result.md)
    - [9.3 要不要 `panic!`](ch09-03-to-panic-or-not-to-panic.md)
  - [10 泛型、Trait 和生命周期](ch10-00-generics.md)
    - [10.1 泛型数据类型](ch10-01-syntax.md)
    - [10.2 Trait：定义共同行为](ch10-02-traits.md)
    - [10.3 生命周期确保引用有效](ch10-03-lifetime-syntax.md)
  - [11 编写自动化测试](ch11-00-testing.md)
    - [11.1 如何编写测试](ch11-01-writing-tests.md)
    - [11.2 控制测试如何运行](ch11-02-running-tests.md)
    - [11.3 测试的组织结构](ch11-03-test-organization.md)
  - [一个 I/O 项目：构建命令行程序](ch12-00-an-io-project.md)
    - [接受命令行参数](ch12-01-accepting-command-line-arguments.md)
    - [读取文件](ch12-02-reading-a-file.md)
    - [重构以改进模块化与错误处理](ch12-03-improving-error-handling-and-modularity.md)
    - [采用测试驱动开发完善库的功能](ch12-04-testing-the-librarys-functionality.md)
    - [处理环境变量](ch12-05-working-with-environment-variables.md)
    - [将错误信息输出到标准错误而不是标准输出](ch12-06-writing-to-stderr-instead-of-stdout.md)
- Rust 编程思想
  - [13 函数式语言特性：迭代器与闭包](ch13-00-functional-features.md)
    - [13.1 闭包：可以捕获其环境的匿名函数](ch13-01-closures.md)
    - [13.2 使用迭代器处理元素序列](ch13-02-iterators.md)
    - [13.3 改进之前的 I/O 项目](ch13-03-improving-our-io-project.md)
    - [13.4 性能比较：循环对迭代器](ch13-04-performance.md)
  - [14 更多关于 Cargo 和 Crates.io 的内容](ch14-00-more-about-cargo.md)
    - [14.1 采用发布配置自定义构建](ch14-01-release-profiles.md)
    - [14.2 将 crate 发布到 Crates.io](ch14-02-publishing-to-crates-io.md)
    - [14.3 Cargo 工作空间](ch14-03-cargo-workspaces.md)
    - [14.4 使用 `cargo install` 安装二进制文件](ch14-04-installing-binaries.md)
    - [14.5 Cargo 自定义扩展命令](ch14-05-extending-cargo.md)
  - [15 智能指针](ch15-00-smart-pointers.md)
    - [15.1 使用 `Box<T>` 指向堆上数据](ch15-01-box.md)
    - [15.2 使用 `Deref` Trait 将智能指针当作常规引用处理](ch15-02-deref.md)
    - [15.3 使用 `Drop` Trait 运行清理代码](ch15-03-drop.md)
    - [15.4 `Rc<T>` 引用计数智能指针](ch15-04-rc.md)
    - [15.5 `RefCell<T>` 与内部可变性模式](ch15-05-interior-mutability.md)
    - [15.6 引用循环会导致内存泄漏](ch15-06-reference-cycles.md)
  - [16 无畏并发](ch16-00-concurrency.md)
    - [16.1 使用线程同时地运行代码](ch16-01-threads.md)
    - [16.2 使用消息传递在线程间通信](ch16-02-message-passing.md)
    - [16.3 共享状态并发](ch16-03-shared-state.md)
    - [16.4 使用 `Sync` 与 `Send` Traits 的可扩展并发](ch16-04-extensible-concurrency-sync-and-send.md)
  - [17 Async 和 await](ch17-00-async-await.md)
    - [17.1 Futures 和 async 语法](ch17-01-futures-and-syntax.md)
    - [17.2 并发与 async](ch17-02-concurrency-with-async.md)
    - [17.3 使用任意数量的 futures](ch17-03-more-futures.md)
    - [17.4 流（Streams）](ch17-04-streams.md)
    - [17.5 深入理解 async 相关的 traits](ch17-05-traits-for-async.md)
    - [17.6 future、任务和线程](ch17-06-futures-tasks-threads.md)
  - [18 面向对象编程特性](ch18-00-oop.md)
    - [18.1 面向对象语言的特征](ch18-01-what-is-oo.md)
    - [18.2 顾及不同类型值的 trait 对象](ch18-02-trait-objects.md)
    - [18.3 面向对象设计模式的实现](ch18-03-oo-design-patterns.md)
- 高级主题
  - [19 模式与模式匹配](ch19-00-patterns.md)
    - [19.1 所有可能会用到模式的位置](ch19-01-all-the-places-for-patterns.md)
    - [19.2 Refutability（可反驳性）: 模式是否会匹配失效](ch19-02-refutability.md)
    - [19.3 模式语法](ch19-03-pattern-syntax.md)
  - [20 高级特性](ch20-00-advanced-features.md)
    - [20.1 不安全 Rust](ch20-01-unsafe-rust.md)
    - [20.2 高级 trait](ch20-02-advanced-traits.md)
    - [20.3 高级类型](ch20-03-advanced-types.md)
    - [20.4 高级函数与闭包](ch20-04-advanced-functions-and-closures.md)
    - [20.5 宏](ch20-05-macros.md)
  - [21 最后的项目：构建多线程 web server](ch21-00-final-project-a-web-server.md)
    - [21.1 建立单线程 web server](ch21-01-single-threaded.md)
    - [21.2 将单线程 server 变为多线程 server](ch21-02-multithreaded.md)
    - [21.3 优雅停机与清理](ch21-03-graceful-shutdown-and-cleanup.md)
  - [附录](appendix-00.md)
    - [A - 关键字](appendix-01-keywords.md)
    - [B - 运算符与符号](appendix-02-operators.md)
    - [C - 可派生的 trait](appendix-03-derivable-traits.md)
    - [D - 实用开发工具](appendix-04-useful-development-tools.md)
    - [E - 版本](appendix-05-editions.md)
    - [F - 本书译本](appendix-06-translation.md)
    - [G - Rust 是如何开发的与 “Nightly Rust”](appendix-07-nightly-rust.md)
