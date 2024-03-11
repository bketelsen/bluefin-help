Note that this is a cheatsheet and not a replacement for the official documentation:

- [ostree](https://ostreedev.github.io/ostree/)
- [rpm-ostree](https://coreos.github.io/rpm-ostree/)

OStree is how the root filesystem is managed in Universal Blue images. It can have multiple deployments including 1 active deployment and 1 or more standby or rollback deployments. 

## Managing ostree

### Update ostree
Pull updated version based on your current upstream repository.
```
rpm-ostree upgrade
```
> Note: Using the `ublue update` command includes this step. 

### Roll back deployment
This will change your next target boot to the previous deployment. Use this if you have issues with your current booted deployment.
```
rpm-ostree rollback
```

### Add rpm package
Install a new package layered on top of the file system tree.
Add `--now` to layer on top of the active tree.

```
rpm-ostree install $PACKAGE
```

### Get ostree status

See the current booted file system tree and any layered packages.
```
rpm-ostree status
```

> **Note:** This is very handy when getting help and reporting issues!

### Pin a file system tree
To pin your current file system use `0` and for the previous booted file system use `1`.
This will keep a deployment available so it is not garbage collected.

Useful for major version changes and kernel changes.
```
sudo ostree admin pin 0
```
Original Docs and Cheatsheet: [Justin Garrison](https://justingarrison.com/) and [Erwan Le Floch](https://github.com/erlefloch)