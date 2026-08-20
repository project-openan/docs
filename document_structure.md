# Document Structure

## Introduction

This document describes the production workflow and repository structure of OpenAN documentation, and provides the specific location of each manual within the documentation repository.

- Document Production:
    - OpenAN documentation is produced in the [OpenAN/docs repository](https://github.com/project-openan/docs) and the `docs` folders of individual code repositories.
    - Project-level documentation: Quick Start, Release Notes, Security Technical White Paper, etc., are stored in the [OpenAN/docs repository](https://github.com/project-openan/docs) and maintained by the docs project team.
    - Module documentation: e.g., registry-center, orchestration-center, etc. The respective project teams own and maintain these documents, which are stored in the `docs` folder of each module's code repository.

```text
├─docs     
│  ├─en    <!-- English documentation -->
│  └─zh    <!-- Chinese documentation -->
```

## Document Locations

OpenAN documentation is stored in the [OpenAN/docs](https://github.com/project-openan/docs) repository and the source code repositories of each module project team. The table below lists the specific location of each manual.

| Document | Repository | Location |
| ---- | ---- | ---- |
| Quick Start, Security Technical White Paper, Release Notes | docs | [Link](https://github.com/project-openan/docs) |
| Registry Center User Guide, Development Guide, API Reference, GCP Containerized Deployment Guide, Security Capability Guide | registry-center | [Link](https://github.com/project-openan/registry-center/tree/main/docs) |
| Orchestration Center User Guide, Development Guide, API Reference, GCP Containerized Deployment Guide | orchestration-center | [Link](https://github.com/project-openan/orchestration-center/tree/main/docs) |
| a2a-t-sdk-python User Guide, Development Guide | a2a-t-sdk-python | [Link](https://github.com/project-openan/a2a-t-sdk-python/tree/main/docs) |
| a2a-t-sdk-java User Guide, Development Guide | a2a-t-sdk-java | [Link](https://github.com/project-openan/a2a-t-sdk-java/tree/main/docs) |
