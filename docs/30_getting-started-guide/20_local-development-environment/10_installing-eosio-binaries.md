---
content_title: Install Antelope Binaries
link_text: Install Antelope Binaries 
---

To get started as quickly as possible, we recommend using Antelope pre-built binaries. You also have an advanced option to build from source but that would consume an hour or more. 

[[info]]
| You can find how to build Antelope from source [here](https://docs.eosnetwork.com/manuals/eos/v2.2/install/build-from-source/).



## Step 1: Install binaries
The below commands will download binaries for respective operating systems.
### Mac OS X Brew Install:
```shell
brew tap eosio/eosio
brew install eosio
```

[[info]]
| If you don't have Brew installed, follow the installation instructions on the <a href="https://brew.sh/" target="_blank">official Brew website</a>.

### Ubuntu 20.04 Package Install
```sh
wget https://github.com/AntelopeIO/leap/releases/download/v2.2.0-rc1/eosio_2.2.0-rc1-ubuntu-20.04_amd64.deb
sudo apt install ./eosio_2.2.0-rc1-ubuntu-20.04_amd64.deb
```
### Ubuntu 18.04 Package Install
```sh
wget https://github.com/AntelopeIO/leap/releases/download/v2.2.0-rc1/eosio_2.2.0-rc1-ubuntu-18.04_amd64.deb
sudo apt install ./eosio_2.2.0-rc1-ubuntu-18.04_amd64.deb
```
### RPM-based (CentOS, Amazon Linux, etc.) Package Install
```sh
wget https://github.com/AntelopeIO/leap/releases/download/v2.2.0-rc1/eosio-2.2.0-rc1.el7.x86_64.rpm
sudo yum install ./eosio-2.2.0-rc1.el7.x86_64.rpm
```

[[warning]]
| If you have previous versions of eosio installed on your system, please uninstall before proceeding. For detailed instructions, see [here](https://github.com/AntelopeIO/leap/blob/master/README.md).

[[Note]]
| The installation process will install `nodeos`, `cleos`, and `keosd`, the components required to run and interact with a blockchain.

## Step 2: Set up a development directory, stick to it
You're going to need to pick a directory to work from, it's suggested to create a `contracts` directory somewhere on your local drive.
```shell
mkdir contracts
cd contracts
```

## Step 3: Enter your local directory below
Get the path of that directory and save it for later, as you're going to need it, you can use the following command to get your absolute path.
```
pwd
```

Enter the absolute path to your contract directory below, and it will be inserted throughout the documentation to make your life a bit easier. _This functionality requires cookies_

![cli](../cli_2.2.2.gif)

<div class="eosio-helper-box">
    <form id="CONTRACTS_DIR">
        <label>Absolute Path to Contract Directory</label>
        <input class="helper-cookie" name="CONTRACTS_DIR" type="text" />
        <input type="submit" />
        <span></span>
    </form>
</div>

## What's Next?
[Install the CDT](20_installing-eosiocdt.md): Steps to install the Antelope Contract Development Toolkit (CDT) on your system.