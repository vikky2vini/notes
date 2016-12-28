## OpenSSL

###### Request a CSR:
  `$ openssl req -new -newkey rsa:2048 -nodes -keyout mail.jaylacroix.me.key -out mail.jaylacroix.me.csr`

###### Print certificate info:
  `$ openssl x509 -text -noout -in <cert>`

###### Test a site or service:
  `$ openssl s_client -connect <server>:<port>`

###### Checksum cert files to amke sure they belong together:
  `$ openssl x509 -noout -modulus -in certificate.crt | openssl md5`
  `$ openssl rsa -noout -modulus -in privateKey.key | openssl md5`
  `$ openssl req -noout -modulus -in CSR.csr | openssl md5`

###### Create a bundle:
  `$ cat mail.jaylacroix.me.crt mail.jaylacroix.me.ca.bundle >> mail.jaylacroix.me.bundle`