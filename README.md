# Okta JML Workflows — Office 365

Automated Joiner-Mover-Leaver identity lifecycle pipeline built with Okta Workflows and Microsoft Entra ID. Triggers on native Okta lifecycle events and executes provisioning actions against Office 365 without manual intervention.

---

## Architecture

Three event-driven flows running on Okta Workflows handle the full employee lifecycle:

- **Joiner**: Triggers on User Created. Automatically assigns the user to Microsoft Office 365 via SSO application assignment.
- **Leaver**: Triggers on User Deactivated. Automatically removes the user from the Office 365 application assignment.
- **Mover**: Triggers on User Okta Profile Updated. Propagates changed profile attributes to Azure Active Directory via Microsoft Graph API.

All flows use the native Okta connection and fire automatically on lifecycle events with no scheduled polling and no manual steps.

---

## Tech Stack

- Okta Workflows
- Okta Universal Directory
- Microsoft Entra ID (Azure Active Directory)
- Microsoft Office 365
- SCIM provisioning
- Microsoft Graph API

---

## Flows

| Flow | Trigger | Action | Target |
|---|---|---|---|
| JML Joiner - Office 365 | User Created | Assign User to Application for SSO | Microsoft Office 365 |
| JML Leaver - Office 365 | User Deactivated | Remove User from Application | Microsoft Office 365 |
| JML Mover - Office 365 | User Okta Profile Updated | Update User | Azure Active Directory |

---

## Security Design

- Zero hardcoded credentials. All connections use OAuth 2.0 delegated authorization through the Okta Workflows connector framework.
- Least privilege. Each flow connection scoped to the minimum permissions required for its action.
- Event-driven. No standing access or scheduled jobs. Flows execute only on identity lifecycle events.

---

## Author

Go Cloud Architects
[github.com/IAM-AI-Security](https://github.com/IAM-AI-Security)
