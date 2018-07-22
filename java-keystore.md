## This Tutorial explains the java keystore use.

**we can secure the TCP/UDP connection using SSL certificate.**
  - Java Keytool is a **_key_** and **_certificate_** _management tool_ that is used to manipulate _Java Keystores_.
  - A Java Keystore is a contianer for _authorization certificates_ or _public key certificates_.
  - The keystore entries are protected by keystore password.
  - A keystore entry is identified by an **alias**, and it consists of _keys_ and _certificates_ that form a trust chain.
  - The keystore file extension is .jks.
  - Each certificate in a Java keystore is associated with a unique alias.
  - we generate a new key pair in new/existing keystore and using this key we can later generate a CSR and obtain an 
    SSL certificate for this CSR form a certificate authority (CA). 

#### List of instructions to generate a certificate or create a keystore.

**To generate a new keypair in New/Existing keystore**
  
  - The below command creates a new keypair with the alias as keypair name in the new/existing keystore.
  
          keytool -genkeypair -alias <alias_name> -keyalg RSA -keystore <keystore_name>.<jks>
          
          e.g.: keytool -genkeypair -alias mykey -keyalg RSA -keystore myNewKeystore.jks
                here the .jks extension is optional.
           
  - The above command generates a 2048-bit RSA key pair, under the specified alias (alias name), in the specified keystore file (keystore.jks).
  - As soosn as we run the above command it will ask for a keystore password, if the keystore doesn;t exist then we've to pass a new password 
    for it to use in future else we've to use the existing password for existing keystore.
  - The it will ask some information for which it has to generate the keypair and then again it will ask for password for the private key
    by which we will generate the CSR and get signed by a CA. we can use the keystore password here too.
 
**Generate CSR For Existing Private Key**
  
  - we can generate an CSR That can be sent to a CA to request the issuance of a CA-signed SSL certificate.
  - it requires that the keystore and alias already exists.
  - This command creates a CSR signed by the private key identified by the alias in the keystore:
    
          keytool -certreq -alias <existing_alias_name> -file <csr_file_name>.csr -keystore <existing_keystore_name_corresponding_to_supplied_alias>.jks
          
          e.g.: keytool -certreq -alias mykey -file mycsr.csr -keystore myNewKeystore.jks
          
   - The provided alias name must exists in the provided keystore before we create the new CSR file.

**Import Signed/Root/Intermediate Certificate**

  - we can use the coomand to import a certificate to the existing keystore. 
  - This certificate cn be self signed certificate or a cerficate signed by CA.
  - This certificate must match the private key that existin the alias in the desired keystore.
  - The certificate to imported must be in .crt format.
  
           keytool -importcert -trustcacerts -file <certificate_name>.crt -alias <existing_alias_name> -keystore <existing_keystore_name>.jks
     
           e.g.: keytool -importcert -trustcacerts -file mycrt.crt -alias mykey1 -keystore myNewKeystore1.jks
                 if anything goes wrong like if the private key won't match then below error message will be thrown.
                 keytool error: java.security.cert.CertificateParsingException: java.io.IOException: ObjectIdentifier() -- data isn't an object ID (tag = 49)
   - Import a root or intermediate CA certificate to an existing Java keystore.
    
            keytool -importcert -trustcacerts -file <certificate_name>.crt -alias root -keystore <existing_keystore_name>.jks      
    

**Generate Self-Signed Certificate in New/Existing Keystore**
  - To create a self signed certificate with custom validity use belwo command.
    
           keytool -genkeypair -alias <alias_name> -keyalg RSA -validity <no_of_days> -keystore <keystore_name>.jks
       
#### Viewing Keystore Entries

**List Keystore Certificate Fingerprints**
  - To list all the availabe certificate fingerprint in a keystore.
  
          keytool -list -keystore <keystore_name>.jks
          output: 
          Keystore type: jks
          Keystore provider: SUN

          Your keystore contains 1 entry

          mykey, 22 Jul, 2018, PrivateKeyEntry, 
          Certificate fingerprint (SHA1): 83:0C:6F:9C:26:74:2B:A8:8E:71:05:B3:BA:D1:B3:E7:E5:67:B7:B8

          
          
**List Keystore content for a with all alias available inside the keystore**
  - It will list all the alias content in details available in keystore.
 
           keytool -list -v -keystore <KeyStore_name>.jks 


**Use Keytool to View Certificate Information**
  - To view certification information. like issuer name, validity, fingerprints, e.t.c
  
          keytool -printcert -file <certificate_name>.csr
        
        
**Export Certificate**
  - This command exports a binary DER-encoded certificate <certificate_name>.der, that is associated with the alias in the 
    keystore.
  - The certificate information inside the alias will be stored in the file specified with extension der.
          
          keytool -exportcert -alias <alias_name> -file <any_file_name>.der -keystore <keystore_name>.jks
         

#### Modifying Keystore

**To change the keystore password**

          keytool -storepasswd -keystore <existing_keystore_name>.jks
          
**To Delete An Alias**
  
        keytool -delete -alias <alias_Name> -keystore <keysotre_name>.jks
        
**To Rename An Alias**

         keytool -changealias -alias <old_alias_name> -destalias <new_alias_name> -keystore <keystore_name>.jks

         e.g. : keytool -changealias -alias mykey1 -destalias myNewAliasName -keystore myNewKeystore1.jks




                
          
