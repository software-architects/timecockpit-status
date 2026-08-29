# Time Cockpit service status events

This repository is the public communication record for [Time Cockpit](https://www.timecockpit.com/) service incidents and planned maintenance. The [Time Cockpit status page](https://status.timecockpit.com/) combines these updates with automated availability and response-time measurements.

## Quick links

| Resource | Link |
| --- | --- |
| Current service health | [status.timecockpit.com](https://status.timecockpit.com/) |
| Active status events | [Open status-event issues](https://github.com/software-architects/timecockpit-status/issues?q=is%3Aissue%20is%3Aopen%20label%3Astatus-event) |
| Complete public history | [All status-event issues](https://github.com/software-architects/timecockpit-status/issues?q=is%3Aissue%20label%3Astatus-event) |
| Product website | [timecockpit.com](https://www.timecockpit.com/) |
| Web client | [web.timecockpit.com](https://web.timecockpit.com/) |
| Documentation | [docs.timecockpit.com](https://docs.timecockpit.com/) |
| Customer support | [support@timecockpit.com](mailto:support@timecockpit.com) |

If the status page cannot be reached, the open-issues link is the independent communication fallback. This public repository is not a support queue or a place to disclose account details, tenant identifiers, personal data, credentials, or confidential information.

## Event types

Every published record carries the `status-event` ingestion label and exactly one type label.

| Label | Meaning |
| --- | --- |
| `type:incident` | Unplanned customer-visible impact being investigated and remediated. |
| `type:maintenance` | Scheduled work announced in advance with a defined maintenance window. |

### Service incidents

Use the [Service incident form](https://github.com/software-architects/timecockpit-status/issues/new?template=service-incident.yml). Incident lifecycle labels are replaced—not accumulated—as work advances:

`status:investigating` → `status:identified` → `status:monitoring` → `status:resolved`

Every incident also has exactly one severity label:

| Label | Customer impact | Minimum displayed state |
| --- | --- | --- |
| `severity:minor` | Limited degradation or a practical workaround exists. | Degraded |
| `severity:major` | Material partial outage or a core workflow is affected. | Partial outage |
| `severity:critical` | Widespread or complete outage of critical functionality. | Major outage |

Incident severity can raise the status derived from monitoring, but never hide a worse measured state.

### Planned maintenance

Use the [Planned maintenance form](https://github.com/software-architects/timecockpit-status/issues/new?template=planned-maintenance.yml). Maintenance lifecycle labels are:

`status:scheduled` → `status:in-progress` → `status:completed`

Use `status:cancelled` when announced work will not proceed. Every maintenance event also has exactly one expected-impact label:

| Label | Meaning |
| --- | --- |
| `impact:none` | No customer-visible interruption is expected. |
| `impact:degraded` | Slower responses or limited degradation may occur. |
| `impact:intermittent` | Brief or intermittent interruptions are expected. |
| `impact:unavailable` | The affected functionality is expected to be unavailable during some or all of the window. |

Planned maintenance never changes measured service health by itself. If unexpected impact occurs, authors open a separate incident and link both records.

## Affected components

Apply at least one component label; apply all that are affected.

| Label | Component |
| --- | --- |
| `component:web-client` | Browser application and public sign-in entry point. |
| `component:web-api` | Core application API. |
| `component:identity` | Authentication and token issuance. |
| `component:management-api` | Account and subscription management. |
| `component:website` | Public Time Cockpit website. |

## Reading and receiving updates

Structured UTC fields in the issue body provide the event window, last update, impact, current update, customer action or workaround, public timeline, and outcome. The issue body is the current canonical summary. Material changes may also be posted as comments so subscribers are notified.

To receive all updates, sign in to GitHub, open this repository's **Watch** menu, choose **Custom**, and select **Issues**. To follow one event, use **Subscribe** on that issue. Notification delivery depends on your [GitHub notification settings](https://github.com/settings/notifications).

## Authorized author checklist

1. Select the form matching the event type; do not describe planned work as an incident.
2. Apply every required type, lifecycle, severity or expected-impact, and component label.
3. Use UTC ISO 8601 timestamps (`YYYY-MM-DDTHH:MM:SSZ`).
4. Publish only customer-observable impact, safe workarounds/actions, and realistic update commitments.
5. Keep the structured fields and public timeline synchronized and comment when subscribers should be notified.
6. Replace lifecycle labels as the event advances; close only after recovery, completion, or cancellation is documented.
7. Open a separate linked incident if maintenance produces unexpected customer impact.

## Required repository labels

Create these labels before using the forms; GitHub does not create missing labels referenced by an issue form.

| Group | Labels | Suggested color |
| --- | --- | --- |
| Ingestion | `status-event` | `#B60205` |
| Type | `type:incident`, `type:maintenance` | `#5319E7` |
| Incident lifecycle | `status:investigating`, `status:identified`, `status:monitoring`, `status:resolved` | orange/yellow/blue/green |
| Maintenance lifecycle | `status:scheduled`, `status:in-progress`, `status:completed`, `status:cancelled` | blue/yellow/green/gray |
| Severity | `severity:minor`, `severity:major`, `severity:critical` | yellow/orange/red |
| Expected impact | `impact:none`, `impact:degraded`, `impact:intermittent`, `impact:unavailable` | green/yellow/orange/red |
| Components | `component:web-client`, `component:web-api`, `component:identity`, `component:management-api`, `component:website` | `#25A4D5` |

Legacy issues using `incident` or `severity:maintenance` remain readable by the status publisher, but new issues must use the contract above.

## Privacy and support

For account-specific help or confidential information, contact [support@timecockpit.com](mailto:support@timecockpit.com) or use the [Time Cockpit contact page](https://www.timecockpit.com/company/contact/). Time Cockpit is a product of [software architects gmbh](https://www.timecockpit.com/about-us/).
