# Catalyst Center Configuration as Code

This repository stores exported Cisco Catalyst Center configuration captured through the Catalyst Center IaC MCP server.

## Layout

```text
data/
  iac2/
    *.yaml
reports/
  scale-test-summary.csv
  scale-test-summary.xlsx
metadata/
  export-run.json
```

## Rules

- Store only sanitized configuration outputs and scale-test reports.
- Do not commit MCP server artifacts, raw logs, credentials, API keys, certificates, or local setup notes.
- Keep one exported flow per file under `data/<cluster>/`.
