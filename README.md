# Solana
本地新建Rust项目
```Rust
cargo new --lib solana-hello-world-localn
```
更新Cargo.toml文件，使用cargo add solana-program命令将solana-program添加到配置文件之中
并将crate-type同样添加到cargo.toml文件之中
```Rust
[lib]
crate-type = ["cdylib", "lib"]
```
更新src/lib.rs
```Rust
use solana_program::{
    account_info::AccountInfo,
    entrypoint,
    entrypoint::ProgramResult,
    pubkey::Pubkey,
    msg
};

entrypoint!(process_instruction);

pub fn process_instruction(
    program_id: &Pubkey,
    accounts: &[AccountInfo],
    instruction_data: &[u8]
) -> ProgramResult{
    msg!("Hello, world!");

    Ok(())
}
```
solana CLI配置指向本地主机
```
solana config set --url localhost
```
检查Solana CLI配置是否更新
```
solana config get
```
单独一个窗口运行本地测试验证器，只有我们的RPC URL命令设置为localhost才需要怎么做
```
solana-test-validator
```
OK事情进行到这里并没有什么问题,cat检查了一下刚刚修改的文件，没问题。现在用sbf命令来构建程序。
```
cargo build-sbf
```
我总会生成一个test-ledger文件夹，删了
```
rm -rf test-ledger/
```
tab找so文件,我的一般在 target/sbf-solana-solana/release/,有的时候会出现RPC request error的情况，那就是本地验证器挂掉了，重新整一下 
```
solana program deploy
```
