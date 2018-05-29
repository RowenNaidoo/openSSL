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
