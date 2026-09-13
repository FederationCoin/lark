# Lark

Java library for USB hardware wallets used by Federation Sparrow. You do not install or run this tree by itself.

Not Bitcoin. Not affiliated with Sparrow Wallet. Experimental. No warranty; see the [Apache 2.0 license](LICENSE).

## For users

Federation Sparrow can talk to hardware through this library. Hot single-sig against a local `federationcoind -testnet` is the current success bar; hardware support on this chain is later. Device lists below are what the code still enumerates, not a promise that every model is tested on FederationCoin testnet.

## For developers

Forked from [privkeyio/lark](https://github.com/privkeyio/lark) (HWI-inspired, then extended; originally sparrowwallet). Origin is `git@github.com:FederationCoin/lark.git`. Mainline is `federationcoin`. GitHub is detached from that fork; **never push** privkeyio or sparrowwallet.

Java package names remain `com.sparrowwallet.lark`. Do not fetch `code.sparrowwallet.com`. `maven.federationcoin.org` is not provisioned. Tern is the sibling submodule, not a Maven coordinate.

Enumerated devices (all models unless noted): Coldcard, Trezor, Ledger, BitBox02, Jade, KeepKey, OneKey (Classic 1S and Pro).

### Clone and build

```bash
git clone git@github.com:FederationCoin/lark.git
git checkout federationcoin
./gradlew jar
./gradlew test
```

Example:

```java
Lark lark = new Lark();
List<HardwareClient> clients = lark.enumerate();

for (HardwareClient client : clients) {
    ExtendedKey xpub = lark.getPubKeyAtPath(client.getType(), client.getPath(), "m/84'/1'/0'");
}
```

BIP32 print form on this chain uses FederationCoin version bytes, not Bitcoin `tpub` / `xpub`.

### Branching

Work on a branch off `federationcoin`. Open a same-repo pull request; a human merges. Do not push straight to mainline. This library has no `get-to-mainnet` branch this iteration.

### Release

Independent versions and git tags come later. Sparrow pins a gitlink SHA that must already be on origin `federationcoin`. No Maven publish.

### Quality

Code quality checks and metrics will be added over time.
