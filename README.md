# r.Potential for Claude

A Claude plugin that connects Claude to r.Potential's library of Units of
Potential (UoPs): AI opportunities sized for a specific company, each with a
modeled dollar range and the tasks that move to agents.

## What's included

- **The r.Potential connector** (`.mcp.json`), at
  `https://api.rpotential.ai/mcp/library/`. You sign in with your r.Potential
  account the first time Claude uses it.
- **Skills:**
  - `account-meeting-prep`: a five-minute brief before a meeting with a
    company. It combines r.Potential's UoPs and AI-hiring comparison with
    the relationship history from a CRM connector when one is on (for
    example Salesforce through the Salesforce connector).

## Requirements

- An r.Potential account. Ask your r.Potential contact for access.
- Optional: a CRM connector in Claude, such as Salesforce, for the
  relationship half of a brief. The skill only reads from it.

## Install

In Claude, add the plugin from the Plugins directory. Then try:

> Prep me for tomorrow's meeting with Northwind Traders.

## Privacy

The connector's privacy notice is at https://rpotential.ai/mcp/claude.

## Support

Questions: info@rpotential.ai. Security issues: see [SECURITY.md](SECURITY.md).
