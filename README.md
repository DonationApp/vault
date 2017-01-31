# vault

Encrypted project related secrets

## Prerequisites

- [KeePass](http://keepass.info/) or [KeePassX](https://www.keepassx.org/)
- Bash
- OpenSSH
- OpenSSL

On Windows; Bash, OpenSSH and OpenSSL can be obtained by installing the git command line tools from https://git-scm.com/

On Linux/OSX they are likely already present

When you have the prerequisites you should clone the repository and create your local config. Change to the repository folder and then

```
cp .config.example .config
```

The config file exports 2 variables.

- `$NAME` should be set to the name of your public SSH key file in `public-keys` without the `.pub` extension
- `$PRIVATE_KEY` should be set to the path to the matching private SSH key file (which should be somewhere else on your system)

## Usage

### Accessing the vault

Store secrets in the `vault.kdbx` KeePass database. If your public SSH key has already been added then the password can be obtained by running

```
./decrypt
```

This will print the password to stdout (there will be OS specific ways to pipe this directly to your clipboard so that it does not appear on screen)

After making changes to the database remember to save and close it, then commit/push the changes.

### Adding a new public key

You can add your own public SSH key to the `public-keys` folder ensuring that it has a `.pub` suffix. You can then commit/push the repository.

However then you will have to get someone who already has access to encrypt the password for your public key. This can be done by

```
./decrypt | ./encrypt
```

And then commiting/pushing the repository

### Changing the database password

If you need to change the database password you can do so (perhaps by generating a new random one with KeePass). You can then use

```
./encrypt
```

To encrypt the new secret for every public key. Remember to commit/push all the changes
