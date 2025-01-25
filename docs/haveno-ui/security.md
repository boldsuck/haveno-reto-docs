# Security tips

## Tor

#### Force Tor routing on monero traffic from RetoSwap:
Syncing your monero wallet is using clearnet by default (transactions are broadcasted over Tor). If you want to do it over Tor to keep your complete haveno/monero traffic private:
Edit your *haveno.properties* file located at `{haveno-reto-path}/haveno.properties` and add
**--useTorForXmr=ON** in a new line (**--useTorForXmr=AFTER_SYNC** is the default arg)

#### Use RetoSwap with Tor running as a system process in background

Be sure to use in your tor configuration file:

```
PidFile {haveno-reto-path}/xmr_mainnet/tor/pid # Only on Linux
DataDirectory {haveno-reto-path}/xmr_mainnet/tor/
GeoIPFile {haveno-reto-path}/xmr_mainnet/tor/geoip
GeoIPv6File {haveno-reto-path}/xmr_mainnet/tor/geoip6
CookieAuthFile {haveno-reto-path}/xmr_mainnet/tor/.tor/control_auth_cookie
RunAsDaemon 1
AvoidDiskWrites 1
CookieAuthentication 1
ControlPort 9051
SOCKSPort 9050
```

And in your *haveno.properties* file:

```
torControlUseSafeCookieAuth 1
useTorForXmr=ON
torControlCookieFile={haveno-reto-path}/xmr_mainnet/tor/.tor/control_auth_cookie
torControlPort=9051
socks5ProxyXmrAddress=127.0.0.1:9050
```

Now you can start Tor in first and then RetoSwap, the client will securely control Tor for all it's needs.

### Install and use RetoSwap on TailsOS
```
$ curl -fsSLO https://github.com/retoaccess1/haveno-reto/raw/master/scripts/install_tails/haveno-install.sh && bash haveno-install.sh https://github.com/retoaccess1/haveno-reto/releases/download/v(last-version)/haveno-linux-deb.zip <DAA24D878B8D36C90120A897CA02DAC12DAE2D0F>
```
To update your TailsOS Retoswap client, just run again this command and be sure you put the [last version](https://github.com/retoaccess1/haveno-reto/releases/latest) link.

## Monero node

#### Use a custom node on RetoSwap

Add in your *haveno.properties* file:
```
xmrNode=http://{IPv4/6, DNS, Tor hidden-service}:{PORT}
```
If your node haves RPC authentication, add:
```
xmrNodeUsername={username}
xmrNodePassword={password}
```
If the connection to the monero node is LAN based or inside a virtual/private network, make sure to add:
```
useTorForXmr=OFF
```
If the monero node is a Tor hidden-service:
```
useTorForXmr=ON
```
