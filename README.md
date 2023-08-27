# OpenLDAP SSH Keys

These are a series of files that allow OpenLDAP to store SSH keys, and then allow an SSH server (typically OpenSSH) to fetch those keys to authenticate users. It includes a custom OpenLDAP schema in .ldif format, an OpenSSH server config file drop-in, and a shell script to allow OpenSSH to query the OpenLDAP server.

### Setup

#### OpenLDAP
Add openldap-ssh-keys.ldif to your OpenLDAP config with `ldapadd`

#### OpenSSH
1. Add the fetch-openldap-ssh-keys.sh script to /usr/local/sbin/ or wherever you want it to be run from. If you choose a different location, be sure to change it in the support-openldap-ssh-keys.conf file as well.
2. Add support-openldap-ssh-keys.conf to /etc/ssh/sshd_config.d/
3. Restart SSHD with `systemctl restart sshd.service`

### Adding an SSH key to a user account
Modify the add-ssh-key.ldif file with the appropriate DN and SSH public key, and then add it to the OpenLDAP user account with `ldapmodify`

### Alternatives
The openldap-ssh-keys.ldif file comes from Andrii Grytsenko's [openssh-ldap-publickey](https://github.com/AndriiGrytsenko/openssh-ldap-publickey/blob/v1.0.2/misc/openssh-lpk-openldap.ldif) project on GitHub, while the shell script is from Dennis Leeuw's [guide](https://pig.made-it.com/ldap-openssh.html#31454) on pig.made-it.com. Both projects are now so obsolete that neither of their OpenSSH configurations work on modern OpenSSH servers, which is what made this project necessary.

A more comprehensive, but more complicated and difficult to use, OpenSSH configuration is Dan Fuhry's [openssh-ldap-authkeys](https://github.com/fuhry/openssh-ldap-authkeys).
