# docker-frps

A fast reverse proxy to help you expose a local server behind a NAT or firewall to the internet. This is the image for frps.

## Build

You can pull the image from `hub.docker.com`.

```sh
$ docker pull xuejianbin/frps
```

Or, you can build with source repository by yourself.

```sh
$ git clone https://github.com/xuejianbin/docker-frps.git
$ cd docker-frps
$ docker build -t xuejianbin/frps .
```

## Usage

You can run a frps container with default config.

```sh
$ sudo docker run --restart always -d \
--name frps \
-p 10080:80 -p 7000:7000 -p 7500:7500 \
xuejianbin/frps
```

```ini
[common]
bind_addr = 0.0.0.0
bind_port = 7000
vhost_http_port = 80
dashboard_port = 7500
dashboard_user = deploy
dashboard_pwd = 01234567a
auth_token = 01234567a
privilege_mode = true
privilege_token = 01234567a
```

Privilege mode is the default. All proxy configurations are set in client. See here for more information about privilege_mode: https://github.com/xuejianbin/frp#privilege-mode

If you want to modify configuration, you can volume your own `frps.ini` via tag `-v`.

```sh
$ docker run --restart always -d \
--name frps \
-p 10080:80 -p 7000:7000 -p 7500:7500 \
-v /path/to/frps.ini:/frps.ini \
xuejianbin/frps
```

Finally, check the iptables config and make sure that the firewall is not blocking the required ports. You can access `http://127.0.0.1:7500` to check frp's status and proxies's statistics information by dashboard.


