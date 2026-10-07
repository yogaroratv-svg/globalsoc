# Claude / Anthropic AI usage hunting

KQL hunting queries to find Claude tooling (website, Chrome extension, Claude Code, `claude rc` Remote Control, Claude Desktop) across endpoints and firewalls.

> Not yet validated against a live tenant. Run each over a short time range first and adjust column names to your connectors.

| File | Platform | Finds |
|---|---|---|
| `mde-01-claude-process-execution.kql` | MDE (Sentinel: `Timestamp` → `TimeGenerated`) | Installs, Claude Code runs, Remote Control, Desktop |
| `mde-02-claude-code-child-commands.kql` | MDE / Sentinel | Commands Claude Code executed |
| `mde-03-claude-network-by-process.kql` | MDE / Sentinel | Claude connections per device and process |
| `mde-04-claude-browser-extension-inventory.kql` | MDE Advanced Hunting only | Installed Claude (and look-alike) browser extensions |
| `azfw-01-application-rule.kql` | Sentinel (`AZFWApplicationRule`) | Azure Firewall application-rule hits |
| `azfw-02-dns-query.kql` | Sentinel (`AZFWDnsQuery`) | DNS lookups via firewall DNS proxy |
| `azfw-03-azurediagnostics-legacy.kql` | Sentinel (`AzureDiagnostics`) | Same as azfw-01, legacy schema |
| `ftd-01-commonsecuritylog.kql` | Sentinel (`CommonSecurityLog`) | Cisco FTD traffic (domain, then IP fallback) |

## Known gaps

- **Renamed binaries** evade file-name matching (mde-01/02); network and signer/hash checks are harder to dodge.
- **IP-based FTD matching** can false-positive on CDN-shared IPs.
- **No TLS inspection** → domain only, no URL path or content.
- **Personal hotspot** bypasses both firewalls; only MDE still sees activity.
- **WSL** usage needs the Defender for Endpoint WSL plug-in for full visibility.
- **Domain list** is a starting point; extend from mde-03 results.
- Monitoring individuals' activity may be subject to HR / privacy rules — get the hunt approved.
