# rdke-assembler-manifest-generic
Manifest to build RDKE image assembler builds

## Build Steps
Note: use latest `TAG` for released versions or `develop` branch for develop HEAD.
```bash
# Initialize the repository
repo init -u https://github.com/rdkcentral/image-assembler-manifest-rdke.git -m raspberrypi4-64.xml -b develop

# Synchronize the repository
repo sync --no-clone-bundle --no-tags
```
---
## Setup IPK Feeds

IPK feeds are required for package installation and dependency resolution in downstream layers. You can configure local (file-based) feeds or remote feeds.

> ⚠️ **Important:** When using a local file feed, include the `file://` prefix and make sure the path ends with a trailing `/`.

### Configure Vendor and Vendor-OSS IPK Feed

Edit the file:
```
rdke/vendor/meta-vendor-release/conf/machine/include/vendor.inc
```

Set the feed path (example):
```
# Configure Vendor IPK's path
VENDOR_IPK_SERVER_PATH = "file://${HOME}/community_shared/raspberrypi4-64-rdke-vendor/<Vendor-IPK-Version>/ipk/"

# Configure Vendor OSS IPK's path
VENDOR_OSS_IPK_SERVER_PATH = "file://${HOME}/community_shared/rdk-arm64-oss-vendor/<Vendor-Oss-IPK-Version>/ipk/"
```
### Configure MW and MW-OSS IPK Feed

Edit the file:
```
rdke/middleware/meta-middleware-release/conf/machine/include/middleware.inc
```

Set the feed path (example):
```
# Configure MW IPK's path
MW_IPK_SERVER_PATH = "file://${HOME}/community_shared/raspberrypi4-64-rdke-middleware/<MW-IPK-Version>/ipk/"

# Configure MW OSS IPK's path
MW_OSS_IPK_SERVER_PATH = "file://${HOME}/community_shared/rdk-arm64-oss-vendor/<MW-Oss-IPK-Version>/ipk/"
```
---

## Build Environment

```
MACHINE=raspberrypi4-64-rdke source ./scripts/setup-environment
```

Enable generation of a deployable IPK feed during the build:

```
echo 'DEPLOY_IPK_FEED = "1"' >> conf/local.conf
```
## Build Target
```
bitbake lib32-rdk-fullstack-image
```
