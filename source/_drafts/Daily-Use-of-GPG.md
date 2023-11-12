---
title: Daily Use of GPG
categories:
    - privacy & anonymity 
tags:
    - gpg 
  
---

# Prepare GPG keys 

## Generate new keys
```sh
gpg --generate-key
```

## Backup keys 

## Import keys from backup

## Share public key with others

<domain>/.well-known/security.txt or at the root of the domain at <domain>/security.txt.

```sh
$ gpg --output ~/mygpg.key --armor --export email@example.com

-----BEGIN PGP PUBLIC KEY BLOCK-----

6HV8Q6put7QEsRjBq89z3Eh+H9XLBz9GXpGBs2J6C3gu2+hBzgagNxfJeMP45zJi
mQGNBGVQYHkBDADF1JkfvUEeZxp+dKxRpAELB7uAjOqkf305twVozoMv3ky76jqW
...
-----END PGP PUBLIC KEY BLOCK-----
```

## Import keys of others

```sh 
gpg --import name_of_pub_key_file
```

## List all keys 
```sh
gpg --list-keys 
```

# Make Outgoing Messages

## Sign document
Recipient can verify the message is not forged or damaged. 

Signing data with sender's private key so that recipient could verify with sender's public key. 

## Encrypt document
Recipient is the only one who can read the message.

Encrypt the document with recipient's public key so that recipient can decrypt.


## Sign GIT commit and tags



# Verify Incoming Message 

## Verify signature from others 


## Decrypt document from others

