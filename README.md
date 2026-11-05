# UltimateDNSBlockList

**Comprehensive, automatically updated DNS blocklists for ad blocking, tracker prevention, and malware protection.**

![GitHub last commit](https://img.shields.io/github/last-commit/resname/UltimateDNSBlockList)
![GitHub license](https://img.shields.io/github/license/resname/UltimateDNSBlockList)

## Overview

**UltimateDNSBlockList** aggregates trusted, high-quality DNS blocklists into a single maintainable source you can subscribe to in **Pi-hole**, **AdGuard Home**, **NextDNS**, **Control D**, and any other DNS sinkhole that accepts plain-text or host-file entries.

The project currently publishes four variants:

- Full list — broad coverage for users who want maximum protection.
- Small list — lighter-weight protection focused on the most common ad, tracker, and malware domains.
- NSFW list — blocks adult content.
- Small NSFW list — a smaller adult-content list for lighter-weight filtering.

The goal is to provide strong network-wide filtering without creating a heavy maintenance burden or relying on fragile custom rules.

### Design Principles

- High-quality upstream sources only
- Remove duplicate entries across upstream feeds
- Apply an allowlist to reduce false positives
- Rebuild automatically on a schedule
- Keep the published lists simple enough for any DNS sinkhole to consume

## Available Lists

### Full blocklist

This is the default, broad coverage list for most installations.

```text
https://raw.githubusercontent.com/resname/UltimateDNSBlockList/refs/heads/main/list/UltimateDNSBlockList.txt
```

**Recommended for most Pi-hole and AdGuard Home installations.** Choose the full list when you want the broadest coverage and your DNS blocker can comfortably handle a larger list.

**Memory guidance:** Reserve about **512 MB of available RAM** for the DNS filtering service when using this list. This is a conservative planning estimate, not a hard minimum or a measured requirement; actual use depends on the DNS blocker, other subscribed lists, and query volume.

### Small blocklist

This list is compiled from a lighter upstream subset and is intended for users who want a smaller, faster-to-sync list with less noise.

```text
https://raw.githubusercontent.com/resname/UltimateDNSBlockList/refs/heads/main/list/SmallDNSBlockList.txt
```

Choose the small list for a more conservative setup, a resource-constrained resolver, or when you prefer a smaller subscription. Subscribe to one variant rather than both; the full list already provides broader coverage, so combining them mostly adds redundant entries.

**Memory guidance:** Reserve about **256 MB of available RAM** for the DNS filtering service when using this list. This is a conservative planning estimate, not a hard minimum or a measured requirement; actual use depends on the DNS blocker, other subscribed lists, and query volume.

These figures refer to memory available to the DNS filtering service, in addition to what the operating system and other applications need. Check your installer's platform-specific requirements and monitor actual usage after adding the list.

### NSFW blocklist

This list blocks adult content. Use it only if you intend to filter that content.

```text
https://raw.githubusercontent.com/resname/UltimateDNSBlockList/refs/heads/main/list/NSFWBlockList.txt
```

### Small NSFW blocklist

This is a smaller alternative for adult-content filtering. Subscribe to one NSFW variant rather than both.

```text
https://raw.githubusercontent.com/resname/UltimateDNSBlockList/refs/heads/main/list/SmallNSFWBlockList.txt
```

## Update Frequency

All four lists are updated at least once every day.

## How the Workflow Works

Each generated list goes through the same basic flow:

1. Download each feed configured in the `Sources/` text files
2. Remove duplicates across sources
3. Apply the repository allowlist to reduce false positives
4. Compare the resulting entries against the previous published output
5. Write a new header with version metadata
6. Commit and push the updated list automatically

The GitHub Actions workflow lives in `.github/workflows/` and runs on a schedule or manually via the Actions tab. It publishes all four generated lists together in one commit when any list changes.


## Contributing

- **Domain submissions** — Report new ad or tracking domains directly to the relevant upstream maintainers. This project aggregates existing lists and does not maintain custom domain entries.
- **False positives** — If a domain is incorrectly blocked, report it to the relevant upstream maintainer so the fix propagates to all downstream consumers.
- **Source recommendations** — Know of a high-quality, low-false-positive list that belongs here? Open an [issue](../../issues) or submit a pull request.
- **Workflow improvements** — If you want to improve the generation pipeline or add a new list variant, open a PR with the relevant workflow and source files.

## Repository Files

- `Sources/` — text files containing the upstream feed URLs
- `allowlist` — domains intentionally excluded from published output
- `version.txt` — current version for the full list
- `small-version.txt` — current version for the small list
- `nsfw-version.txt` and `nsfw-small-version.txt` — current versions for the NSFW lists
- `list/UltimateDNSBlockList.txt` — generated full output
- `list/SmallDNSBlockList.txt` — generated small output
- `list/NSFWBlockList.txt` — generated NSFW output
- `list/SmallNSFWBlockList.txt` — generated small NSFW output
