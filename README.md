# linux-portable-encrypted-file-system

Create a Linux portable encrypted file system

- `apt install udisks2`

## CREATE

- `fallocate -l 128M linux.iso`
- `sudo cryptsetup -y luksFormat linux.iso`
- `udisksctl loop-setup -f linux.iso`
- `ls /dev/mapper`
- `sudo mkfs.ext4 -L crypt_fun /dev/mapper/luks-12ba09f7-4218-4923-a861-71af23dcdded`

## MOUNT EXISTING

- `udisksctl loop-setup -f linux.iso`
- If it's the initial mount chown the dir /media/rudi/crypt_fun

## UNMOUNT

- Use the explorer and click unmount
- OR
- `sudo umount /media/rudi/6345cdab-5f9a-45d9-8bdd-34f939718e52`
- `sudo cryptsetup luksClose /dev/mapper/luks-8b5bf64f-3c40-42c1-b568-05fc6fcc40fc`

NOTES

- The UUID from the file command will match the /dev/mapper filename:
- `file linux.iso`
- `linux.iso: LUKS encrypted file, ver 1 [aes, xts-plain64, sha256] UUID: 12ba09f7-4218-4923-a861-71af23dcdded`
- `ls /dev/mapper`
- Output:

```
ls -1 /dev/mapper
control
luks-12ba09f7-4218-4923-a861-71af23dcdded
```

## References

http://goohackle.com/how-to-create-a-portable-encrypted-file_system-on-a-loop-file/
https://askubuntu.com/questions/63594/mount-encrypted-volumes-from-command-line
https://help.ubuntu.com/community/EncryptedFilesystemsOnRemovableStorage
http://linuxbsdos.com/2014/01/16/manual-full-disk-encryption-setup-guide-for-ubuntu-13-10-linux-mint-16/
