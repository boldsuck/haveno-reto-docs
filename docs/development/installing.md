# Build and run Haveno

These are the steps needed to build and run Haveno. You can test it locally or on our test network using the official Haveno repository.

!!! note
    Trying to use Haveno on mainnet?

    The official Haveno repository does not operate or endorse any mainnet network.

    Find a third party network and use their installer or build their repository. Alternatively [create your own mainnet network](https://github.com/haveno-dex/haveno/blob/master/docs/create-mainnet.md).

## Install dependencies

On Ubuntu: `sudo apt install make wget git`

On Windows, first install MSYS2:

  1. Install [MSYS2](https://www.msys2.org/).
  2. Start MSYS2 MINGW64 or MSYS MINGW32 depending on your system. Use MSYS2 for all commands throughout this document.
  4. Update pacman: `pacman -Syy`
  5. Install dependencies. During installation, use default=all by leaving the input blank and pressing enter.

      64-bit: `pacman -S mingw-w64-x86_64-toolchain make mingw-w64-x86_64-cmake git`

      32-bit: `pacman -S mingw-w64-i686-toolchain make mingw-w64-i686-cmake git`

On all platforms, install Java JDK 21:

```
curl -s "https://get.sdkman.io" | bash
sdk install java 21.0.2.fx-librca
```

## Build Haveno

If it's the first time you are building Haveno, run the following commands to download the repository, the needed dependencies, and build the latest release. If using a third party network, replace the repository URL with theirs:

```
git clone https://github.com/haveno-dex/haveno.git
cd haveno
git checkout master
make
```

*If you only want to quickly build the binaries, use `make skip-tests` instead of `make`. It will skip the tests and increase the build speed drastically.*

If you are updating from a previous version, run from the root of the repository:

```
git fetch --tags
git checkout master
make clean && make
```

## Run Haveno

!!! note
    When you run Haveno, your application folder will be installed to:

    - Linux: `~/.local/share/Haveno/`
    - macOS: `~/Library/Application\ Support/Haveno/`
    - Windows: `~\AppData\Roaming\Haveno\`

### Mainnet

If you are building a third party repository which supports mainnet, you can start Haveno with:

```
make haveno-desktop-mainnet
```

### Join the public test network

If you want to try Haveno in a live setup, launch a Haveno instance that will connect to other peers on our public test environment, which runs on Monero's stagenet (you won't need to download the blockchain locally). You'll be able to make test trades with other users and have a preview of Haveno's trade protocol in action. Note that development is very much ongoing. Things are slow and might break.

Steps:

1. Run `make user1-desktop-stagenet` to start the application.
2. Click on the "Funds" tab in the top menu and copy the generated XMR address.
3. Go to the [stagenet faucet](https://stagenet-faucet.xmr-tw.org) and paste the address above in the "Get XMR" field. Submit and see the stagenet coins being sent to your Haveno instance.
4. While you wait for the 10 confirmations (20 minutes) needed for your funds to be spendable, create a fiat account by clicking on "Account" in the top menu, select the "National currency accounts" tab, then add a new account. For simplicity, we suggest testing using a Revolut account with a random ID.
5. Now pick up an existing offer or open a new one. Fund your trade and wait for 10 blocks for your deposit to be unlocked.
6. Now if you are taking a trade you'll be asked to confirm you have sent the payment outside Haveno. Confirm in the app and wait for the confirmation of the received payment from the other trader.
7. Once the other trader confirms, deposits are sent back to the owners and the trade is complete.

### Run a local test network

If you are a developer who wants to test Haveno in a more controlled way, follow the next steps to build a local test environment.

#### Run a local XMR testnet

1. In a new terminal window run `make monerod1-local`
1. In a new terminal window run `make monerod2-local`
3. Now mine the first 150 blocks to a random address before using, so wallets only use the latest output type. Run in one of the terminal windows opened above:

`start_mining 9tsUiG9bwcU7oTbAdBwBk2PzxFtysge5qcEsHEpetmEKgerHQa1fDqH7a4FiquZmms7yM22jdifVAD7jAb2e63GSJMuhY75 1`

#### Deploy

If you are a *screen* user, simply run `make deploy`. This command will open all needed Haveno instances (seednode, user1, user2, arbitrator) using *screen*. If this is the first time launching the arbitrator desktop application, register the arbitrator as explained in step 3 below.

If you don't use *screen*, open 4 terminal windows and run in each one of them:

  1. `make seednode-local`
  2. `make user1-desktop-local` or if you want to run user1 as a daemon: `make user1-daemon-local`
  3. `make user2-desktop-local` or if you want to run user2 as a daemon: `make user2-daemon-local`

If this is the first time launching the arbitrator desktop application, register the arbitrator after the interface opens. Go to the *Account* tab and press `cmd+r`. Confirm the registration of the arbitrator.

#### Fund your wallets

When running user1 and user2, you'll see a Monero address prompted in the terminal. Send test XMR to the addresses of both user1 and user2 to be able to initiate a trade.

You can fund the two wallets by mining some test XMR coins to those addresses. To do so, open a terminal where you ran monerod and run: `start_mining ADDRESS 1`.

monerod will start mining local testnet coins on your device using one thread. Replace `ADDRESS` with the address of user1 first, and then user2's. Run `stop_mining` to stop mining.

#### Start testing

You are all set. Now that everything is running and your wallets are funded, you can create test trades between user1 and user2. Remember to mine a few blocks after opening and accepting the test trade so the transaction will be confirmed.
