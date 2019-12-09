---
layout: post
title: How to install swoole on mac
---
- The dependence of the php version
    - Swoole-1.x require PHP-5.3.10 or later
    - Swoole-4.x require PHP-7.0.0 or later
    - It does not rely on PHP's stream, sockets, pcntl, POSIX, sysvmsg and other extensions. PHP only needs to install the most basic extension
    - The PHP version support is consistent with the official PHP maintenance version. [Please refer to the PHP version support schedule](https://www.php.net/supported-versions.php)
    - Xenial 16.04 (LTS)

- Compilation and installation

    The swoole extension is built according to the PHP standard extension. Use phpize to generate compilation and detection script,. / configure to do compilation configuration detection, make to compile, and make install to install.

    - Please download the releases version of swoole. Pulling the latest code directly from the GitHub trunk may fail to compile
    - If there is no special requirement, please be sure to compile and install the latest version of swoole
    - If the current user is not root, you may not have write permission to the PHP installation directory. Sudo or Su are required during installation
    - If you are updating the code directly on the GIT branch, you must execute make clean before recompiling

- Installation preparation

    The following software must be installed before installation:
    
    - Php-7.0 or later
    - gcc-4.8 or later
    - make
    - autoconf
    - pcre (you can use yum install pcre-devel on CentOs)

- Download address
    
    - [https://github.com/swoole/swoole-src/releases](https://github.com/swoole/swoole-src/releases)
    - [http://pecl.php.net/package/swoole](http://pecl.php.net/package/swoole)
    - [http://git.oschina.net/swoole/swoole](http://git.oschina.net/swoole/swoole)

    After downloading the source code package, enter the source code directory at the terminal, execute the following command to compile and install

- New compilation example:

```
cd swoole
phpize (Ubuntu does not install phpize executable command: sudo apt-get install php-dev to install phpize)
./configure
make 
sudo make install
```

- Advanced full compilation example

    First contact with the developer of swoole, please try the simple compilation above. If there is any further need, you can adjust the compilation parameters of the following examples according to the specific needs and version

    [Compile parameter reference](https://wiki.swoole.com/wiki/page/437.html)

    The following script will download and compile the source code of the master branch. Make sure you have installed all dependencies, or you will encounter various dependency errors

```
mkdir -p ~/build && \
cd ~/build && \
rm -rf ./swoole-src && \
curl -o ./tmp/swoole.tar.gz https://github.com/swoole/swoole-src/archive/master.tar.gz -L && \
tar zxvf ./tmp/swoole.tar.gz && \
mv swoole-src* swoole-src && \
cd swoole-src && \
phpize && \
./configure \
--enable-coroutine \
--enable-openssl  \
--enable-http2  \
--enable-async-redis \
--enable-sockets \
--enable-mysqlnd && \
make clean && make && sudo make install
```

- PECL

    Note: PECL release time is later than GitHub release time

    The swoole project has been included in the official PHP extension library. In addition to downloading and compiling manually, you can also download and install with one click through the PECL command provided by the official PHP

```
pecl install swoole
```
- Configure php.ini

    After the compilation and installation are successful, modify php.ini to join

```
extension=swoole.so
```

Use php-m or phpinfo() to check whether swoole.so has been loaded successfully. If not , it is possiable that the path of php.ini is wrong, you can use php --ini to locate the absolute path of php.ini.