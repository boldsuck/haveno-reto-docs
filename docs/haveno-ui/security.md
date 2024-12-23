# Security tips

### Tor

- Full Tor routing:
Syncing your monero wallet is using clearnet by default (transactions are broadcasted over Tor). If you want to do it over Tor to keep your complete haveno/monero traffic private:
Edit your *haveno.properties* file located at `{haveno-reto-path}/haveno.properties` and add<br>
**--useTorForXmr=ON** in a new line (**--useTorForXmr=AFTER_SYNC** is the default arg)

- To use RetoSwap with an existing Tor connection, be sure to use in your tor configuration file:

```
PidFile {Cryptocurrency-path}/xmr_mainnet/tor/pid # Only on Linux
DataDirectory {Cryptocurrency-path}/xmr_mainnet/tor/
GeoIPFile {Cryptocurrency-path}/xmr_mainnet/tor/geoip
GeoIPv6File {Cryptocurrency-path}/xmr_mainnet/tor/geoip6
CookieAuthFile {Cryptocurrency-path}/xmr_mainnet/tor/.tor/control_auth_cookie
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

Now you can start Tor in first and then Cryptocurrency, the client will securely control Tor for all it's needs.

- To use RetoSwap on TailsOS
```
$ curl -fsSLO https://github.com/retoaccess1/haveno-reto/raw/master/scripts/install_tails/haveno-install.sh && bash haveno-install.sh https://github.com/retoaccess1/haveno-reto/releases/download/v(last-version)/haveno-linux-deb.zip <DAA24D878B8D36C90120A897CA02DAC12DAE2D0F>
```
To update your TailsOS Retoswap client, just run again this command and be sure you put the last version link.
