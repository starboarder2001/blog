---
layout: post
title:  "Using a SmartCard, PIV, or CAC (Common Access Card) with Ansible"
date:   2016-10-12 10:13:53 -0700
categories: piv smartcard ansible cac hspd12
---

Need to use Ansible with your SmartCard, PIV, CAC credentials?  The below forks of Paramiko and Ansible adds pkcs11 support which enables the use of SmartCards to authenticate the ssh session with Ansible.

Install opensc
===

Debian:
```
apt-get install opensc
```

CentOS:
```
yum install opensc
```

Mac/OSX:
```
brew install opensc
```

Install the PKCS11 enabled Paramiko
First uninstall paramiko (pip uinstall paramiko, brew uninstall paramiko, etc)
===

```
git clone https://github.com/starboarder2001/paramiko.git
pushd paramiko
git checkout smartcard_pkcs11 && python setup.py install
popd
```

Install the PKCS11 enabled Ansible (note this is forked from a development release of Ansible 2.2)
First uninstall ansible (pip uninstall ansible, brew uninstall ansible, etc)
====

```
git clone https://github.com/starboarder2001/ansible.git
pushd ansible
git submodule update --init --recursive
git checkout smartcard_pkcs11_cve-2016-9587 && python setup.py install
popd
```

Using The PKCS11 features with Ansible
```
-Z tells ansible to prompt for your pin and use pkcs11.
--pkcs11provider is the pkcs11 middleware, currently the only tested middleware is opensc.
--connection=paramiko is required to force ansible to use paramiko as the connection method.
```

```
$ ansible-playbook playbook.yml -s -K -Z --pkcs11provider=/usr/local/lib/opensc-pkcs11.so --connection=paramiko
sudo PASSWORD: XXXX
pin: XXXX
```

Notes
===

If you run into issues with install cryptography on mac >= 10.11.

```
brew install openssl
env LDFLAGS="-L$(brew --prefix openssl)/lib" CFLAGS="-I$(brew --prefix openssl)/include" python setup.py install
```
