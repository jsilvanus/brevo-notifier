# brevo-notifier

Small repo that sends Brevo transactional emails and SMS based on a simple configuration mapping.

## Usage (CLI)

Set required env vars and run:

```bash
export BREVO_API_KEY=...
export BREVO_SENDER_EMAIL=alerts@example.com
export BREVO_SENDER_NAME="My Alerts"
export INPUT_REPOSITORY="your repo path"
export THRESHOLD=critical
export USAGE_PERCENT=87
export REMAINING_EMAILS=13
export REMAINING_SMS=5
export NOTIFY_CONFIG=.github/brevo-notify.json
node send-alert.js
```

## Action usage

This repo also exposes a simple JS action (`action.yml`) which can be used from other workflows:

```yaml
- name: Notify via Brevo
  uses: jsilvanus/brevo-notifier@main
  with:
    threshold: ${{ steps.check.outputs.thresholdTriggered }}
    usagePercent: ${{ steps.check.outputs.usagePercent }}
    remainingEmails: ${{ steps.check.outputs.remainingEmails }}
    remainingSMS: ${{ steps.check.outputs.remainingSMS }}
    notify_config: .github/brevo-notify.json
  env:
    BREVO_API_KEY: ${{ secrets.BREVO_API_KEY }}
    BREVO_SENDER_EMAIL: ${{ secrets.BREVO_SENDER_EMAIL }}
    BREVO_SENDER_NAME: ${{ secrets.BREVO_SENDER_NAME }}
```

## Configuration

Create `.github/brevo-notify.json` in the consuming repo. Example:

```json
{
  "warning": { "channels": ["email"], "recipients": ["devops@example.com"] },
  "critical": { "channels": ["email","sms"], "recipients": ["devops@example.com","+15551234567"] }
}
```

## Notes

- This repo is intentionally focused solely on delivery; keep quota-checking logic in the other repository (jsilvanus/brevo-checker)

## Copyright and License

Copyright (c) Juha Itäleino, 2026.

License: MIT
