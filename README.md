# GPG Cheat Sheet

A list of common GPG commands.

# Install

### Using Homebrew

```brew install gnupg```

# Commands

## Setup & Key Management

#### Create GPG key
```gpg --gen-key```

#### Export your public key
```gpg --export --armor [optional email or name?] > publickey.asc```

#### Import another person's public key
```gpg --import theirpublickey.asc```

#### List the public keys in your keyring
```gpg --list-keys```

#### List the private keys in your keyring
```gpg --list-secret-keys```

#### Trust a public key
``` 
gpg --edit-key [email or username]

trust (invoke trust command on the key)
5 (ultimate trust)
y (if prompted)
quit

```

## Encryption & Decryption

#### Encrypt a file
```gpg --encrypt --recipient [email or username] [filename.txt]```

If you want to encrypt a file so that **only you can decrypt it**, then specify yourself as the email or username:

```gpg --encrypt --recipient [your username or email] [filename.txt]```

If you want to encrypt a file so that **only a group can decrypt it**, define the group in your gpg.conf file (see below) and then specify that group in the recipient parameter:

```gpg --encrypt --recipient [group name] [filename.txt]```

And the **shortened version** of these commands:

```gpg -e -r [recipient] [filename.txt]```

#### Decrypt a file to terminal
```gpg --decrypt [filename.txt]```

Omit *--decrypt* if the file is a binary file.

#### Decrypt a file to disk
```gpg [filename.txt.gpg]```

### Signing and Verifying Signatures

#### Sign a file & output in binary format
```gpg --output output.txt --sign doc.txt```

#### Sign a file & output with clearsign
```gpg --clearsign doc.txt```

#### Sign a file & detach its signature
```gpg --output output.txt --detach-sig doc.txt```

#### Decrypt and verify signature
```gpg --output output.txt --decrypt signed.sig```

#### Verify signature
```gpg --verify signed.txt```

#### Verify with detached signature
```gpg --verify doc.sig doc.txt```

# Configuration

#### Create groups of people in your configuration file
GPG software configuration is stored in your home directory at **~/.gnupg/gpg.conf**.

You list the members of a group by some attribute of their public key found in your GPG keyring; this is typically a person's name or email address (or partials of either of these).

```group spies = nick, steve, chris```

# Sources

[http://blog.ghostinthemachines.com/2015/03/01/how-to-use-gpg-command-line/](http://blog.ghostinthemachines.com/2015/03/01/how-to-use-gpg-command-line/)
[https://www.gnupg.org/gph/en/manual/x135.html](https://www.gnupg.org/gph/en/manual/x135.html)
