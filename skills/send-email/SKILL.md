---
name: send-email
title: Send Email
category: communication
version: 1.0.0
---

# Send Email

## Description

Compose and send a plain-text or HTML email via SMTP.

## When to Use

- Automated notification workflows
- Agent needs to send a report or alert

## When NOT to Use

- Mass mailing (use dedicated email service with unsubscribe handling)
- Sending sensitive data — prefer secure channels

## Inputs

| Name | Type | Required | Description |
|------|------|---------|-------------|
| to | list | yes | Recipient email addresses |
| subject | string | yes | Email subject |
| body | string | yes | Plain text body |
| html_body | string | no | HTML version of body |
| smtp_host | string | yes | SMTP server |
| smtp_port | int | no | Default 587 |
| username | string | yes | SMTP username |
| password | string | yes | SMTP password (use env var) |

## Example

```python
import smtplib
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
import os

def send_email(to: list, subject: str, body: str, html_body: str = None) -> bool:
    smtp_host = os.environ["SMTP_HOST"]
    smtp_port = int(os.environ.get("SMTP_PORT", 587))
    username = os.environ["SMTP_USER"]
    password = os.environ["SMTP_PASS"]

    msg = MIMEMultipart("alternative")
    msg["From"] = username
    msg["To"] = ", ".join(to)
    msg["Subject"] = subject
    msg.attach(MIMEText(body, "plain"))
    if html_body:
        msg.attach(MIMEText(html_body, "html"))

    with smtplib.SMTP(smtp_host, smtp_port) as server:
        server.starttls()
        server.login(username, password)
        server.sendmail(username, to, msg.as_string())
    return True

# send_email(["alice@example.com"], "Report Ready", "Your weekly report is attached.")
```

## Security Notes

- Never hardcode credentials. Use environment variables or a secrets manager.
- Validate recipient addresses to prevent injection.
- Log sent emails for audit trail.
