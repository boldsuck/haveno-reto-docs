## Security tips
#### Tor
- Syncing your monero wallet is using clearnet by default (transactions are broadcasted over Tor). If you want to do it over Tor to keep your complete haveno/monero traffic private:
Edit your *haveno.properties* file located at *{haveno-reto-path}/haveno.properties* and add **--useTorForXmr=ON** in a new line (**--useTorForXmr=AFTER_SYNC** is the default arg)

- To use Haveno-reto on TailsOS, an installation script [is available here]()
- To use Haveno-reto with an existing Tor connection, be sure to use in your tor configuration file:
```
PidFile {Haveno-reto-path}/xmr_mainnet/tor/pid # Only on Linux
DataDirectory {Haveno-reto-path}/xmr_mainnet/tor/
GeoIPFile {Haveno-reto-path}/xmr_mainnet/tor/geoip
GeoIPv6File {Haveno-reto-path}/xmr_mainnet/tor/geoip6
CookieAuthFile {Haveno-reto-path}/xmr_mainnet/tor/.tor/control_auth_cookie
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
Now you can start Tor in first and then haveno-reto, the client will securely control Tor for all it's needs.
