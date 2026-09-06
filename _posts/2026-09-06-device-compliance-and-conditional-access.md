---
layout: post
title: "From Device Enrollment to Secure Access: Designing Device Compliance and Conditional Access"
date: 2026-09-06
categories: [Identity, Security, Endpoint Management]
author: Anil Kumar BM
---

A device can be enrolled in management and still present a security risk. Enrollment tells us that a management platform can see and configure the device. It does not, by itself, confirm that encryption is active, endpoint protection is healthy, the operating system is supported, or the device has recently reported its status.

This is where device compliance and Microsoft Entra Conditional Access work together. Compliance evaluates the state of a device. Conditional Access uses that state, along with identity and sign-in context, to decide whether access should be granted.

The objective is not simply to block more sign-ins. The objective is to make access decisions consistently, provide a clear remediation path and reduce the chance that an unhealthy or unmanaged endpoint can reach protected resources.

## Managed, Compliant and Trusted Are Different States

These terms are often used as if they mean the same thing, but they answer different questions:

| State | Question answered |
|---|---|
| Managed | Is the device enrolled and visible to an approved management platform? |
| Compliant | Does it currently satisfy the organization's defined security requirements? |
| Trusted for access | Do the identity, device and sign-in conditions satisfy the applicable access policy? |

A managed device can become noncompliant when encryption is disabled, endpoint protection is unhealthy, its operating system falls outside the supported range or it stops checking in. Likewise, a compliant device should not automatically bypass identity controls such as multifactor authentication.

Trust should therefore be evaluated from more than one signal.

## Reference Access Flow

A simplified access decision follows this sequence:

1. A user signs in to a protected application.
2. Microsoft Entra ID authenticates the identity.
3. Conditional Access evaluates applicable policies.
4. The registered device identity and current compliance state are checked.
5. Microsoft Intune supplies the compliance state for managed Windows devices.
6. Jamf Pro can supply the compliance state for managed Apple devices through Microsoft's Partner Compliance integration.
7. Access is granted, challenged or blocked according to the combined policy result.
8. If the device is noncompliant, the user receives a remediation path and the device is evaluated again after correction.

This separation is important: the endpoint platform evaluates device health, while Conditional Access makes the access decision.

## Building a Practical Compliance Baseline

A compliance baseline should begin with controls that are important, measurable and reasonably easy to remediate. Attempting to enforce every possible setting on day one often creates noise and makes genuine risks harder to identify.

A practical starting baseline may include:

### Storage encryption

Require BitLocker on Windows and FileVault on macOS. Encryption status should be reported by the management platform, and recovery information should be securely escrowed through an approved process.

### Endpoint protection

Confirm that the approved endpoint security agent is installed, active and reporting a healthy state. Where supported, risk information from the security platform can become an additional compliance signal.

### Host firewall

Validate that the operating-system firewall is enabled and managed. The detailed rule set should be delivered through configuration policy rather than exposed in a public document.

### Supported operating-system version

Define a supported version range and allow enough time for staged updates. A minimum version should reflect both security requirements and the organization's ability to deploy and support the update.

### Management health

The device should remain enrolled, retain its management profile and check in within an approved validity period. A device that has stopped reporting should not remain trusted indefinitely.

### Device integrity

Use platform-appropriate integrity or health signals where available. The precise checks will differ across Windows and macOS, so the outcome should be consistent even when the underlying technologies are different.

## Windows Compliance with Microsoft Intune

For a Windows device, the typical relationship is:

1. The device is registered with Microsoft Entra ID.
2. It enrolls in Microsoft Intune.
3. Intune assigns the applicable platform-specific compliance policy.
4. The device evaluates the assigned requirements and reports its result.
5. Intune sends the compliance state to Microsoft Entra ID.
6. Conditional Access uses that state when a protected resource is requested.

An important design decision is how devices with no assigned compliance policy are treated. An apparently compliant result should always be backed by an explicitly assigned policy. Administrators should also understand evaluation and check-in timing before interpreting a temporary status as a permanent failure.

Compliance policy and configuration policy serve different purposes. Configuration policy attempts to establish the desired state; compliance policy evaluates whether the required state exists. Used together, they can both prevent drift and identify it.

## macOS Compliance with Jamf Pro and Microsoft Entra

In a Jamf-managed macOS environment, Jamf Pro can calculate compliance by using inventory information and smart-group membership. Through Microsoft's Partner Compliance Connector, that state can be passed to Intune and then made available to Microsoft Entra Conditional Access.

A generalized sequence is:

1. The Mac enrolls through Automated Device Enrollment and Jamf Pro.
2. Required profiles, applications and security controls are deployed.
3. The Mac is registered with Microsoft Entra ID using the approved registration workflow.
4. Jamf Pro evaluates the Mac against the configured compliance criteria.
5. Jamf sends the management and compliance state to the Microsoft partner connector.
6. Microsoft Entra uses the resulting state during Conditional Access evaluation.

The success of this design depends on more than enabling an integration. Registration experience, identity mapping, application availability, smart-group logic and synchronization timing must all be tested. Platform Single Sign-on can also participate in supported registration designs, but any migration should be validated carefully before broad enforcement.

