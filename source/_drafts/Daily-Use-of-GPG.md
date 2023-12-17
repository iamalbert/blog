---
title: Daily Use of GPG
categories:
    - privacy & anonymity 
    - opsec
tags:
    - gpg 
  
---

# Prepare GPG keys 

## Generate new keys
```sh
gpg --gen-key
```

Or you can use `--full-gen-key` to set encryption algorithm, key size, and expiry date.

```sh
gpg --full-gen-key 
```

Sample output

```text
Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
  (14) Existing key from card
Your selection? 1
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072)
Requested keysize is 3072 bits
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 0
Key does not expire at all
Is this correct? (y/N) y
```

## List all keys 

```sh
gpg --list-key --keyid-format long
```

Sample Output
```text
/home/user/.gnupg/pubring.kbx
----------------------------
pub   rsa3072/84C9694F05E46BFA 2023-12-16 [SC]
              ^^^^^^^^^^^^^^^^ This is key ID
      8A4111386A906867172C760684C9694F05E46BFA
uid                 [ultimate] Firstname Lastname (comment) <example@gmail.com>
sub   rsa3072/B848B278A951A079 2023-12-16 [E]
```

## Backup keys 

```sh
gpg --armor --export-options backup --export-secret-keys KEY_ID_OR_EMAIL > private.gpg 
```

Options are 

- `--armor` to output ASCII-based keys instead of binary format
- `--export-options backup` to include meta data like ownertrust, signature, and user attributes.

## Import keys from backup

```sh
$ gpg --import-options restore --import private.gpg
$ gpg --edit-key your@id.here
gpg> trust
Your decision? 5
```

# Share public key with others


Some people post their public keys on their website. Some place it under `<domain>/.well-known/security.txt` or `<domain>/security.txt`.

## Export your key


```sh
$ gpg --armor --export email@example.com

-----BEGIN PGP PUBLIC KEY BLOCK-----

6HV8Q6put7QEsRjBq89z3Eh+H9XLBz9GXpGBs2J6C3gu2+hBzgagNxfJeMP45zJi
mQGNBGVQYHkBDADF1JkfvUEeZxp+dKxRpAELB7uAjOqkf305twVozoMv3ky76jqW
...
-----END PGP PUBLIC KEY BLOCK-----
```

## Import keys of others

```sh 
gpg --import public.gpg
```

# Sign GIT commit and tags




# Make Outgoing Messages

## Sign document
Recipient can verify the message is not forged or damaged. 

Signing data with sender's private key so that recipient could verify with sender's public key. 

## Encrypt document
Recipient is the only one who can read the message.

Encrypt the document with recipient's public key so that recipient can decrypt.





# Verify Incoming Message 

## Verify signature from others 


## Decrypt document from others

