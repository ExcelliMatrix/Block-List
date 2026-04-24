# EiM Block Lists

ExcelliMatrix maintained block lists for use with pfBlockerNG and similar DNS filtering tools.

These lists are intended to provide a conservative business-focused starting point for managed client environments. The initial focus is on blocking categories that are commonly unnecessary or undesirable on business networks, such as gaming, gambling, torrenting, tunneling, anonymization, and high-distraction social or entertainment platforms.

Adult-content domains are intentionally excluded from this repository.

## Purpose

The purpose of this repository is to provide ExcelliMatrix with a centralized, version-controlled location for maintaining DNS block lists that can be used across internal and client firewall deployments.

Using GitHub allows ExcelliMatrix to:

- Maintain a clear revision history
- Review changes before they are deployed
- Roll back problematic entries if needed
- Use raw file URLs directly in pfBlockerNG
- Maintain separate lists for different blocking categories or client needs

## Repository Structure

Recommended structure:

```text
EiM-Block-Lists
├── README.md
└── dnsbl
    └── EiM-Block-List.txt
```

## Available Lists

### `dnsbl/EiM-Block-List.txt`

General business-focused DNS block list.

This list is intended to include domains that are usually not required in professional business environments and may introduce productivity, security, or support concerns.

Current intended categories include:

- Social and entertainment platforms
- Gaming platforms and gaming communities
- Gambling and sports betting
- Torrent and piracy-related destinations
- Crypto mining and crypto utility services
- Tunneling, anonymization, and commonly abused paste services

## List Format

The block list uses a simple one-domain-per-line format.

Example:

```text
example.com
example.net
example.org
```

Comments may be included by starting the line with `#`.

Example:

```text
# Gaming platforms
roblox.com
minecraft.net
```

Blank lines are allowed and may be used for readability.

## pfBlockerNG Usage

In pfBlockerNG, use the raw GitHub URL for the list.

Example raw URL:

```text
https://raw.githubusercontent.com/ExcelliMatrix/EiM-Block-Lists/main/dnsbl/EiM-Block-List.txt
```

This URL can be added as a DNSBL feed in pfBlockerNG.

## Recommended pfBlockerNG Feed Settings

Recommended starting point:

```text
Format: Auto
State: ON
Action: Unbound
Update Frequency: Daily
```

Client environments may vary. Review each deployment before enabling the list globally.

## Important Review Notes

This list should be treated as a business-policy block list, not a complete security threat intelligence feed.

For known malicious domains, phishing domains, malware command-and-control infrastructure, and other active threats, pfBlockerNG should also use reputable maintained threat intelligence feeds.

This ExcelliMatrix list is intended to cover domains that may be inappropriate, unnecessary, distracting, risky, or commonly abused in business networks.

## Client-Specific Considerations

Not every domain in this list will be appropriate for every client.

Examples:

- A bank may reasonably block social media, gaming, gambling, torrenting, and tunneling services.
- A marketing company may need access to social media platforms.
- A software development client may need access to services such as tunneling tools or paste services.
- A manufacturing client may have less need for public collaboration platforms but may require vendor-specific cloud services.

Client-specific exceptions should be handled in pfBlockerNG using allow lists, client-specific feeds, or separate policy groups.

## Suggested Future List Separation

As the repository grows, the list may be split into separate category-specific files.

Possible future structure:

```text
dnsbl
├── EiM-Block-List-Core.txt
├── EiM-Block-List-Social.txt
├── EiM-Block-List-Gaming.txt
├── EiM-Block-List-Gambling.txt
├── EiM-Block-List-Torrent.txt
├── EiM-Block-List-Crypto.txt
└── EiM-Block-List-Tunneling.txt
```

This would allow ExcelliMatrix to apply different list combinations depending on the client’s business requirements.

## Change Management

Recommended change process:

1. Add or remove domains in a working branch.
2. Review the purpose of each change.
3. Confirm the domain does not have a legitimate business use for affected clients.
4. Merge the change into the main branch.
5. Allow pfBlockerNG to update on its regular schedule.
6. Monitor for client impact.

For urgent changes, pfBlockerNG may be manually updated after the repository change is published.

## Entry Guidelines

Before adding a domain, consider the following:

- Does the domain create a reasonable business risk?
- Is the domain commonly unnecessary in managed business environments?
- Could blocking the domain interfere with a legitimate business workflow?
- Should the domain belong in a client-specific list instead of the shared list?
- Is the domain already covered by a stronger third-party security feed?

Avoid adding domains solely because they are annoying, unpopular, or personally undesirable. The list should stay practical, defensible, and business-focused.

## Allow List Guidance

If a domain must be allowed for a specific client, prefer handling the exception in pfBlockerNG rather than removing the domain from the shared list.

Examples of possible client-specific exceptions:

```text
discord.com
ngrok.io
pastebin.com
tiktok.com
```

The appropriate decision depends on the client’s business model, risk tolerance, and support requirements.

## Disclaimer

This repository is provided for operational use by ExcelliMatrix and its managed client environments.

Blocking domains can affect business workflows. Review and test before applying broadly.

ExcelliMatrix may revise, reorganize, or remove entries as business requirements change.