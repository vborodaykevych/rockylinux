# Rocky Linux Multiarch Docker Images

[![Build and Push Rocky Linux Images](https://github.com/vborodaykevych/rockylinux/actions/workflows/build-and-push.yml/badge.svg)](https://github.com/vborodaykevych/rockylinux/actions/workflows/build-and-push.yml)
[![Docker Pulls](https://img.shields.io/docker/pulls/uacontainers/rockylinux.svg)](https://hub.docker.com/r/uacontainers/rockylinux)

## Overview

This repository automates the daily builds of **Rocky Linux** Docker images, ensuring they are always up-to-date with the latest security patches and updates. Unlike the [official Rocky Linux Docker repository](https://hub.docker.com/_/rockylinux), which may have outdated images vulnerable to security issues, these images are rebuilt every day to provide a secure and reliable container base.

## Key Features

- **Daily Builds**: Automated builds ensure the images are up-to-date with the latest patches and fixes.
- **Multiarch Support**: Includes support for `amd64`, `arm64`, `ppc64le`, and `s390x` architectures.
- **Variants**: Offers both `base` and `minimal` variants, with an additional `nonroot` security option.
- **Optimized for Security**: Images are rebuilt daily to include all security updates.
- **Simplified Structure**: Final images are based on `scratch` with a minimal filesystem (`layer.tar.xz`) for improved performance and security.

## Tags and Variants

The following tags and variants are supported:

### Variants:
- `base`: The standard full-featured image.
- `minimal`: A slimmed-down version of the image with essential components only.
- `nonroot`: Security-focused images where processes run as non-root.

### Example Tags:
- `latest`: Base image with the latest updates.
- `9`: Base image for Rocky Linux version 9.
- `<MINOR_VERSION>`: Specific minor version tag (e.g., `9.5`).
- `latest-minimal`, `9-minimal`, `<MINOR_VERSION>-minimal`: Corresponding minimal variants.
- `amd64`, `arm64`, `ppc64le`, `s390x`: Architecture-specific tags.

## Getting Started

Pull the desired image from Docker Hub:

```bash
# Pull the latest base image
docker pull uacontainers/rockylinux:latest

# Pull a minimal image for arm64 architecture
docker pull uacontainers/rockylinux:arm64-minimal

# Pull a nonroot image for ppc64le
docker pull uacontainers/rockylinux:ppc64le-nonroot
```

## Usage

Run a container using the pulled image:

```bash
docker run --rm -it uacontainers/rockylinux:latest
```

Or, for minimal and nonroot images:

```bash
docker run --rm -it uacontainers/rockylinux:minimal-nonroot
```

## Architecture Support

The following architectures are supported:
- **amd64** (x86_64)
- **arm64** (ARMv8)
- **ppc64le** (IBM POWER8/9)
- **s390x** (IBM Z)

## Build Workflow

The GitHub Actions workflow automates:
1. **Building Architecture-Specific Images**:
   - Builds images for each architecture, variant, and security mode.
2. **Extracting Filesystem**:
   - Extracts the filesystem from intermediate images and compresses it for final builds.
3. **Inspecting Version**:
   - Reads the Rocky Linux version (`MINOR_VERSION`) from the built image.
4. **Creating and Pushing Manifests**:
   - Combines architecture-specific images into multiarch manifests for Docker Hub.

The full workflow file is available in the repository: [build-and-push.yml](.github/workflows/build-and-push.yml).

## Contributing

We welcome contributions to improve these images or workflows. Please follow these steps:
1. Fork the repository.
2. Create a feature branch.
3. Submit a pull request.

## Licensing

This repository is licensed under the [MIT License](LICENSE).
