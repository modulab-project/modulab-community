# modulab-community

Community module discovery index for ModuLab Core (https://modulab.app).

## What is this?

This repository is the discovery index for community-maintained ModuLab modules. It does not contain module source code or container images, only a manifest.yaml "business card" per module, pointing to the module's actual repository and release. ModuLab Core periodically syncs this repository to populate the in-app module store (specification section 4.10).

## Structure

The repository contains one subdirectory per module, named after the module's name field with the modulab-mod- prefix removed, and each subdirectory contains a single manifest.yaml.

## Adding your module

See CONTRIBUTING.md for the full process.

## Licensing note

This index and its manifest.yaml entries are released under CC0 (public domain), see LICENSE. This applies only to the metadata in this repository. Each listed module retains its own license, as declared in its manifest.yaml license field (SPDX identifier). Listing here does not imply any change of ownership or licensing of the referenced module.

## Related repositories

modulab-core (https://github.com/modulab-project/modulab-core) is the Core backend and frontend. modulab-modules (https://github.com/modulab-project/modulab-modules) holds the official modules. modulab-module-sdk (https://github.com/modulab-project/modulab-module-sdk) is the module starter kit. modulab-manifest-schema (https://github.com/modulab-project/modulab-manifest-schema) defines the manifest.yaml JSON schema. modulab-docs (https://github.com/modulab-project/modulab-docs) holds the specification. modulab.app (https://github.com/modulab-project/modulab.app) is the landing page.
