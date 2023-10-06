# Compile and Setup PHP with ASDF on Debian or Ubuntu

## Requirements

```bash
sudo apt update && sudo apt install -y autoconf bison build-essential curl gettext git libgd-dev libcurl4-openssl-dev libedit-dev libicu-dev libjpeg-dev default-libmysqlclient-dev libonig-dev libpng-dev libpq-dev libreadline-dev libsqlite3-dev libssl-dev libxml2-dev libzip-dev openssl pkg-config re2c zlib1g-dev
```

### OpenSSL

```bash
cd $HOME/.local
mkdir opt
cd opt
wget https://www.openssl.org/source/openssl-1.1.1i.tar.gz
tar xzf openssl-1.1.1i.tar.gz
cd openssl-1.1.1i
./Configure --prefix=$HOME/.local/opt/openssl-1.1.1i/bin -fPIC -shared linux-x86_64
make -j 8 
make install
```

### Solve errors
```bash
error:1416F086:SSL routines:tls_process_server_certificate:certificate verify failed in Command line code on line 1
```

Go to: ~/.asdf/plugins/php/bin
Edit install script and remove the last line 'install_composer "$ASDF_INSTALL_PATH"'
So that way you can install composer later yourself.

## Install

You can just change the desired version on command.
```bash
export PKG_CONFIG_PATH=$HOME/.local/opt/openssl-1.1.1i/bin/lib/pkgconfig && asdf install php 7.4.30
asdf global php 7.4.30
asdf reshim
```

### Install composer
```bash
wget -O ~/composer-setup.php https://getcomposer.org/installer
php ~/composer-setup.php --install-dir=$HOME/.asdf/installs/php/7.4.30/bin --filename=composer
asdf reshim
```
