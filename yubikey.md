## Yubikey

#### Two-factor authentication with SSH
######To prepare the yubikey:
  * install opensc
  * insert yubikey
  * install yubico software
    `# apt-add-repository ppa:yubico/stable`
    `# apt-get update`
    `# apt-get install yubico-piv-tool`

  * `$ yubico-piv-tool -s 9a -a generate -o public.pem`
  * verify the pin:
      `$ yubico-piv-tool -a verify-pin -P 123456`
  * change the pin:
      `$ yubico-piv-tool -a change-pin -P 123456 -N 1234`
  * self sign the cert:
      `$ yubico-piv-tool -a verify-pin -P 183192 -a selfsign-certificate -s 9a -S "/CN=SSH key/" -i public.pem -o cert.pem`
  * import it:
      `$ yubico-piv-tool -a import-certificate -s 9a -i cert.pem`

###### Set up computer:
  * Extract public key from yubikey:
      `$ ssh-keygen -D /usr/lib/x86_64-linux-gnu/opensc-pkcs11.so`
  * Add to the bottom of /etc/ssh/ssh_config (Arch):
      `PKCS11Provider /usr/lib/opensc-pkcs11.so`
  * Add to the botton of /etc/ssh_config (Debian, Ubuntu):
      `PKCS11Provider /usr/lib/x86_64-linux-gnu/opensc-pkcs11.so`
  * Add to the bottom of /etc/ssh_config (Fedora):
     `PCKS11Provider /usr/lib64/opensc-pkcs11.so`
  * SSH into a machine:
     `$ ssh -I /usr/lib/x86_64-linux-gnu/opensc-pkcs11.so root@198.211.96.59`

[Notes from Jupiter Broadcasting episode](http://www.jupiterbroadcasting.com/85062/ssh-authentication-with-yubikey-las-373/)