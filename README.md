# Arbitrum airdrop scripts

*All responsibility for running scripts lies entirely on your shoulders*
*No warranties*


Proxy takes randomly - every request - random proxy
Use `production:` settings section for run

#### TG [channel](https://t.me/arbitrum_airdrop_ruby_script) and [chat](https://t.me/arbitrum_airdrop_rb_script_chat) (rare answers, sorry, public)


## Features
- Random changable proxy (also can work without proxy) (see `proxy_list:`)
- Ordered changable rpc (if bad response received from RPC - it will be rotately changed) (see `rpcs_list:`)
- Multithreading (threads count can be set by settings) (see `threads_count:`)
- Gas limit adaptation strategy (through request, or will be used from settings) __Be aware, if set by settings will not be changeable (restart script)__
- Gas price adaptation strategy (initial can be set in settings)

## Scripts set
- [Claimer](#claimer) (for claim tokens)
- [Transferer](#transferer) (for transfer tokens)
- [Seeder](#seeder) (for seeding native coins)


### Main notes
- Script can be launched at any time
- If script dropped - analyze log - and run it again
- If you want to stop script execution - use `CTRL+C` hotkey

### Requirements:
- ruby 3.1.3

### Environment installation guide
#### For windows
- Install [Sublime Merge](https://www.sublimemerge.com/)
- Install [RubyInstaller (3.1.3)](https://github.com/oneclick/rubyinstaller2/releases/download/RubyInstaller-3.1.3-1/rubyinstaller-devkit-3.1.3-1-x64.exe) (dowloads [page](https://rubyinstaller.org/downloads/))
- Clone this repository `https://github.com/d4mk0/ArbitrumAirdrop.git` by Sublime Merge
- Open folder with this project and open PowerShell window inside folder
- Run `bundle`

#### For mac/linux
- Open terminal and run inside
- Install brew
```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
- Install git through brew
```sh
brew install git
```
- Clone repository
```sh
git clone https://github.com/d4mk0/ArbitrumAirdrop.git
```
- Go to folder
```sh
cd ArbitrumAirdrop
```
- Install rvm
```sh
gpg --keyserver keyserver.ubuntu.com --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
curl -sSL https://get.rvm.io | bash
```
- Install ruby `rvm install 3.1.3`
- Run `bundle`



### Claimer
_Use to claim tokens_

#### Logic:
- Script checks current wallets situation and displays it on screen.
- When we have < 3 blocks (~30 seconds) before claim - displaying stopped and current block info only showed
- When we reach start block - script will try execute claim function if wallet have correct amount of eth

#### Run command
```sh
ruby claimer.rb
```

#### Required:
- fill `claimer/wallets.txt` by private keys (one per line)
- check `claimer/claimer_settings.yml` ensure its correct
    - `l1_block_start_period` claim will be started at 16890400 block (Ethereum mainnet)
    - `eth_border` - to ensure what u wallets have amount of ETH for claim/transfer fee

### Transferer

_Use to transfer tokens_

#### Logic:
- Script checks current wallets token and eth balances and displays it on screen.
- When some tokens available on wallet and eth for fee - present. It will try make transfer tokens to presented wallet

#### Notes:
- You can add two lines for transferring like this (wallet1(minter) -> wallet2(proxy) -> wallet3(exchange))

#### Required:
- fill `transferer/wallets.txt` by list of private_key and address to transfer (one private key per line, one address for send per line)
- check `transferer/transferer_settings.yml` ensure its correct
    - `eth_border` - to ensure what u wallets have amount of ETH for claim/transfer fee

#### Run command
```sh
ruby transferer.rb
```

### Seeder

_Use to transfer native ETH coins to wallets when specified L1 block will be created_

#### Notes:
- If you set one private key multiple times - it can cause bad nonce error (its ok, it will be retryable, but sending can take longer time). Best - use 1 private key one time.

#### Required:
- fill `seeder/wallets.txt` by private_keys for seeder and addresses to transfer
- check `seeder/seeder_settings.yml` ensure its correct
    - `amount_to_send` eth amount to sending in WEI
    - `l1_block_start_period` claim will be started at 16890400 block (Ethereum mainnet)
    
#### Run command
```sh
ruby seeder.rb
```

###### Donations. If u satisfy u can send some tips to 0xAB3966f0BDCB6D67a35C99F383C23c7350FB8943
