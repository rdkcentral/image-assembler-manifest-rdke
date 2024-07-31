# rdke-assembler-manifest-generic
Manifest to build RDKE image assembler builds

## Build Steps
Note: use `main` or `develop` branch.
```bash
# Initialize the repository
repo init -u git@github.com:rdkcentral/rdke-assembler-manifest-generic -m raspberrypi4-64.xml -b develop
or
repo init -u https://github.com/rdkcentral/rdke-assembler-manifest-generic.git -m raspberrypi4-64.xml -b develop

# Synchronize the repository
repo sync --no-clone-bundle --no-tags

# Build the project
MACHINE=raspberrypi4-64-rdke source ./scripts/setup-environment
bitbake lib32-rdk-fullstack-image
```