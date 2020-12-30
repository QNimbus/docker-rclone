# docker-rclone <!-- omit in toc -->

## Table of contents <!-- omit in toc -->

- [About](#about)
- [Changelog](#changelog)
  - [Troubleshooting](#troubleshooting)
  - [Unreleased](#unreleased)
  - [0.0.1](#001---2020-12-30)

# About

This repository contains several Docker images related to the [`rclone`](https://rclone.org/) utility.

# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## Troubleshooting

When running the docker commands from a Windows Git Bash shell (MSYS) you may need to prepend the `MSYS_NO_PATHCONV=1` environment variable to the commands like so:

```bash
MSYS_NO_PATHCONV=1 docker run --rm -it -v ${PWD}/downloads:/downloads qnimbus/youtube-dl --version
```

## [Unreleased]

## [0.0.1] - 2020-12-30
### Added
- Initial version of `docker-rclone` repository

[Unreleased]: https://github.com/olivierlacan/keep-a-changelog/compare/v1.0.0...HEAD
[0.0.1]: https://github.com/olivierlacan/keep-a-changelog/releases/tag/v0.0.1
