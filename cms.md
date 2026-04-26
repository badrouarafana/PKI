# 1. Document to sign
```bash
echo "Hello world !" > hello.txt
```
# 2. Sign CMS using OpenSSL (assume cert + key already exist)

2.1 Requirements
- Certificate must include:
  - Digital Signature key usage
  - Email Protection EKU (recommended for CMS/S/MIME compatibility)
- Certificate chain should be available for verification (CA/intermediate if needed)

2.2 Create CMS signature (attached content)
```bash
openssl cms -sign   -in hello.txt   -signer cms-sig.pem   -inkey private.pem   -out hello.cms   -outform PEM   -nodetach
```
# 3. Verify signature
```bash
openssl cms -verify   -in hello.cms   -inform PEM   -content hello.txt   -CAfile cert.pem
```
# 4. Check CMS structure
```bash
openssl cms -cmsout -print   -in hello.cms   -inform PEM
```
# 5. Extract certificates from CMS
```bash
openssl cms -in hello.cms   -inform PEM   -noout   -certsout certs.pem
```
