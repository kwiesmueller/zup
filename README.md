# Zup - Backup and restore using zfs, ssh, encryption and golang
[![Go Report Card](https://goreportcard.com/badge/github.com/kwiesmueller/zup)](https://goreportcard.com/report/github.com/kwiesmueller/zup)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/513590eff4e54095a25b66bf65bd1323)](https://www.codacy.com/app/kwiesmueller/zup?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=kwiesmueller/zup&amp;utm_campaign=Badge_Grade)
[![Build Status](https://travis-ci.org/kwiesmueller/zup.svg?branch=master)](https://travis-ci.org/kwiesmueller/zup)
[![Docker Repository on Quay](https://quay.io/repository/kwiesmueller/zup/status "Docker Repository on Quay")](https://quay.io/repository/kwiesmueller/zup)

Zup is used to create regular snapshots using zfs and storing them on an encrypted drive on a remote server.

## Process

Zup is doing backups in the following way:

1. A ZFS snapshot is being made
2. Zup is powering up the remote backup server using the respective api (if the server is down)
3. A SSH connection is being opened
4. The remote backup disk is being decrypted using a key stored only on the client side (piping it into decrypt) and the zpool on it get's mounted
5. The latest snapshot(s) is being transfered to the remote pool using zfs send/receive through ssh
6. Both the zpool and the decrypted drive get unmounted
7. Zup is shutting down the remote server using the respective api

## Dependencies

All dependencies inside this project are being managed by [dep](https://github.com/golang/dep) and are checked in.
After pulling the repository, it should not be required to do any further preparations aside from `make deps` to prepare the dev tools (once).

If new dependencies get added while coding, make sure to add them using `dep ensure --add "importpath"` and to check them into git.
We recommend adding your vendor changes in a separate commit to make reviewing your changes easier and faster.

## Contributing
Feedback and contributions are highly welcome. Feel free to file issues or pull requests.

## Attributions

* [Kolide for providing `kit`](https://github.com/kolide/kit)
