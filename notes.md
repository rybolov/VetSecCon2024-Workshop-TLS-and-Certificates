### Acronyms

3DES: Triple DES  
AES: Advanced Encryption Standard  
CA: Certificate Authority  
CN: Canonical Name  
CRL: Certificate Revocation List  
CSR: Certificate Signing Request  
DES: Data Encryption Standard  
DH: Diffie-Hellman  
DSA: Digital Signature Algorithm  
ECC: Elliptic Curve Cryptography  
HMAC: Keyed Hash Message Authentication Code  
HSTS: HTTP Strict Transport Security  
HTTP: Hyper Text Transport Protocol  
MD5: Message Digest #5  
PFS: Perfect Forward Secrecy  
PKI: Public Key Infrastructure  
RSA: Rivest-Shamir-Adleman  
SAN: Subject Alternate Names  
SHA: Secure Hash Algorithm  
SHA-2: SHA #2  
SHA-256: SHA-2 with 256 bits  
SNI: Server Name Indicator  
SSL: Secure Sockets Layer
TLS: Transport Layer Security  


### View the TLS handshake with a server
`curl -v -o /dev/null https://www.google.com/`  
`curl --insecure -v -o /dev/null https://www.google.com/`  

### View your Root CAs
Windows: `certmgr.msc`  
MacOS: Applications => Utilities => Keychain Access  
Linux: `ls /etc/ssl/certs`  

### View your machine certificates
Windows: `certlm.msc`  
MacOS: Applications => Utilities => Keychain Access  
Linux: `ls /etc/ssl/private`  

### Create Your Own CA and Certificate
https://deliciousbrains.com/ssl-certificate-authority-for-local-https-development/  
`sudo apt-get install ca-certificates`  
`mkdir pki-stuff`  
`cd pki-stuff`  
`openssl genrsa -des3 -out myCA.key 2048`  
`openssl req -x509 -new -nodes -key myCA.key -sha256 -days 1825 -out myCA.pem`

Look at your certificate:  
`openssl x509 -in myCA.pem -text -noout`

### Create a Certificate Using Your CA
`openssl genrsa -out webserver.key 2048`  
`openssl req -new -key webserver.key -out webserver.csr`  
`openssl x509 -req -in webserver.csr -CA myCA.pem -CAkey myCA.key -CAcreateserial -out webserver.pem -days 365 -sha256`  

Look at your certificate:  
`openssl x509 -in webserver.pem -text -noout `

### Use a Certificate in Apache
`sudo apt-get install apache`  
`sudo a2enmod ssl`  
`sudo ae2ensite default-ssl.conf`  
`sudo vi /etc/apache2/sites-enabled/default-ssl.conf` 
Replace the certificate file paths.  
`sudo systemctl restart apache2`


### SSL Labs

https://www.ssllabs.com/ssltest/  

### Installing Postfix Email Server with TLS
https://ubuntu.com/server/docs/install-and-configure-postfix


### Cloud Service Providers CA

AWS: https://aws.amazon.com/certificate-manager/  
Azure: https://learn.microsoft.com/en-us/azure/app-service/configure-ssl-certificate  
GCP: https://cloud.google.com/security/products/certificate-authority-service







