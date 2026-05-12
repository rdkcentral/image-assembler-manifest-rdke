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
```
## Setup IPK Feeds

IPK feeds are required for package installation and dependency resolution in downstream layers. You can configure local (file-based) feeds or remote feeds.

> ⚠️ **Important:** When using a local file feed, include the `file:/` prefix and make sure the path ends with a trailing `/`.

### Configure Vendor and Vendor-OSS IPK Feed

Edit the file:
```
rdke/vendor/meta-vendor-release/conf/machine/include/vendor.inc
```

Set the feed path (example):
```
# Configure Vendor OSS IPK's path
VENDOR_OSS_IPK_SERVER_PATH = "file:/${HOME}/community_shared/rdk-arm64-oss-vendor/<Vendor-Oss-IPK-Version>/ipk/"

# Configure Vendor IPK's path
VENDOR_IPK_SERVER_PATH = "file:/${HOME}/community_shared/raspberrypi4-64-rdke-vendor/<Vendor-IPK-Version>/ipk/"
```
# Build the project
```
MACHINE=raspberrypi4-64-rdke source ./scripts/setup-environment
```
Enable generation of a deployable IPK feed during the build:

```bash
echo 'DEPLOY_IPK_FEED = "1"' >> conf/local.conf
```
bitbake lib32-rdk-fullstack-image
```
