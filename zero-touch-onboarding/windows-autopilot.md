---
layout: page
title: "Windows Zero-Touch Deployment"
permalink: /zero-touch-onboarding/windows-autopilot/
---

# Windows Zero-Touch Deployment with Intune

## Purpose

This page describes a generalized Windows Autopilot user-driven deployment
using Microsoft Entra join and Microsoft Intune.

Windows Autopilot can transform the manufacturer-installed Windows environment
into a managed business-ready device without maintaining a separate custom
image for every hardware model.

## Prerequisites

- Supported Windows edition
- Microsoft Entra ID
- Microsoft Intune
- Required user and device licensing
- Automatic MDM enrollment
- Registered corporate device
- Assigned deployment profile
- Network access to required Microsoft services
- Approved application and security assignments

## Deployment Workflow

1. The device is registered with Windows Autopilot.
2. A deployment profile is assigned.
3. The device connects to the internet.
4. Windows identifies the assigned organization.
5. The user authenticates using the approved identity.
6. The device joins Microsoft Entra ID.
7. The device enrolls in Microsoft Intune.
8. Required applications and policies are deployed.
9. Security and compliance status are evaluated.
10. Corporate access becomes available after validation.

## Configuration Areas

| Area | Design consideration |
|---|---|
| Deployment mode | User-driven, pre-provisioned or self-deploying |
| Join type | Microsoft Entra join |
| Enrollment Status Page | Track required applications and policies |
| Device naming | Use a consistent fictional naming convention |
| Applications | Separate essential and optional applications |
| Encryption | Require and validate BitLocker |
| Endpoint security | Deploy an approved protection platform |
| Local access | Use standard-user access by default |
| Updates | Apply controlled Windows update policies |
| Compliance | Evaluate encryption, OS and security health |

## Application Strategy

Applications should be categorized as:

- Essential applications required during provisioning
- Security applications required before access
- Productivity applications installed after enrollment
- Optional applications available through Company Portal

Dependencies, detection rules and restart behavior should be tested before
production assignment.

## Validation Checklist

- [ ] Deployment profile received
- [ ] Microsoft Entra join completed
- [ ] Intune enrollment completed
- [ ] Expected device name assigned
- [ ] Required applications installed
- [ ] BitLocker enabled
- [ ] Recovery information securely escrowed
- [ ] Endpoint protection healthy
- [ ] Firewall enabled
- [ ] Windows update policy applied
- [ ] Standard-user access confirmed
- [ ] Device marked compliant
- [ ] Corporate access validated

## Recovery Considerations

Recovery procedures should cover:

- Failed application installation
- Enrollment Status Page timeout
- Incorrect profile assignment
- Duplicate or stale device records
- Device reset and reprovisioning
- Hardware replacement
- Secure device retirement

Avoid deleting Microsoft Entra device objects without understanding their
relationship to the Autopilot registration and Intune enrollment.

## References

- [Microsoft: Windows Autopilot overview](https://learn.microsoft.com/en-us/autopilot/overview)
- [Microsoft: Autopilot registration](https://learn.microsoft.com/en-us/autopilot/registration-overview)
- [Microsoft: Autopilot device preparation](https://learn.microsoft.com/en-us/autopilot/device-preparation/overview)
