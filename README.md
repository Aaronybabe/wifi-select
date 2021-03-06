## Introduction

*wifi-select* is a console tool for selecting wireless networks in "real-time"
(in NetworkManager fashion). The tool might be convenient to use in Internet
cafés or other places you are visiting for the first (and maybe the last) time.
With *wifi-select* you do not need to create a profile for a new network, just
type:

    $ sudo wifi-select wlan0

and choose the network you need. In order not to type "wlan0" every time, you
can set it (or make sure it is already there) in $WIRELESS_INTERFACE in
/etc/conf.d/netcfg

*wifi-select* is currently packaged and available in the [community] ArchLinux
repository. To install it, please run:

    # pacman -S wifi-select

## Synopsis

    Usage: wifi-select [-p | --show-pass] [-x | --pass-in-hex] [--use-dhclient] [-h | --help] [interface]

    Shows a list of available wireless networks and interactively connects to
    the network you select, asking for a password if needed.

    Arguments:
     -p, --show-pass    show password characters instead of '*' while typing a password,
                        (by default it shows '*')
     -x, --pass-in-hex  store the entered WPA password as a hexadecimal string
                        (using wpa_passphrase)
         --use-dhclient use "dhclient" instead of "dhcpcd" in generated profiles
     -h, --help         show this help

     interface          a wireless interface to use
                        (if omitted, uses WIRELESS_INTERFACE from /etc/conf.d/netcfg)


## Functionality

*wifi-select* does the following and nothing more:

* parses `iwlist scan` results and presents a list of networks along with their
  security settings (WPA/WEP/None) and signal quality using "dialog" tool

* if a user selects a network with an existing profile -- it uses this profile to
  connect with "netcfg"

* if the user selects a new network (which doesn't have a profile yet),
  *wifi-select* automatically generates a new profile with corresponding $SECURITY
  and asks for the key (if needed). The key for WPA may be stored as a hex string
  generated by `wpa_passphrase`. *wifi-select* uses DHCP as $IP by default

* if a network connection succeeds, the profile is saved for later usage

* if a network connection fails, the user is asked whether he/she wants to keep the
  generated profile for further usage (for example to change $IP to static or
  adjust some additional options)

## Links

* ArchLinux [Forum][] thread related to development of *wifi-select*
* *wifi-select* in \[community\] [community][]
* section in [ArchLinux wiki][wiki] page
* *wifi-select* in the [AUR][]

[forum]:     https://bbs.archlinux.org/viewtopic.php?id=63973
[community]: http://www.archlinux.org/packages/community/any/wifi-select/
[wiki]:      https://wiki.archlinux.org/index.php/Netcfg#wifi-select
[aur]:       http://aur.archlinux.org/packages.php?ID=23471
