# rdke-assembler-manifest-generic
Manifest to build RDKE image assembler builds

## Build Steps
Note: use latest `TAG` for released versions or `develop` branch for develop HEAD.
```bash
# Initialize the repository
repo init -u https://github.com/rdkcentral/image-assembler-manifest-rdke.git -m raspberrypi4-64.xml -b develop

# Synchronize the repository
repo sync --no-clone-bundle --no-tags

# Build the project
MACHINE=raspberrypi4-64-rdke source ./scripts/setup-environment
bitbake lib32-rdk-fullstack-image
```
