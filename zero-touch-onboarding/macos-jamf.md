---
layout: page
title: "macOS Zero-Touch Deployment"
permalink: /zero-touch-onboarding/macos-jamf/
---

# macOS Zero-Touch Deployment with Jamf

## Purpose

This page describes a generalized zero-touch deployment for organization-owned
Mac computers using Apple Business Manager, Automated Device Enrollment and
Jamf Pro.

## Prerequisites

- Devices assigned through Apple Business Manager
- Active connection between Apple Business Manager and Jamf Pro
- Valid Automated Device Enrollment token
- Valid Apple Push Notification service certificate
- Jamf PreStage Enrollment
- Approved identity and local-account design
- Application and configuration-profile assignments
- FileVault recovery-key escrow design
- Tested internet connectivity

## Enrollment Workflow

1. The Mac is assigned to the management server.
2. Jamf Pro synchronizes the device assignment.
3. A PreStage Enrollment is assigned.
4. The user starts the Mac and connects to the internet.
5. Setup Assistant receives the enrollment configuration.
6. The Mac enrolls with Jamf Pro.
7. The approved local account and identity configuration are applied.
8. Required applications and configuration profiles are installed.
9. FileVault and endpoint protection are enabled.
10. Inventory and compliance status are validated.

## Configuration Areas

| Area | Design consideration |
|---|---|
| Automated enrollment | Confirm device and management-server assignment |
| PreStage | Configure Setup Assistant and account options |
| Identity | Use an approved identity integration |
| Local account | Standard-user access by default |
| Encryption | Enable FileVault and escrow the recovery key |
| Bootstrap token | Confirm creation and escrow |
| Applications | Separate essential and optional software |
| Updates | Enforce supported macOS versions |
| Security | Deploy endpoint protection and configuration profiles |
| Inventory | Validate management and compliance information |

## Security Controls

- Require FileVault encryption
- Securely escrow recovery keys
- Restrict unnecessary administrative privileges
- Deploy approved endpoint protection
- Enforce firewall and security configurations
- Maintain supported macOS versions
- Validate management-profile health
- Monitor token and certificate expiry dates

## Token and Certificate Lifecycle

Track and renew:

- Apple Push Notification service certificate
- Automated Device Enrollment token
- Apps and Books token
- Identity-provider certificates
- Application signing certificates, where applicable

Renewal responsibilities and reminders should be documented to prevent
enrollment or application-deployment interruptions.

## Validation Checklist

- [ ] Device appears in Apple Business Manager
- [ ] Device is assigned to the correct management server
- [ ] Jamf PreStage Enrollment is assigned
- [ ] Automated enrollment completed
- [ ] Expected local account created
- [ ] Jamf management framework installed
- [ ] Configuration profiles applied
- [ ] Required applications installed
- [ ] FileVault enabled
- [ ] Recovery key escrowed
- [ ] Bootstrap token escrowed
- [ ] Endpoint protection healthy
- [ ] Inventory submitted
- [ ] Corporate access validated

## References

- [Apple: Automated Device Enrollment](https://support.apple.com/guide/deployment/automated-device-enrollment-management-dep73069dd57/web)
- [Apple Platform Deployment](https://support.apple.com/guide/deployment/welcome/web)
- [Jamf: Automated Device Enrollment for computers](https://learn.jamf.com/r/en-US/jamf-pro-documentation-11.21.0/Automated_Device_Enrollment_for_Computers)
