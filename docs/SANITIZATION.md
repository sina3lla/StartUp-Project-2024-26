# Repository sanitization

On 23 October 2026, all four preserved branch histories were rewritten to remove identified personal and deployment details.

- Contributor names and email addresses in commit metadata are anonymized.
- Personal names, postal addresses, personal email addresses, and personal-domain references in tracked files are replaced with placeholders.
- Personal biography content in the older website is removed.
- Cloudflare account/tunnel identifiers, the deployed worker URL, and a workstation username are replaced with deployment placeholders.
- FeelY branding and service contact addresses remain. Test credentials and example values are not live credentials.

## Using this archive

Clone the repository again after the rewrite. Do not merge or push pre-cleanup history back into it.

Deployment examples must be configured locally with your own values. Keep secrets outside Git. Anonymized legal documents are reference material, not deployable legal terms: their bytes and hashes have changed, and any deployment must publish a new reviewed terms version rather than reuse prior acceptance records.

The cleanup changes repository history; it does not revoke credentials or erase copies in other repositories, existing clones, downloads, or hosting-provider caches. Automated scanning cannot guarantee the absence of every possible secret. No recognized live API credentials were detected by the audit.