## Designing the Conditional Access Policy

The policy should clearly define:

- Included identities
- Explicit exclusions
- Target resources
- Device platforms
- Client or authentication conditions when required
- Grant controls
- Session controls, if applicable
- Deployment state

For a strong access decision, organizations commonly combine multifactor authentication with the requirement that a device be marked compliant. If both controls are necessary, confirm that the policy requires all selected controls rather than accepting only one.

Emergency-access accounts should be deliberately excluded, secured separately and monitored. Non-interactive identities and device-registration dependencies should also be understood before a broadly scoped policy is enforced.

Avoid treating Conditional Access as an isolated setting. Existing policies are evaluated together, and their combined effect can differ from what one policy appears to do on its own.

## A Safer Rollout Method

### Phase 1: Establish visibility

Confirm that targeted devices are registered, receiving a compliance policy and reporting current results. Resolve unexplained states before access enforcement is introduced.

### Phase 2: Use report-only mode

Create the Conditional Access policy in report-only mode. Review sign-in records to understand which sign-ins would succeed, fail or require user action. Microsoft notes that report-only compliance evaluation can still produce certificate-selection prompts on some Apple and mobile platforms, so the user experience should also be tested.

### Phase 3: Pilot

Apply enforcement to a small, representative pilot population covering:

- Windows and macOS
- Browser and desktop applications
- Office-based and remote connectivity
- Newly enrolled and existing devices
- Standard and privileged roles

Provide a documented support and rollback path during the pilot.

### Phase 4: Expand in stages

Expand only after reviewing failures, remediating application dependencies and confirming that support teams can distinguish identity failures from device-compliance failures.

### Phase 5: Operate continuously

After enforcement, monitor policy results, stale device records, recurring noncompliance and exception expiry. A control is not complete simply because it was enabled successfully once.

## Common Problems and First Checks

| Symptom | Likely area | First checks |
|---|---|---|
| Device is managed but shown as noncompliant | Failed compliance setting | Review the per-setting compliance result and last check-in |
| Intune shows compliant but access is blocked | Token, registration or policy evaluation | Review the Microsoft Entra sign-in record and device identity |
| Device shows no assigned compliance policy | Scope or group assignment | Confirm policy assignment and applicable filters |
| Mac is managed in Jamf but has no usable compliance state | Registration or partner integration | Validate Entra registration, applicable group and compliance group |
| User is repeatedly asked to register | Identity mapping or stale registration | Check the registered account, device record and authentication workflow |
| Corrected device remains blocked | Synchronization delay | Initiate an approved check-in and review the latest timestamps |
| Unexpected users are affected | Policy scope or overlapping policy | Use sign-in details and the Conditional Access What If tool |
| Duplicate device records appear | Re-enrollment or incomplete lifecycle cleanup | Identify the active record before removing stale objects |

Deleting device objects should not be the first troubleshooting step. The relationship between management, registration and identity records should be understood before cleanup, otherwise a working deployment can be made harder to recover.

## Measuring the Outcome

Useful operational measures include:

- Percentage of active devices that are compliant
- Time from enrollment to the first compliant state
- Number of blocked sign-ins caused by noncompliance
- Average time to remediate a device
- Number of devices with stale check-in information
- Repeated failures by compliance setting
- Exception count and age
- Support cases created after policy changes

The goal is not a dashboard that always shows 100 percent. The goal is trustworthy reporting, timely remediation and predictable access decisions.

## Key Lessons

1. Enrollment establishes management; it does not establish permanent trust.
2. Compliance criteria should be measurable and supported by a remediation process.
3. Windows and macOS can feed a common access decision while retaining platform-specific management.
4. Report-only analysis and a representative pilot reduce the risk of unintended disruption.
5. Sign-in records are essential for understanding why Conditional Access granted or blocked access.
6. Emergency access and rollback planning are part of the security design, not afterthoughts.
7. Compliance requires continuous monitoring because device state changes over time.

## Conclusion

Zero-touch enrollment provides a consistent starting point, but secure access requires continuous verification. By connecting Intune and Jamf Pro compliance signals with Microsoft Entra Conditional Access, organizations can move from simply managing devices to making evidence-based access decisions.

The most effective implementation is not the one with the largest number of controls. It is the one that produces reliable signals, gives users a clear path to remediation and can be operated safely at scale.

## References

- [Microsoft: Device compliance policies in Intune](https://learn.microsoft.com/en-us/intune/device-security/compliance/overview)
- [Microsoft: Require device compliance with Conditional Access](https://learn.microsoft.com/en-us/entra/identity/conditional-access/policy-all-users-device-compliance)
- [Microsoft: Analyze Conditional Access policy impact with report-only mode](https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-conditional-access-report-only)
- [Microsoft: Conditional Access What If tool](https://learn.microsoft.com/en-us/entra/identity/conditional-access/what-if-tool)
- [Jamf: Device Compliance with Microsoft Entra and Jamf Pro](https://learn.jamf.com/r/en-US/technical-paper-microsoft-intune-current/Device_Compliance_with_Microsoft_Intune_and_Jamf_Pro)

---

*This article contains generalized guidance and fictional examples for educational purposes. It does not describe any specific production environment.*
