1. Document to sign
```bash
echo "Hello world !" > hello.txt
```

2. sign cms using openssl (suppose you have cert and pem already provided)
```bash
openssl cms -sign -in hello.txt -signer cert.pem -inkey private.pem -out hello.sig  -outform PEM
```
3. verify signature
```bash
openssl cms -verify -in hello.sig -inform PEM -content hello.txt -CAfile cert.pem
```
4. check elements of the CMS
```bash
openssl cms -verify -in hello.sig -inform PEM -content hello.txt -CAfile cms-sig.pem
```
5. extract the certificate of the CMS
```bash
openssl cms -in hello.sig -inform PEM -noout -certsout certs.pem
```
6. See the details of CMS
7. ```bash
openssl cms -cmsout -print -in hello.sig -inform PEM
   ```
