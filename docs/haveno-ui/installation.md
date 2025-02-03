# Installation

- This guide covers just what you need start using RetoSwap

**Before you can start trading on RetoSwap, you'll need a little Moneroj for a security deposit and fees (0.2 XMR should be enough). Each trader must lock Moneroj in a multisignature escrow until the trade is complete—this is part of what makes trading on RetoSwap highly secure.**

### 1. [Download and Install RetoSwap](https://retoswap.com/#downloads)

### 1.1 Software verification

Verify your installer file with our [PGP key](https://retoswap.com/reto_public.asc), signatures are available on the [releases page](https://github.com/retoaccess1/haveno-reto/releases)

!!! info
    After import and trust RetoSwap's GPG key, example for Debian installer:<br>
    `gpg --verify haveno-linux-deb.zip.sig && sha512sum haveno-linux-deb.zip`

If you'd like to build RetoSwap from source, [here are directions](https://github.com/retoaccess1/haveno-reto/blob/master/docs/installing.md). Haveno is free/libre open-source software that you can contribute to [(github)](https://github.com/retoaccess1/haveno-reto).

### 1.2 Installation

- .dmg packages aren't verified by apple, so you'll have to do ```$ xattr -d com.apple.quarantine /Applications/Haveno.app``` for allowing installations from builds untrusted by apple.
-  For installing a .deb: ```$ sudo dpkg -i /path/to/haveno.deb```
-  For flatpak: ```$ sudo flatpak install /path/to/Haveno.flatpak```
-  For .appimages, make sure you marked haveno.appimage as an executable ```$ chmod +x /path/to/haveno.appimage```
-  For TailsOS, please follow [security-section](./security.md#install-and-use-retoswap-on-tailsos) instructions.

If you'd like to build Haveno-reto from source, [here are directions](https://github.com/retoaccess1/haveno-reto/blob/master/docs/installing.md).

!!! info
    You can verify your self-built binary with provides hashes. Signature of hashes.txt can be checked with the following command:<br>
    `gpg --verify v*-hashes.txt.sig && sha512sum v*-hashes.txt`

Haveno is free/libre open-source software that you can contribute to [(github)](https://github.com/retoaccess1/haveno-reto).

### 2. Back Up Keys, Write Down Seed

- With RetoSwap, you're in total control of your funds and your data. This means you retain unparalleled sovereignty, but it also means no one can help you if you lose something important—so it's critical that you do proper backups before using RetoSwap to trade.

More details at: [data backup and restoration](backup_and_restore.md).

#### 2.1 Harden RetoSwap

If you want more security or needing custom network settings, go to [security page](./security.md)

### 3. Do a Trade

Go on [getting started](./get_started.md) for a trading tutorial to see both sides of a RetoSwap trade at the same time, side-by-side. Be sure to check out our [trading recommendations](./trading-recommendations.md) and [linked tutorials made by the community](https://haveno-reto.com/#posts) for more informations.

Making an offer will usually get you a better price and more control (e.g.: setting payment method and deposit percentage), but taking an offer can be more convenient.
