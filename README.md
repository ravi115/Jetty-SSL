# Jetty-SSL
This repository contains the information about jetty configuration on linux and SSL connection setup using keystore and openSSL.

- Most of those sites use the Socket Layer (SSL) protocol to secure their Internet applications. 
- SSL allows the data from a client, such as a Web browser, to be encrypted prior to transmission so that someone trying to sniff the data is unable to decipher it.
- Many Java application servers and Web servers support the use of keystores for SSL configuration.

**This is in short how it works:**

 - A browser requests a secure page (usually https://).
 - The web server sends its public key with its certificate.
 - The browser checks that the certificate was issued by a trusted party (usually a trusted root CA), that the certificate is still    valid and that the certificate is related to the site contacted.
 - The browser then uses the public key, to encrypt a random symmetric encryption key and sends it to the server with the encrypted URL required as well as other encrypted http data.
 - The web server decrypts the symmetric encryption key using its private key and uses the symmetric key to decrypt the URL and http data.
 - The web server sends back the requested html document and http data encrypted with the symmetric key.
 - The browser decrypts the http data and html document using the symmetric key and displays the information.
 
 
**There are three types of certificates:**
 
 - 1. **Private key**: 
   - The private key contains the identity information of the server, along with a key value. 
   - It should keep this key safe and protected by password because it’s used to negotiate the hash during the handshake.
   - It can be used by someone to decrypt the traffic and get your personal information. It like leaving your house key in the door lock.
 - 2. **Public key**: 
   - The public key is a portion that is presneted to a client. 
   - Public key is tightly associated with private key.
   - basically public key is a CSR which is created using private key after creating the private key. This, then send to CA. which signs the certificate by validating the serer information which this key contains.
 - 3. **Root Certificate**:
   - Root CA Certificate is a CA Certificate which is simply a Self-signed Certificate. 
   - This certificate represents a entity which issues certificate and is known as Certificate Authority or the CA such as VeriSign, Thawte, etc.
  
