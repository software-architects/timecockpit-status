# Time Cockpit service incidents

This repository is the public incident record for [Time Cockpit](https://www.timecockpit.com/). Software architects gmbh uses it to publish customer-visible service incidents, planned maintenance, progress updates, and resolutions.

## Quick links

| Resource | Link |
| --- | --- |
| Current service health | [Time Cockpit Status](https://status.timecockpit.com/) |
| Active incidents | [Open incident issues](https://github.com/software-architects/timecockpit-status/issues?q=is%3Aissue%20is%3Aopen%20label%3Aincident) |
| Incident history | [All incident issues](https://github.com/software-architects/timecockpit-status/issues?q=is%3Aissue%20label%3Aincident) |
| Product website | [timecockpit.com](https://www.timecockpit.com/) |
| Time Cockpit web client | [web.timecockpit.com](https://web.timecockpit.com/) |
| Product documentation | [docs.timecockpit.com](https://docs.timecockpit.com/) |
| Customer support | [support@timecockpit.com](mailto:support@timecockpit.com) |

If the status page cannot be reached, use the active-incidents link above as the independent communication fallback.

## What this repository is for

Issues carrying the `incident` label are official customer-facing communications about Time Cockpit service health. An open incident is active; a closed incident is resolved. Issues retain their updates after recovery so customers can review recent service history.

The [status page](https://status.timecockpit.com/) combines these incident communications with automated availability and response-time measurements for the web client, web API, identity service, management API, and public website. Missing monitoring data is shown as unknown rather than healthy.

This repository is not:

- a customer-support queue;
- a place to report product defects or request features;
- the internal alerting or engineering work-tracking system; or
- a source of contractual SLA or service-credit calculations.

For help with your account or an issue that is not already described here, contact [Time Cockpit support](mailto:support@timecockpit.com). Do not publish account details, personal data, credentials, tenant identifiers, or confidential business information in a GitHub issue or comment.

The absence of an open incident does not by itself prove that every service is healthy. Check the status page for the latest automated measurements.

## Reading an incident

Incident titles use `[Incident] <customer-visible impact>`, for example `[Incident] Sign-in unavailable for some users`.

The issue body is the current canonical summary. Times are written in UTC using ISO 8601 (`YYYY-MM-DDTHH:MM:SSZ`) and your browser may display GitHub's own timestamps in your local time zone.

| Field | Meaning |
| --- | --- |
| Incident began | Earliest evidence-backed start of customer impact. |
| Incident ended | `Ongoing` while active, then the verified recovery time. |
| Last public update | Time of the latest material customer-facing update. |
| Next public update by | The next update commitment while the incident is active. |
| Customer impact | Observable symptoms, known scope, and unaffected functionality. |
| Current update | What is known and what customers should expect now. |
| Workaround | A safe action customers can take, when one exists. |
| Public timeline | Chronological customer-relevant events. |
| Resolution | How service was restored and any customer-relevant follow-up. |

Material updates are kept in the issue body and may also be posted as comments so subscribers receive notifications. Internal diagnostics and remediation tasks remain in private operational systems.

## Labels

Labels are the authoritative machine-readable metadata used by the status page. Every incident has the `incident` label, exactly one `status:*` label, exactly one `severity:*` label, and at least one `component:*` label.

### Lifecycle status

| Label | Meaning |
| --- | --- |
| `status:investigating` | Impact, scope, or cause is still being assessed. |
| `status:identified` | Cause or scope is understood and remediation is in progress. |
| `status:monitoring` | A mitigation is in place and recovery is being verified. |
| `status:resolved` | Recovery is verified and the public record is complete. |

Lifecycle labels are replaced as an incident advances; they are not accumulated.

### Severity

| Label | Meaning | Effect on the displayed overall status |
| --- | --- | --- |
| `severity:maintenance` | Planned maintenance without an unplanned service failure. | Does not raise measured service health. |
| `severity:minor` | Limited degradation or a practical workaround exists. | At least degraded. |
| `severity:major` | Material partial outage or a core workflow is affected. | At least partial outage. |
| `severity:critical` | Widespread or complete outage of critical functionality. | Major outage. |

Severity communicates customer impact, not engineering effort or root-cause complexity. If planned maintenance causes unplanned impact, `severity:maintenance` is replaced with the appropriate impact severity. An incident can raise the status displayed from monitoring, but it never hides a worse measured state.

### Affected components

| Label | Component |
| --- | --- |
| `component:web-client` | Browser application and public sign-in entry point. |
| `component:web-api` | Core application API used by the web client and integrations. |
| `component:identity` | Authentication and token issuance. |
| `component:management-api` | Account and subscription management services. |
| `component:website` | Public Time Cockpit website. |

More than one component label can be present when an incident crosses service boundaries.

## Receiving notifications

To receive updates for all incidents, sign in to GitHub, open this repository's **Watch** menu, choose **Custom**, and select **Issues**. To follow only one incident, open that issue and use its **Subscribe** control. Delivery through GitHub, email, or mobile depends on your [GitHub notification settings](https://github.com/settings/notifications).

GitHub notification behavior is controlled by GitHub and your account settings. The [status page](https://status.timecockpit.com/) remains the best place to check current service health directly.

## Incident-author workflow

The incident form and label controls are intended for authorized Time Cockpit incident authors. All published content is public.

1. Confirm customer impact through internal monitoring; do not wait for the public status publisher.
2. Open the [**Service incident** form](https://github.com/software-architects/timecockpit-status/issues/new?template=service-incident.yml). It applies `incident` and `status:investigating` automatically.
3. Apply exactly one severity label and every affected component label.
4. Complete the UTC metadata and publish only customer-safe impact, scope, workaround, and next-update time.
5. For each material update, synchronize **Last public update**, **Next public update**, **Current update**, and **Public timeline**. Post a corresponding comment when subscriber notification is required.
6. Replace the lifecycle label as the incident advances from investigating to identified to monitoring.
7. After verified recovery, set **Incident ended**, complete **Resolution**, apply `status:resolved`, close the issue, and verify that the status page reflects the resolution.

Before publishing, verify that the issue contains no tenant names, personal data, secrets, traces, parameterized customer URLs, internal-only infrastructure details, or unsupported estimates.

## Repository setup

Create the following labels before the incident form is used. GitHub does not create missing labels referenced by an issue form, so a missing label would not be applied automatically.

| Label | Suggested color |
| --- | --- |
| `incident` | `#B60205` |
| `status:investigating` | `#D93F0B` |
| `status:identified` | `#FBCA04` |
| `status:monitoring` | `#1D76DB` |
| `status:resolved` | `#0E8A16` |
| `severity:maintenance` | `#5319E7` |
| `severity:minor` | `#FBCA04` |
| `severity:major` | `#D93F0B` |
| `severity:critical` | `#B60205` |
| `component:web-client` | `#25A4D5` |
| `component:web-api` | `#25A4D5` |
| `component:identity` | `#25A4D5` |
| `component:management-api` | `#25A4D5` |
| `component:website` | `#25A4D5` |

The issue repository is intentionally separate from the status-page hosting and monitoring infrastructure. This provides a public communication path even when the status page or its data pipeline is unavailable.

## Privacy and support

This is a public repository. If you need to share customer-specific information, contact [support@timecockpit.com](mailto:support@timecockpit.com) instead of posting it here. Additional contact options are available on the [Time Cockpit contact page](https://www.timecockpit.com/company/contact/).

Time Cockpit is a product of [software architects gmbh](https://www.timecockpit.com/about-us/).
