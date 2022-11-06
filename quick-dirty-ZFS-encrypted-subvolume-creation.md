## Note, this is how one creates a ZFS subvolume that is decrypted automatically... assuming `/`, especially `/root` is encrypted.

### First, create a keyfile:

`mkdir /root/keys`
`openssl rand -out /root/keys/keyfile.dat 32`

Second, create the ZFS pool.

To add, type in :

`zfs create -o encryption=on -o keyformat=raw -o keylocation=file:///root/keys/enc.dat pool/subvolume`

-----

If it doesn't mount, type in:

`zfs loadkey -a`

`zfs mount -a`

-----

Assumptions:

* `/root/keys` is protected.  With `/` encrypted, this is usually the case.
* A recent version of ZFS is used.

Caveats:

*  Please save that 32 byte file.  I use `gpg --enarmor` and copy it off somewhere secure, so if I lose access to the directory, I still have access to the encrypted ZFS volumes.