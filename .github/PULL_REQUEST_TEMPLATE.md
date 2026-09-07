## Summary

Provide a concise, mechanism-first explanation of what this pull request changes and why.

## Motivation & Context

What issue, limitation, or requirement does this address? (Link related issues using `#issue_number`).

## Changes Proposed

- List bulleted changes here
- Include any protocol, schema, or API modifications

## Impacted Components

- [ ] `@weavetab/mcp` (Core Server / CDP Engine)
- [ ] `@weavetab/sdk` (Plugin SDK & Types)
- [ ] `@weavetab/skills` (Operational Guidance)
- [ ] `Studio` / Workspace
- [ ] Companion Extension
- [ ] Documentation / Website

## Verification & Testing

Explain how these changes were tested and verified:

```bash
# Provide reproduction or test commands executed
npm test
npm run verify
```

- [ ] Verified locally against live Chromium instances (Chrome / Edge / Brave)
- [ ] Verified latency impact (sub-10ms dispatch preserved)
- [ ] Automated tests added or updated

## Engineering Checklist

- [ ] My code adheres to the project's TypeScript and lint standards.
- [ ] I have verified documentation matches runtime implementation (no doc drift).
- [ ] Breaking changes are explicitly highlighted and justified below.
- [ ] No sensitive credentials, secrets, or unmasked logs are committed.

## Breaking Changes

If this introduces a breaking change (API, schema, or protocol level), describe the migration path:
