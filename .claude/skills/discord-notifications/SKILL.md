---
name: discord-notifications
description: Send notifications to Discord channels using webhooks. Documents environment variables and provides examples for simple messages, formatted embeds, and error handling.
---

# Discord Notifications Skill

Send notifications to Discord channels using webhooks.

## Environment Variables

- `DISCORD_WEBHOOK_URL` - The Discord webhook URL for sending notifications
- `DISCORD_WEBHOOK_URL_IMPORTANT` - Alternative webhook URL for important/critical notifications

## Basic Usage

Send a simple notification:

```bash
curl -X POST "$DISCORD_WEBHOOK_URL" \
  -H "Content-Type: application/json" \
  -d '{"content": "Your message here"}'
```

## Formatted Messages

Send a formatted message with embeds:

```bash
curl -X POST "$DISCORD_WEBHOOK_URL" \
  -H "Content-Type: application/json" \
  -d '{
    "embeds": [{
      "title": "Notification Title",
      "description": "Your message description",
      "color": 5814783,
      "fields": [
        {
          "name": "Field Name",
          "value": "Field Value",
          "inline": false
        }
      ]
    }]
  }'
```

## Color Codes

Common Discord embed colors:
- Green (success): `3066993`
- Yellow (warning): `16776960`
- Red (error): `15158332`
- Blue (info): `3447003`
- Purple: `10181046`

## Examples

### Simple notification
```bash
curl -X POST "$DISCORD_WEBHOOK_URL" \
  -H "Content-Type: application/json" \
  -d "{\"content\": \"Claude is starting work on issue #123\"}"
```

### Status notification
```bash
curl -X POST "$DISCORD_WEBHOOK_URL" \
  -H "Content-Type: application/json" \
  -d '{
    "embeds": [{
      "title": "Task Started",
      "description": "Beginning work on repository health audit",
      "color": 3447003,
      "timestamp": "'$(date -u +%Y-%m-%dT%H:%M:%S)'.000Z"
    }]
  }'
```

### Critical alert
```bash
curl -X POST "$DISCORD_WEBHOOK_URL_IMPORTANT" \
  -H "Content-Type: application/json" \
  -d '{
    "embeds": [{
      "title": "⚠️ Critical Issue Detected",
      "description": "Pausing machine due to repeated workflow violations",
      "color": 15158332,
      "fields": [
        {
          "name": "Machine ID",
          "value": "'"$FLY_MACHINE_ID"'",
          "inline": true
        },
        {
          "name": "Repository",
          "value": "'"$GIT_REPOSITORIES"'",
          "inline": true
        }
      ],
      "timestamp": "'$(date -u +%Y-%m-%dT%H:%M:%S)'.000Z"
    }]
  }'
```

## Error Handling

Add error handling to ensure notifications don't fail silently:

```bash
if ! curl -X POST "$DISCORD_WEBHOOK_URL" \
  -H "Content-Type: application/json" \
  -d '{"content": "Message"}' \
  --silent --show-error --fail; then
  echo "Warning: Failed to send Discord notification" >&2
fi
```

## Best Practices

1. **Use appropriate webhook URLs**: Use `DISCORD_WEBHOOK_URL` for routine notifications and `DISCORD_WEBHOOK_URL_IMPORTANT` for critical alerts
2. **Include context**: Add relevant information like machine ID, repository, or issue number
3. **Handle failures gracefully**: Don't let notification failures stop the main workflow
4. **Use embeds for structured data**: Embeds provide better formatting and more information
5. **Add timestamps**: Include timestamps in embeds for better tracking
