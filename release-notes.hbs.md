# Tanzu Application Platform release notes

This topic contains release notes for Tanzu Application Platform v{{ vars.url_version }}.

{{#unless vars.hide_content}}

This Handlebars condition is used to hide content.

In release notes, this condition hides content that describes an unreleased patch for a released minor.

{{/unless}}

## <a id='1-6-0'></a> v1.6.0

**Release Date**: 11 July 2023

### <a id='1-6-0-whats-new'></a> What's new in Tanzu Application Platform

This release includes the following platform-wide enhancements.

#### <a id='1-6-0-new-platform-features'></a> New platform-wide features

- Feature Description.

#### <a id='1-6-0-new-components'></a> New components

- [COMPONENT-NAME-AND-LINK-TO-DOCS](): Component description.

---

### <a id='1-6-0-new-features'></a> New features by component and area

This release includes the following changes, listed by component and area.

#### <a id='1-6-0-flux-sc'></a> FluxCD Source Controller

Flux Source Controller *v0.36.1-build.2* release brings several API changes we want to highlight here.

- `GitRepository` API

  - Field `spec.ref.name` is the reference value for git check out. It takes precedence over Branch,
  Tag and SemVer. It must be a valid 
  [Git reference](https://git-scm.com/docs/git-check-ref-format#_description). 
  Examples: 
    - "refs/heads/main" 
    - "refs/tags/v0.1.0"
    - "refs/pull/420/head"
    - "refs/merge-requests/1/head".
  - Field `status.artifact.digest` represents the value of the file in the form of `<algorithm>:<checksum>`.
  - Field `status.observedIgnore` represents the latest `spec.ignore` value. It indicates the ignore
  rules used in building the current artifact in storage.
  - Field `status.observedRecurseSubmodules` represents the latest `spec.recurseSubmodules` value 
  during the latest reconciliation.
  - Field `status.observedInclude` represent the list of `GitRepository` resources used to produce
  the current artifact.

- `OCIRepository` API
  - Field `spec.layerSelector` specifies which layer should be extracted from an OCI Artifact.
  This field is optional and defaults to extracting the first layer in the artifact.
  - Field `spec.verify` contains the secret name containing the trusted public keys used to verify
  the signature and specifies which provider to use to check whether OCI image is authentic.
  - Field `spec.insecure` allows connecting to a non-TLS HTTP container registry.

- `HelmChart` API
  - Added new field `spec.verify`. It contains the secret name containing the trusted public keys
  used to verify the signature and specifies which provider to use to check whether OCI image is
  authentic. This field is only supported when using HelmRepository source with `spec.type` *oci*.
  Chart dependencies, which are not bundled in the umbrella chart artifact, are not verified.

- `HelmRepository` API
  - Added new field `spec.provider`. It is used for authentication purposes. Supported values are 
  `aws, azure, gcp or generic`.
  Default is `generic`. This field is only taken into account if the `.spec.type` field is set to *oci*

- `Bucket` API
  - Added new field `status.observedIgnore`. It represents the latest `spec.ignore` value.
  It indicates the ignore rules used in building the current artifact in storage.

#### <a id='1-6-0-appsso'></a> Application Single Sign-On (AppSSO)

- Incorporate the token expiry settings into the `AuthServer` resource.
  Service operators can customize the expiry settings of access, refresh or
  identity token.
  For more information, see [Token settings](app-sso/service-operators/token-settings.hbs.md#token-expiry-settings).

---

### <a id='1-6-0-breaking-changes'></a> Breaking changes

This release includes the following changes, listed by component and area.

#### <a id='1-6-0-COMPONENT-NAME-bc'></a> COMPONENT-NAME

- Breaking change description.

#### <a id='1-6-0-appsso-bc'></a> Application Single Sign-On (AppSSO)

- Remove the field `AuthServer.spec.tls.disabled` and use `AuthServer.spec.tls.deactivated` instead.

#### <a id='1-6-0-flux-sc-bc'></a> FluxCD Source Controller

- `GitRepository` resource status field `status.artifact.revision` value format changed
from `<branch>/<checksum>` to `<branch>@sha1:<checksum>`. 
  - Example `main/6db88c7a7e7dec1843809b058195b68480c4c12a` to `main@sha1:6db88c7a7e7dec1843809b058195b68480c4c12a`.

---

### <a id='1-6-0-security-fixes'></a> Security fixes

This release has the following security fixes, listed by component and area.

#### <a id='1-6-0-COMPONENT-NAME-fixes'></a> COMPONENT-NAME

- Security fix description.

---

### <a id='1-6-0-resolved-issues'></a> Resolved issues

The following issues, listed by component and area, are resolved in this release.

#### <a id='1-6-0-COMPONENT-NAME-ri'></a> COMPONENT-NAME

- Resolved issue description.

---

### <a id='1-6-0-known-issues'></a> Known issues

This release has the following known issues, listed by component and area.

#### <a id='1-6-0-tap-gui-ki'></a> Tanzu Application Platform GUI

- Ad-blocking browser extensions and standalone ad-blocking software can interfere with telemetry
  collection within the VMware
  [Customer Experience Improvement Program](https://www.vmware.com/solutions/trustvmware/ceip.html)
  and restrict access to all or parts of Tanzu Application Platform GUI.
  For more information, see [Troubleshooting](tap-gui/troubleshooting.hbs.md#ad-block-interference).

---

## <a id='1-6-deprecations'></a> Deprecations

The following features, listed by component, are deprecated.
Deprecated features will remain on this list until they are retired from Tanzu Application Platform.

### <a id="1-6-alv-deprecations"></a> Application Live View

- `appliveview_connnector.backend.sslDisabled` is deprecated and marked for removal in
  Tanzu Application Platform v1.7.0.
  For more information about the migration, see [Deprecate the sslDisabled key](app-live-view/install.hbs.md#deprecate-the-ssldisabled-key).

### <a id='1-6-app-sso-deprecations'></a> Application Single Sign-On (AppSSO)

- `ClientRegistration` resource `clientAuthenticationMethod` field values `post` and `basic` are
  deprecated and marked for removal in Tanzu Application Platform v1.7.0.
  Use `client_secret_post` and `client_secret_basic` instead.

- `AuthServer.spec.tls.disabled` is deprecated and marked for removal in Tanzu Application Platform v1.6.0.
  For more information about how to migrate to `AuthServer.spec.tls.deactivated`, see
  [Migration guides](app-sso/upgrades/index.md#migration-guides).

### <a id="1-6-0-stk-deprecations"></a> Services Toolkit

- The `tanzu services claims` CLI plug-in command is now deprecated. It is
  hidden from help text output, but continues to work until officially removed
  after the deprecation period. The new `tanzu services resource-claims` command
  provides the same function.

### <a id="1-6-scst-scan-deprecations"></a> Supply Chain Security Tools (SCST) - Scan

- The `docker` field and related sub-fields used in SCST -
  Scan are deprecated and marked for removal in Tanzu Application Platform
  v1.7.0.

   The deprecation impacts the following components: Scan Controller, Grype Scanner, and Snyk Scanner.
   Carbon Black Scanner is not impacted.
   For information about the migration path, see
   [Troubleshooting](scst-scan/observing.hbs.md#unable-to-pull-scanner-controller-images).

### <a id="1-6-tbs-deprecations"></a> Tanzu Build Service

- The Ubuntu Bionic stack is deprecated: Ubuntu Bionic stops receiving support in April 2023.
  VMware recommends you migrate builds to Jammy stacks in advance.
  For how to migrate builds, see [Use Jammy stacks for a workload](tanzu-build-service/dependencies.md#using-jammy).

- The Cloud Native Buildpack Bill of Materials (CNB BOM) format is deprecated.
  VMware plans to deactivate this format by default in Tanzu Application Platform v1.5.0 and remove
  support in Tanzu Application Platform v1.6.0.
  To manually deactivate legacy CNB BOM support, see [Deactivate the CNB BOM format](tanzu-build-service/install-tbs.md#deactivate-cnb-bom).

### <a id="1-6-apps-plugin-deprecations"></a> Tanzu CLI Apps plug-in

- The default value for the
  [--update-strategy](./cli-plugins/apps/command-reference/workload_create_update_apply.hbs.md#update-strategy)
  flag will change from `merge` to `replace` in Tanzu Application Platform v1.7.0.

- The `tanzu apps workload update` command is deprecated and marked for removal
  in Tanzu Application Platform v1.6.0. Use the command `tanzu apps workload apply` instead.

### <a id="1-6-flux-sc"></a> FluxCD Source Controller

- `GitRepository` API

  - Field `spec.gitImplementation` is deprecated.
  GitImplementation specifies which Git client library implementation to use.
  `go-git` is the default and only supported implementation, `libgit2`
  is no longer supported.
  - Field `spec.accessFrom` is deprecated. AccessFrom specifies an Access Control List for allowing
  cross-namespace references to this object. It was never implemented.
  - Field `status.contentConfigChecksum` is deprecated in favor of explicit fields defined in the 
  observed artifact content config in the status.
  - Field `status.artifact.checksum` is deprecated in favor of the `status.artifact.digest`.
  - Field `status.url` is deprecated in favor of the `status.artifact.url`.

- `OCIRepository` API

  - Field `status.contentConfigChecksum` is deprecated in favor of explicit fields defined in the
  observed artifact content config in the status.


