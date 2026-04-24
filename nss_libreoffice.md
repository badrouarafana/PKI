1. Create a database
```bash
certutil -d ~/.pki/nssdb -N --empty-password
```
2. import the pfx full chain
```bash
pk12util -d ~/.pki/nssdb -i file.pfx
#Enter password for PKCS12 file:
#pk12util: PKCS12 IMPORT SUCCESSFUL
```
3. List elements
```bash
certutil -L -d sql:$HOME/.pki/nssdb
```

3. Trust the root and sub CAs
```bash
certutil -M -n "Root CA NAME - Project" -t "CT,C,C" -d sql:$HOME/.pki/nssdb
certutil -M -n "Sub CA NAME - Project" -t "CT,C,C" -d sql:$HOME/.pki/nssdb
```

It should work after restaring libreoffice, don't forget to set the Path of the NSS database in libre office
link for explanation.
https://askubuntu.com/questions/1225262/how-do-i-generate-a-certificate-to-sign-pdf-electronically

dont forget also, to have a valid endpoint for the CRls (didn't try OSCP).
