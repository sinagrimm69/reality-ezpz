# reality-ezpz
You can install and configure reality protocol on your linux server by executing a single command.

This script:
* Installs docker with compose plugin in your server
* Generates docker-compose.yml and reality configuration
* Create Cloudflare warp account and configure warp as outbound
* Generates client configuration string and QRcode

Features:
* Generates client configuration string
* Generates client configuration QRcode
* You can choose between xray or sing-box core
* You can use a Text-based user interface (TUI)
* You can create multiple user accounts
* You can regenerate configuration and keys
* You can change SNI domain
* You can change transport protocol
* You can block malware and adult contents
* Supports natvps.net servers
* Use Cloudflare WARP to hide your outbound traffic
* Supports Cloudflare warp+
* Install with a single command

Supported OS:
* Ubuntu 22.04
* Ubuntu 20.04
* Ubuntu 18.04
* Debian 11
* Debian 10
* CentOS Stream 9
* CentOS Stream 8
* CentOS 7
* Fedora 37

## Quick Start
You can start using this script with default configuration by copy and paste the line below in terminal:
```
bash <(curl -sL https://bit.ly/realityez)
```
or (if the above command dosen't work):
```
bash <(curl -sL https://raw.githubusercontent.com/aleskxyz/reality-ezpz/master/reality-ezpz.sh)
```
After a while you will get configuration string and QR code:
![image](https://user-images.githubusercontent.com/39186039/232563871-0140e10a-22b4-4653-9bc9-cdba519a8b41.png)

You can run TUI with `-m` or `--menu` option:
```
bash <(curl -sL https://bit.ly/realityez) -m
```
And then you will see management menu in your terminal:
![image](https://github.com/aleskxyz/reality-ezpz/assets/39186039/a727148c-1a11-4702-80f3-ab8b46d916af)

```
Usage: reality-ezpz.sh [-t|--transport=tcp|h2|grpc] [-d|--domain=<domain>] [--regenerate] [--default] [-r|--restart]
[-p|--path=<path>] [-s|--enable-safenet] [--disable-safenet] [--port=<port>] [--enable-natvps] [--disable-natvps]
[--warp-license=<license>] [-w|--enable-warp] [--disable-warp] [-c|--core=xray|singbox] [-m|--menu]
[--add-user=<username>] [--lists-users] [--show-config=<username>] [--delete-user=<username>] [-u|--uninstall]

  -t, --transport <tcp|h2|grpc> Transport protocol (h2, grpc, tcp, default: tcp)
  -d, --domain <domain>     Domain to use as SNI (default: www.google.com)
      --regenerate          Regenerate public and private keys
      --default             Restore default configuration
  -r  --restart             Restart services
  -u, --uninstall           Uninstall reality
  -p, --path <path>         Absolute path to configuration directory (default: /home/username/reality)
  -s  --enable-safenet      Enable blocking malware and adult content
      --disable-safenet     Disable block malware and adult content
      --port <port>         Server port (default: 443)
      --enable-natvps       Enable natvps.net support
      --disble-natvps       Disable natvps.net support
      --warp-license <warp-license> Add Cloudflare warp+ license
  -w  --enable-warp         Enable Cloudflare warp
      --disable-warp        Disable Cloudflare warp
  -c  --core <singbox|xray> Select core (xray, singbox, default: singbox)
  -m  --menu                Show menu
      --add-user <username> Add new user
      --list-users          List all users
      --show-config <username> Shows the config and QR code of the user
      --delete-user <username> Delete the user
  -h, --help                Display this help message
```

## Clients
- Android
  - [v2rayNG](https://github.com/2dust/v2rayNg/releases)
  - [NekoBox](https://github.com/MatsuriDayo/NekoBoxForAndroid/releases)
- iOS
  - [Wings X](https://apps.apple.com/app/wings-x-client/id6446119727)
  - [Shadowrocket](https://apps.apple.com/app/shadowrocket/id932747118)
  - [Stash](https://apps.apple.com/app/stash/id1596063349)
- Windows
  - [v2rayN](https://github.com/2dust/v2rayN/releases)

## User Management
You can add, view and delete multiple user account with this script easily!

### Add User
You can add additional user by using `--add-user` option:
```
bash <(curl -sL https://bit.ly/realityez) --add-user user1
```
This command will create `test1` as a new user.

Notice: Username can only contains A-Z, a-z and 0-9

### List Users
You can view a list of all users by using `--list-users` option:
```
bash <(curl -sL https://bit.ly/realityez) --list-users
```

### Show User Configuration
You can get config string and QR code of the user for importing by using `--show-config` option:
```
bash <(curl -sL https://bit.ly/realityez) --show-config user1
```
This command will print config string and QR code of `user1`

### Delete User
You can delete a user by using `--delete-user` option:
```
bash <(curl -sL https://bit.ly/realityez) --delete-user user1
```
This command will delete `user1`

## Advanced Configuration
You can change script defaults by using different arguments.

Your configuration will be saved and restored in each execution.

### Change SNI domain
Default SNI domain is `www.google.com`.

You can change it by using `--domain` or `-d` options:
```
bash <(curl -sL https://bit.ly/realityez) -d yahoo.com
```
### Change transport protocol
Default (and recommended) transport protocol is `tcp`.

You can change it by using `--transport` or `-t` options:
```
bash <(curl -sL https://bit.ly/realityez) -t h2
```
Valid options are `tcp`,`h2` and `grpc`.

### Block malware and adult contents
You can block malware and adult contents by using `--enable-safenet` or `-s` options:
```
bash <(curl -sL https://bit.ly/realityez) -s
```
You can disable this feature by using `--disable-safenet` option.

### Installing on natvps.net servers
By using `--enable-natvps` option you can use this script on natvps.net servers:
```
bash <(curl -sL https://bit.ly/realityez) --enable-natvps
```
This script will find first available port automatically so you don't need to use `--port` option while using it.

You can disable feature with `--disable-natvps` option.

It seems that natvps.net servers have some dns configuration problems and the `curl` package is not installed in them by default.

You can solve these problems by running this command:
```
grep -q "^DNS=1.1.1.1$" /etc/systemd/resolved.conf || echo "DNS=1.1.1.1" >> /etc/systemd/resolved.conf && systemctl restart systemd-resolved && apt update && apt install curl -y
```

### Regenerate user account
You can regenerate public and private keys by using `--regenerate` option:
```
bash <(curl -sL https://bit.ly/realityez) --regenerate
```
All other configuration will be same as before.

### Restart services
You can restart reality by using `-r` or `--restart` options:
```
bash <(curl -sL https://bit.ly/realityez) -r
```

### Restore default configuration
You can restore default configuration by using `--default` option.
```
bash <(curl -sL https://bit.ly/realityez) --default
```
User account will not change with this option.

### Uninstall
You can delete configuration and services by using `--uninstall` or `-u` options:
```
bash <(curl -sL https://bit.ly/realityez) -u
```

### Change configuration path
Default configuration path is `$HOME/reality`.

You can change it by using `--path` or `-p` options:
```
bash <(curl -sL https://bit.ly/realityez) -p /opt/reality
```
The path should be absolute path.

### Change port
Notice: Do not change default port. This may block your IP!

Default port is `443`.

You can change it by using `--port` option:
```
bash <(curl -sL https://bit.ly/realityez) --port 8443
```

### Change engine core
Default engine core is sing-box but you can also switch to xray by using `--core` or `-c` options:
```
bash <(curl -sL https://bit.ly/realityez) -c xray
```
Valid options are `xray` and `singbox`.

### Text-based user interface (TUI)
You can also use the TUI for changing the configuration of the service.

To access to TUI you can use `-m` or `--menu` options:
```
bash <(curl -sL https://bit.ly/realityez) -m
```

## Cloudflare WARP
This script uses official Cloudflare WARP client for connecting to Cloudflare network and send all outbound traffic to Cloudflare server. So your servers address will be masked by Cloudflare IPs. This gives you a better web surffing experience due to less captcha challenges and also resolves some websites limitations on your servers IP.

You can enable Cloudflare WARP by using `-w` or `--enable-warp` options. This script will create and register a free WAPR account and use it.
```
bash <(curl -sL https://bit.ly/realityez) --enable-warp
```
Free account has traffic limitation and lower performance in comparison with WARP+ account which needs license.

You can either buy an WARP+ Unlimited license or get a free WARP+ license from this telegram bot: https://t.me/generatewarpplusbot

After getting a license from that telegram bot, you can use the license for your server with `--warp-license` option:
```
bash <(curl -sL https://bit.ly/realityez) --warp-license aaaaaaaa-bbbbbbbb-cccccccc
```
You can use each warp+ license on 4 devices only.

You can disable Cloudflare WARP by using `--disable-warp` option:
```
bash <(curl -sL https://bit.ly/realityez) --disable-warp
```

## Example
You can combine different options together.

We want to setup a server with these configurations:
* `grpc` transport protocol
* `www.wikipedia.org` as SNI domain
* Block adult contents
* Enable Cloudflare WARP
* Set Cloudflare WARP+ license

So we need to execute this command:
```
bash <(curl -sL https://bit.ly/realityez) -t grpc -d www.wikipedia.com -s -w --warp-license d34tgvde-gf73xvsj-23acfbg7
```
or
```
bash <(curl -sL https://bit.ly/realityez) --transport grpc --domain www.wikipedia.com --enable-safenet -enable-warp --warp-license d34tgvde-gf73xvsj-23acfbg7
```
