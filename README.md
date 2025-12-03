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

### Rocky Linux 10 (default):
- `latest`, `10`, `10.x`: Base image with the latest updates.
- `latest-minimal`, `10-minimal`, `10.x-minimal`: Minimal variants.
- `nonroot`, `nonroot-minimal`: Non-root variants.
- `amd64`, `arm64`, `ppc64le`, `s390x`: Architecture-specific tags.
- `amd64-minimal`, `amd64-nonroot`, `amd64-minimal-nonroot`: Architecture + variant tags.

### Rocky Linux 9:
- `9`, `9.x`: Base image for Rocky Linux 9.
- `9-minimal`, `9.x-minimal`: Minimal variants.
- `9-amd64`, `9-arm64`, `9-ppc64le`, `9-s390x`: Architecture-specific tags.
- `9-amd64-minimal`, `9-amd64-nonroot`, `9-amd64-minimal-nonroot`: Architecture + variant tags.

## Getting Started

Pull the desired image from Docker Hub:

```bash
# Pull the latest base image (Rocky Linux 10)
docker pull uacontainers/rockylinux:latest

# Pull Rocky Linux 9
docker pull uacontainers/rockylinux:9

# Pull a minimal image
docker pull uacontainers/rockylinux:latest-minimal

# Pull a nonroot image
docker pull uacontainers/rockylinux:nonroot
```

## Usage

Run a container using the pulled image:

```bash
docker run --rm -it uacontainers/rockylinux:latest
```

Or, for minimal and nonroot images:

```bash
docker run --rm -it uacontainers/rockylinux:nonroot-minimal
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
