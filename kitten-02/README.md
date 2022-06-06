# CoolCat - kitten-02 - Testnet

**Genesis File**

[Genesis File](/kitten-02/genesis.json):

```bash
   curl -s  https://raw.githubusercontent.com/DigitalKitchenLabs/testnets/main/kitten-02/genesis.json > ~/.coolcatd/config/genesis.json
```

## Setup

**Prerequisites:** Make sure to have [Golang >=1.17](https://golang.org/).

#### Build from source

You need to ensure your gopath configuration is correct. If the following **'make'** step does not work then you might have to add these lines to your .profile or .zshrc in the users home folder:

```bash
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export GO111MODULE=on
export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin
```

```bash
git clone https://github.com/DigitalKitchenLab/coolcatd
cd coolcatd
starport chain build
```

This will build and install `coolcatd` binary into `$GOBIN`.

Note: When building from source, it is important to have your `$GOPATH` set correctly. When in doubt, the following should do:

```bash
mkdir ~/go
export GOPATH=~/go
```

### Minimum hardware requirements

- 4GB RAM
- 250GB of disk space
- 1.4 GHz amd64 CPU

## Setup validator node

Below are the instructions to generate & submit your genesis transaction

### Generate genesis transaction (pre-launch only)

1. Initialize the binary directories and create the local genesis file with the correct
   chain id

   ```bash
   coolcatd init <MONIKER-NAME> --chain-id="kitten-02"
   ```

2. Create a local key pair (you should use the same key associated with you airdropped account)

   ```bash
   coolcatd keys add <key-name>
   ```

   Note: if you're using an offline key for signing (for example, with a Ledger), do this with `junod keys add <KEY-NAME> --pubkey <YOUR-PUBKEY>`. For the rest of the transactions, you will use the `--generate-only` flag and sign them offline with `junod tx sign`.

3. Download the pre-genesis file:

   ```bash
   curl -s  https://raw.githubusercontent.com/DigitalKitchenLab/testnets/main/kitten-02/pre-genesis.json >~/.coolcatd/config/genesis.json
   ```

   Find your account in the `kitten-02/pre-genesis.json` file. The balance of your airdrop is what you'll be able to use with your validator.

4. Create the gentx, replace `<KEY-NAME>` and `<BALANCE>`:

   ```bash
   coolcatd gentx <KEY-NAME> <BALANCE>uccat --chain-id="kitten-02"
   ```

   If all goes well, you will see a message similar to the following:

   ```bash
   Genesis transaction written to "/home/user/.coolcatd/config/gentx/gentx-******.json"
   ```

### Submit genesis transaction

- Fork this repo into your Github account

- Clone your repo using:

  ```bash
  git clone https://github.com/<YOUR-GITHUB-USERNAME>/testnets
  ```

- Copy the generated gentx json file to `<REPO-PATH>/kitten-02/gentx/`

  ```bash
  cd testnets
  cp ~/.coolcatd/config/gentx/gentx*.json ./kitten-02/gentx/
  ```

- Commit and push to your repo
- Create a PR onto https://github.com/DigitalKitchenLab/testnets
