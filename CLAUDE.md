# globalsoc

Security operations content for Microsoft security tooling (Defender for Endpoint, Sentinel, Azure Firewall) and related sources such as Cisco FTD.

## Standing instruction from the repo owner

Whenever a conversation produces something reusable for Microsoft security (KQL hunting queries, Sentinel analytics rules, workbooks, playbooks, Defender/Intune/Entra configuration, detection notes), proactively suggest committing it to this repo.

## Layout

- `hunting/<topic>/` — KQL hunting queries, one query per `.kql` file, with a README listing platform, purpose and known gaps.
- Query file names are prefixed by source: `mde-`, `azfw-`, `ftd-`, numbered within each topic.
- Each `.kql` starts with comment lines naming the platform (MDE Advanced Hunting vs Sentinel) and caveats.
