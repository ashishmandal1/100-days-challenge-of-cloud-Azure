# Day 40 – Azure Key Vault RSA Encryption & Decryption

## Objective

Created an Azure Key Vault and used a 4096-bit RSA key to encrypt and decrypt a sensitive file using RSA-OAEP.

## Azure Resources

* Resource Group: `kml_rg_main-6555965ec2674d01`
* Region: `East US`
* Key Vault: `nautilus-21121670`
* SKU: `Standard`
* Soft Delete Retention: `7 days`
* RBAC Authorization: Disabled
* Access Policy: Get, List, Encrypt, Decrypt
* RSA Key: `nautilus-key`
* Key Type: RSA
* Key Size: `4096 bits`
* Encryption Algorithm: `RSA-OAEP`

## Encryption

* Source file: `/root/SensitiveData.txt`
* Base64-encoded the plaintext before encryption.
* Encrypted using the Azure Key Vault RSA key.
* Encrypted output: `/root/EncryptedData.bin`
* Ciphertext size: `512 bytes`

## Decryption

* Base64-encoded the encrypted binary before sending it to Key Vault.
* Decrypted using RSA-OAEP.
* Base64-decoded the decrypted result.
* Output file: `/root/DecryptedData.txt`

## Verification

* Original file size: `26 bytes`
* Decrypted file size: `26 bytes`
* `cmp` verification: `MATCH`
* SHA-256 hashes of original and decrypted files were identical.

## Result

Azure Key Vault RSA encryption and decryption was successfully completed and verified end-to-end.
