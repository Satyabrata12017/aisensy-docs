---
title: Release Notes
---

# Release Notes

## v1.0.0 (27 October 2026)

First Marketplace release. The app was rebuilt to be generic, configurable and compatible with Frappe v14, v15 and v16.

### Compatibility
| Frappe | Branch |
|---|---|
| v14 | `version-14` |
| v15 | `version-15` |
| v16 | `version-16` |

ERPNext and HRMS are optional.

### New
- **Any DocType:** notifications on any doctype, sent on After Insert, After Save, Before Submit, After Submit or After Cancel
- **Field pickers:** mobile, recipient name, template parameter, attachment and condition fields are chosen from the selected doctype
- **Media attachments:** images (jpg, jpeg, png, webp), videos (mp4, 3gp) and documents (PDF, office files), from an attach field, any attached file, a URL field or a fixed URL, with a media-type filter and file name
- **Conditions** on every notification: `=`, `!=`, `>`, `>=`, `<`, `<=`, `in`, `not in`, `like`, `not like`, `is`, `is not`, with values cast by fieldtype
- **Send Only If Checked:** optional opt-in checkbox field
- **Send Test Message** button, optionally to another number
- **Scheduled daily messages** with retries (every 15 minutes, up to 5 attempts)
- **Default Country Code** setting; international numbers are kept as entered
- **Notification Log** shows status, HTTP status, doctype and document
- Workspace, app logo and apps-screen entry

### Improved
- Messages are sent in a **background job after the document is saved**, so a slow API never blocks users and a rolled-back save never sends
- The API key is **stored encrypted**
- Whitelisted methods check permissions and accept POST only
- Fieldnames are validated when a notification is saved

### Fixed
- Scheduled messages crashed on retry, retried forever and were marked Sent even when the API call failed
- API errors (4xx/5xx) were logged as Success, and requests had no timeout
- One notification's rule could stop the remaining notifications for the same document

### Upgrading from 0.x
Run `bench migrate`. Patches keep the old built-in behavior (the `custom_send_on_whatsapp` checkbox, `contact_display` as the name, +91) and encrypt the stored API key. Any deployment-specific rules from the old code must be re-added as **Conditions** or **Attachment Field** settings on your notifications.
