# psp22-nuko

**This readme is current as of April 2024.**

The uploaded file is used by nukotoken.

Below is a simple example of how to build.

## 1. Example of OS used
ubuntu-22.04.4-desktop-amd64

Installation configuration - Minimal

## 2. Installing required packages
```
sudo apt install curl
sudo apt install g++
```

## 3. Installing Rust
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.cargo/env
```

## 4. Installing necessary ink-related packages

```
rustup toolchain install nightly
rustup component add rust-src --toolchain nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
```

```
sudo apt install binaryen
```

## 5. Installing cargo-contract
```
cargo install --force --locked cargo-contract
```

## 6. Install docker using snap

```
snap install docker
```

## 7. Add docker group
This is a **required** setting and will not work properly if you do not do it.
```
sudo groupadd docker
```

```
sudo usermod -aG docker $USER
```

Restart docker and exit from the console once.
```
sudo /bin/systemctl restart docker.service
exit
```

OR: Restart to apply settings.
```
sudo reboot
```

## 8. Create a new project with cargo contract
Set `NAME` by yourself.
```
cargo contract new NAME
```

## 9. Move to working directory
```
cd NAME
```
Add and modify files if necessary.

## 10. Verifiable build
```
cargo contract build --verifiable
```
By using `--verifiable`, the docker image (paritytech/contracts-verifiable) will be downloaded.

And built using the container of that image.

## 11. The build is complete and the contract is generated
The built file location is `NAME/target/ink/`

Three files are generated.

`NAME.wasm`, `NAME.json`, `NAME.contract`

The file `.contract` is used for verification.

## 12. When you need to verify the generated contract
Specify the location of the `.contract` file you want to verify.
```
cargo contract verify P/A/T/H/FILENAME.contract
```
By using verify, you can verify that the code in the working directory, and the specified `.contract` are the same code.

In case of successful completion.
```
Successfully verified contract `/home/user/NAME/target/ink/test.contract` against reference contract `P/A/T/H/FILENAME.contract`!
```

In cases where validation fails, the cause will be displayed.
```
Failed to verify the authenticity of `NAME` contract against the workspace 
found at "FILENAME.ext".
```

## 13. Finished
Meow.

## Reference
Installing required tools: docs.alephzero.org

https://docs.alephzero.org/aleph-zero/build/aleph-zero-smart-contracts-basics/installing-required-tools

paritytech/cargo-contract: github

https://github.com/paritytech/cargo-contract/tree/master

Contract Verification: use.ink

https://use.ink/basics/verification/contract-verification/

Linux post-installation steps for Docker Engine: docs.docker.com

https://docs.docker.com/engine/install/linux-postinstall/
