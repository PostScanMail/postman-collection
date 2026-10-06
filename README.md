# Virtual Mailbox API (PostScan Mail) – Postman Collection

This repository provides the official Postman collection for the **PostScan Mail Virtual Mailbox API and Mail Scanning API**, allowing developers to receive, scan, manage, and automate physical mail digitally.

Get started in minutes and integrate real-world mail into your applications to build workflows around document handling, mail automation, and AI-powered mail insights.

---

## 🚀 What You Can Build

- Automate incoming mail processing for your business
- Sync scanned mail and documents to your CRM or database
- Build digital mailbox and virtual address workflows
- Trigger workflows when new mail arrives
- Request supported mail item actions programmatically
- Enable or disable account-level mail automations
- Use AI-powered mail summaries when available

---

## 🔐 Access Requirement

To use these APIs, you must have:

- An active PostScan Mail account
- Access to the Developer API

If you do not yet have access, requests will fail even if the endpoints are reachable.

📧 Contact: **api@postscanmail.com** for onboarding and API support.

---

## 📦 What’s Included

- Official Postman collection JSON for the current public Developer API
- Request examples for supported endpoints
- Example success and error responses
- Environment variables for API onboarding

---

## 🌐 Base URL

`https://api.postscanmail.com/api/account-docs/v2/`

---

## 🔑 Authentication

All requests require the following header:

- Header: `x-api-key`
- Value: your API key

Example:

```text
x-api-key: YOUR_API_KEY
```

---

## ⚡ Quick Start

Get started in a few steps:

1. Download the latest Postman collection from this repository.
2. Open Postman and click **Import**.
3. Select the collection JSON file.
4. Configure the following variables:
   - `base_url` = `https://api.postscanmail.com/api/account-docs/v2/`
   - `api_key` = `YOUR_API_KEY`
5. Run requests from the available API areas.

> Never commit or share a real API key publicly.

---

## 📬 Available API Areas

### Mail Items

Retrieve mail items received in the account.

`GET /items`

The response can include:

- Mail item identifiers and sender details
- Address information
- Cover image and scanned PDF links
- Mail item metadata
- `ai_summary` when an AI-generated summary is available
- `ai_summary_version` for the returned AI summary

When an AI summary is not available:

- `ai_summary` returns an empty array
- `ai_summary_version` returns `null`

---

### Automation Status

Retrieve the current system user-defined automation rules.

`GET /user-defined-rules/system-user-defined-rules`

Supported automation statuses include:

- Auto Scan
- Auto Shred
- Auto Discard
- Auto AI Summary

---

### Automation Toggle

Enable or disable a supported system user-defined automation rule.

`PUT /user-defined-rules/update-system-user-defined-rule`

Supported `automation_name` values include:

- `auto_scan`
- `auto_shred`
- `auto_discard`
- `auto_ai_summary`

Use:

- `is_active: 1` to enable
- `is_active: 0` to disable

---

## 📮 Mail Item Actions

Mail Item Actions allow authorized accounts to request and cancel supported physical mail operations.

These endpoints are scoped to a PostScan Mail address using:

`/addresses/{address_id}/items/actions/...`

### Open Items

Request that one or more mail items be opened.

`POST /addresses/{address_id}/items/actions/open`

Cancel an open request:

`POST /addresses/{address_id}/items/actions/open/cancel`

### Discard Items

Request a discard operation.

`POST /addresses/{address_id}/items/actions/discard`

Cancel a discard request:

`POST /addresses/{address_id}/items/actions/discard/cancel`

### Rescan Items

Request a rescan operation.

`POST /addresses/{address_id}/items/actions/rescan`

Cancel a rescan request:

`POST /addresses/{address_id}/items/actions/rescan/cancel`

### Shred Items

Request a shred operation.

`POST /addresses/{address_id}/items/actions/shred`

Cancel a shred request:

`POST /addresses/{address_id}/items/actions/shred/cancel`

---

## 🤖 AI Summary Support

The Developer API supports AI-generated mail summaries where available.

### Mail Item Response

`GET /items` can return:

```json
{
  "ai_summary": [
    "Sender: ...",
    "Subject: ...",
    "Text Summary:",
    "...",
    "Key Insights:",
    "...",
    "Required Customer Actions:",
    "..."
  ],
  "ai_summary_version": "Version 2"
}
```

If no AI summary is available:

```json
{
  "ai_summary": [],
  "ai_summary_version": null
}
```

### Auto AI Summary

Auto AI Summary can also be viewed and managed through the system user-defined rules endpoints using:

`auto_ai_summary`

---

## ⚠️ Error Handling

API responses may include a structured error body:

```json
{
  "code": 433,
  "message": "You don't have access to the API specified."
}
```

Integrations should evaluate both:

- The HTTP status
- The response body `code` and `message`

Mail Item Actions may also return action-specific validation errors based on:

- Address ownership or availability
- Mail item ownership
- Mail item type or current status
- Account or subscription status
- Required verification
- Whether the requested operation is allowed for the item

Refer to the API documentation for the full error list and handling guidance.

---

## 🔄 Versioning

GitHub Releases are used to track updates to the public Developer API resources.

- **v1.0.0** — Initial public API collection
- **v1.1.0** — Added Mail Item Actions
- **v1.2.0** — Added AI Summary support and updated related automation/documentation

Always use the latest release for the most current Postman collection and API documentation.

---

## ⚠️ Security Notes

- Do not commit real API keys.
- Do not publish customer IDs, mail IDs, addresses, or other customer data.
- Use placeholders in examples and shared requests.
- API access is restricted to registered and authorized PostScan Mail accounts.
- Do not share API keys through public GitHub issues or other public channels.

---

## 💬 Support

For Developer API onboarding, access questions, or integration support:

📧 **api@postscanmail.com**
