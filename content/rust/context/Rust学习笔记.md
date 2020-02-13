### 安装
```
# windows
https://win.rustup.rs/

#linux
curl https://sh.rustup.rs -sSf | sh
source $HOME/.cargo/env
```

### 卸载
```
rustup self uninstall
```

### Cargo 是 Rust 的构建系统和包管理工具
```
# 创建项目
cargo new hello_cargo
# 构建项目
cargo build
# 编译运行
cargo run
# 代码检查
cargo check
# 发布版构建
cargo build --release
```