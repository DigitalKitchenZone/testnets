# CoolCat - kitten-04 - Testnet

**Genesis File**

[Genesis File](/kitten-04/genesis.json):

```bash
curl -s  https://raw.githubusercontent.com/DigitalKitchenLabs/testnets/main/kitten-04/genesis.json > ~/.coolcat/config/genesis.json
```

## Setup

**Prerequisites:** Make sure to have [Golang >=1.18](https://golang.org/).

#### Build from source

You need to ensure your gopath configuration is correct. If the following **'make'** step does not work then you might have to add these lines to your .profile or .zshrc in the users home folder:

```bash
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export GO111MODULE=on
export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin
```

```bash
git clone https://github.com/DigitalKitchenLabs/coolcat
cd coolcat
make install
```

This will build and install `coolcat` binary into `$GOBIN`.

Note: When building from source, it is important to have your `$GOPATH` set correctly. When in doubt, the following should do:

```bash
mkdir ~/go
export GOPATH=~/go
```

### Minimum hardware requirements

- 8GB RAM
- 250GB of disk space
- 2 GHz AMD64 CPU

## Setup validator node

Below are the instructions to generate & submit your genesis transaction

### Generate genesis transaction (pre-launch only)

1. Initialize the binary directories and create the local genesis file with the correct
   chain id

   ```bash
   coolcat init <MONIKER-NAME> --chain-id="kitten-04"
   ```

2. Create a local key pair (you should use the same key associated with you airdropped account)

   ```bash
   coolcat keys add <key-name>
   ```

   Note: if you're using an offline key for signing (for example, with a Ledger), do this with `coolcat keys add <KEY-NAME> --pubkey <YOUR-PUBKEY>`. For the rest of the transactions, you will use the `--generate-only` flag and sign them offline with `coolcat tx sign`.

3. Check if your validator key received the CatDrop and then create the gentx, replace `<KEY-NAME>` with yours:

   ```bash
   coolcat gentx <KEY-NAME> 1000000uccat --chain-id="kitten-04"
   ```

   If all goes well, you will see a message similar to the following:

   ```bash
   Genesis transaction written to "/home/user/.coolcat/config/gentx/gentx-******.json"
   ```

### Submit genesis transaction

- Fork this repo into your Github account

- Clone your repo using:

  ```bash
  git clone https://github.com/<YOUR-GITHUB-USERNAME>/testnets
  ```

- Copy the generated gentx json file to `<REPO-PATH>/kitten-04/gentx/`

  ```bash
  cd testnets
  cp ~/.coolcatd/config/gentx/gentx*.json ./kitten-02/gentx/
  ```

- Commit and push to your repo
- Create a PR onto https://github.com/DigitalKitchenLab/testnets
