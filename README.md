# openSSL
Generate ECDSA private key
```
openssl ecparam -name prime256v1 -genkey -noout -out ecdsa_private.pem
```

Generate Certificate Request using private key
```
openssl req -new -sha256 -key ecdsa_private.pem -out ecdsa.csr -subj "/C=AU/CN=Project Name/O=Company Name/OU=Department/L=Location/ST=State" -nodes
```

Self sign certificate
```
openssl x509 -req -days 365 -in ecdsa.csr -signkey ecdsa_private.pem -out servercert.pem
```

Generate public key
```
openssl x509 -pubkey -noout -in servercert.pem > pubkey.pem
```

Sign message
```
openssl dgst -sha256 -sign ecdsa_private.pem myData.txt > signature.bin
```

Verify signed message suing public key
```
openssl dgst -sha256 -verify pubkey.pem -signature signature.bin boardingPass.json
```

Sign using Java
```
Signature ecdsaSignature = Signature.getInstance("SHA256withECDSA");
ecdsaSignature.initSign(eccPrivateKey);
ecdsaSignature.update(dataToSign);
byte[] signature = ecdsaSignature.sign();
```

Verify signature using Java
```
Signature ecdsaSignature = Signature.getInstance("SHA256withECDSA");
ecdsaSignature.initVerify(certificate);
ecdsaSignature.update(dataToVerify);
boolean isValide = ecdsaSignature.verify(rawSignature);
```
