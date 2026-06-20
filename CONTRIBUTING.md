# Contributing a module

Thanks for building a module for ModuLab! To get listed in the in-app module store, follow these steps.

## Step 1: Build your module

Use modulab-module-sdk (https://github.com/modulab-project/modulab-module-sdk) as a starting point. ModuLab modules are plugins, not containers, so your module must provide a valid manifest.yaml (validated against modulab-manifest-schema, https://github.com/modulab-project/modulab-manifest-schema), including tier, min_core_api and min_core_ui. It must implement no custom authentication, trusting the typed auth context Core passes into your handler (tier 2/3). It must declare all outbound connections in egress_allowlist (tier 3), which is enforced at runtime via Deno's --allow-net flag. Vendor any external dependencies your handler or jobs use (deno vendor) into a vendor/ directory in your package, since Core runs handlers with --cached-only and unvendored runtime fetches simply fail. The module must be packaged as a module.zip (manifest.yaml plus migrations/, ui/, handlers/, jobs/, i18n/, see the modulab-module-sdk README) and attached to a GitHub Release, and must use the namespace modulab-mod-{name} (specification section 4.1).

## Step 2: Add a discovery entry

Open a pull request that adds a new directory named after your module (without the modulab-mod- prefix), containing a single manifest.yaml. That manifest.yaml must additionally include the fields source_repo, manifest_path, and release_url, pointing at your module's own repository, the path to its manifest.yaml, and the module.zip attached to your latest GitHub Release. This copy serves only as the initial discovery entry. When a user installs the module, ModuLab Core fetches the module.zip from release_url directly, so keep your GitHub Releases up to date.

## Step 3: Automated checks

Every PR is automatically validated against the JSON schema in modulab-manifest-schema (https://github.com/modulab-project/modulab-manifest-schema) via GitHub Actions. PRs that fail validation cannot be merged.

## Step 4: Review

At least one maintainer review is required before merging. We check for a valid and complete manifest.yaml (required fields, a valid SPDX license identifier, a plausible egress_allowlist and requested_scopes), a reachable source_repo with a matching manifest.yaml, a working module.zip at the declared release_url with a vendor/ directory if external packages are used, and no obviously suspicious patterns in ui/bundle.js or handlers/*.ts such as obfuscation, eval, or dynamic imports bypassing vendor/. Signing your release with cosign sign-blob is optional but recommended: signed community modules are marked as verified in the module store, unsigned ones are marked checksum-only. Official modules in modulab-modules require signing.

## Updating your listing

To update version, description, or other fields, open a PR updating your manifest.yaml entry, or simply publish a new GitHub Release; Core picks up new release_url versions automatically on the next sync.

## Removing your listing

Open a PR removing your module's directory.
