# UltimateDNSBlockList

**Comprehensive, automatically updated DNS blocklist for ad blocking, tracker prevention, and malware protection.**

![GitHub last commit](https://img.shields.io/github/last-commit/resname/BigBlockList)
![GitHub license](https://img.shields.io/github/license/resname/BigBlockList)

## Overview

**UltimateDNSBlockList** is a continuously updated aggregation of trusted, high-quality DNS blocklists designed for use with **Pi-hole**, **AdGuard Home**, **NextDNS**, **Control D**, and any other DNS sinkhole that accepts host-file or plain-text list formats.

It delivers network-wide protection against **ads, trackers, malicious domains, and telemetry** while preserving full functionality across websites, mobile apps, and smart devices.

### Design Principles

Effective DNS-level protection should not degrade the browsing experience. Every source included in this list is selected for its low false-positive rate and proven reliability, so the end result is a single, maintainable blocklist that works out of the box with no manual tuning required.

## Sources

This list aggregates the following well-established upstream providers:

| Source | Description | Report Issues |
|--------|-------------|---------------|
| [AdGuard DNS Filter](https://adguardteam.github.io/AdGuardSDNSFilter/Filters/filter.txt) | Composite filter combining AdGuard Base, Social Media, Tracking Protection, Mobile Ads, EasyList, and EasyPrivacy — optimized for DNS-level blocking. | [Report](https://reports.adguard.com/en/new_issue.html) |
| [OISD Big](https://big.oisd.nl) | Large community-maintained blocklist focused on accurate ad and tracker blocking without disrupting legitimate services. | [Report](https://oisd.nl/report) |
| [HaGeZi DNS Rebind Protection](https://raw.githubusercontent.com/hagezi/dns-blocklists/refs/heads/main/adguard/dns-rebind-protection.txt) | Specialized security list that protects local networks against DNS rebinding attacks. | [Report](https://github.com/hagezi/dns-blocklists/issues) |

## Update Frequency

The list is rebuilt and published **every hour** to ensure timely coverage of newly registered tracking and malware domains.

## Quick Start

Add the following URL to your DNS blocker's subscription list:

```
https://raw.githubusercontent.com/resname/UltimateDNSBlockList/refs/heads/main/list/UltimateDNSBlockList.txt
```

**Compatible with:** Pi-hole (Adlists), AdGuard Home (DNS blocklists), NextDNS, Control D, and any DNS-level blocker that supports host-file or plain-text formats.

## Contributing

- **Domain submissions** — Report new ad or tracking domains directly to the upstream providers listed above. This project aggregates existing lists and does not maintain custom block entries.
- **False positives** — If a domain is incorrectly blocked, report it to the relevant upstream provider so the fix propagates to all downstream consumers.
- **Source recommendations** — Know of a high-quality, low-false-positive list that belongs here? Open an [issue](../../issues) or submit a pull request.
