# UltimateDNSBlockList

**Comprehensive, automatically updated DNS blocklists for ad blocking, tracker prevention, and malware protection.**

![GitHub last commit](https://img.shields.io/github/last-commit/resname/UltimateDNSBlockList)
![GitHub license](https://img.shields.io/github/license/resname/UltimateDNSBlockList)

## Overview

**UltimateDNSBlockList** aggregates trusted, high-quality DNS blocklists into a single maintainable source you can subscribe to in **Pi-hole**, **AdGuard Home**, **NextDNS**, **Control D**, and any other DNS sinkhole that accepts plain-text or host-file entries.

The project currently publishes two variants:

- Full list — broad coverage for users who want maximum protection.
- Small list — lighter-weight protection focused on the most common ad, tracker, and malware domains.

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

## Upstream Sources

This project aggregates the following providers:

| Source | Description | Report Issues |
|--------|-------------|---------------|
| [OISD Big](https://big.oisd.nl) | Large community-maintained blocklist focused on accurate ad and tracker blocking without disrupting legitimate services. | [Report](https://oisd.nl/report) |
| [HaGeZi Multi Normal](https://gitlab.com/hagezi/mirror/-/raw/main/dns-blocklists/adblock/multi.txt) | All-round protection list for ads, trackers, metrics, telemetry, phishing, malware, scams, fakes, cryptojacking, and similar junk. | [Report](https://github.com/hagezi/dns-blocklists/issues) |
| [OISD Small](https://small.oisd.nl) | A smaller, lower-noise version of the main OISD feed intended for leaner deployments. | [Report](https://oisd.nl/report) |
| [HaGeZi Light](https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/adblock/light.txt) | A lighter-weight blocklist optimized for broad protection without the full breadth of the large feed. | [Report](https://github.com/hagezi/dns-blocklists/issues) |

## Update Frequency

The generated lists are rebuilt on a schedule and published as needed to cover newly registered and newly observed malicious, tracking, or advertising domains.

- Full list: scheduled hourly at minute 25
- Small list: scheduled hourly at minute 55, 30 minutes after the full-list workflow
- Version metadata is stored in the repository and bumped each time a publish occurs

## How the Workflow Works

Each generated list goes through the same basic flow:

1. Download each upstream source listed in `sources.txt` or `sources-small.txt`
2. Remove duplicates across sources
3. Apply the repository allowlist to reduce false positives
4. Compare the resulting entries against the previous published output
5. Write a new header with version metadata and source attribution
6. Commit and push the updated list automatically

The GitHub Actions workflows live in `.github/workflows/` and are designed to run either on a schedule or manually via the Actions tab.


## Contributing

- **Domain submissions** — Report new ad or tracking domains directly to the upstream providers listed above. This project aggregates existing lists and does not maintain custom domain entries.
- **False positives** — If a domain is incorrectly blocked, report it to the relevant upstream provider so the fix propagates to all downstream consumers.
- **Source recommendations** — Know of a high-quality, low-false-positive list that belongs here? Open an [issue](../../issues) or submit a pull request.
- **Workflow improvements** — If you want to improve the generation pipeline or add a new list variant, open a PR with the relevant workflow and source files.

## Repository Files

- `sources.txt` — upstream feeds for the full list
- `sources-small.txt` — upstream feeds for the small list
- `allowlist` — domains intentionally excluded from published output
- `version.txt` — current version for the full list
- `small-version.txt` — current version for the small list
- `list/UltimateDNSBlockList.txt` — generated full output
- `list/SmallDNSBlockList.txt` — generated small output
