## apache

###### Support only TLS 1.2:
  Add to SSL Virtualhost:
  `SSLProtocol -all +TLSv1.2`

###### Enable perfect forward secrecy:
  Add to SSL Virtualhost:
  `SSLHonorCipherOrder on`
