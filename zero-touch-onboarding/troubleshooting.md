---
layout: page
title: "Zero-Touch Troubleshooting"
permalink: /zero-touch-onboarding/troubleshooting/
---

# Zero-Touch Deployment Troubleshooting

## Troubleshooting Method

For every issue, record:

1. The visible symptom
2. The affected provisioning stage
3. The device and operating-system version
4. The diagnostic source
5. The likely cause
6. The corrective action
7. The final validation result
8. The preventive improvement

## Common Issues

| Symptom | Platform | Check | Possible cause | Corrective action |
|---|---|---|---|---|
| Deployment profile not received | Windows | Autopilot registration and assignment | Device or profile assignment issue | Validate registration and group targeting |
| Enrollment does not start | Windows | Licence, MDM scope and network | User or enrollment configuration issue | Confirm prerequisites and retry |
| Required application fails | Windows | Intune app status and detection rules | Package, dependency or detection failure | Correct the application configuration |
| Enrollment Status Page remains blocked | Windows | Required applications and policy status | A required component has failed | Identify and remediate the blocking item |
| Device remains noncompliant | Windows | BitLocker, security health and OS version | Compliance condition is not satisfied | Correct the failed control and synchronize |
| Mac does not enter managed enrollment | macOS | Apple Business Manager assignment | Incorrect management-server assignment | Correct the assignment and synchronize |
| PreStage configuration not received | macOS | Jamf PreStage scope | Device is not assigned to the PreStage | Add the device to the correct scope |
| Application does not install | macOS | Policy scope and inventory | Trigger, package or targeting issue | Correct targeting and run inventory update |
| FileVault key is not escrowed | macOS | Encryption and inventory status | Profile or secure-token issue | Correct the configuration and rotate the key |
| Login repeatedly loops | macOS | Identity configuration, time and network | Authentication or redirect issue | Validate identity settings and connectivity |
| Employee is blocked after enrollment | Both | Compliance and access records | Compliance state has not synchronized | Synchronize and review the access decision |

## Diagnostic Principles

- Start with the first failed provisioning stage.
- Confirm licensing and assignment before changing policies.
- Check device time and internet connectivity.
- Review application dependencies and detection logic.
- Avoid deleting device records without understanding their relationship.
- Test corrective actions on a limited device group.
- Record the successful resolution.
- Remove credentials and personal information before sharing logs.

## Escalation Information

An escalation should include:

- Generalized device identifier
- Platform and OS version
- Provisioning stage
- Approximate failure time
- Error code
- Relevant sanitized logs
- Actions already attempted
- Expected and actual results

Never publish access tokens, recovery keys, employee details, tenant identifiers
or unredacted production logs.
