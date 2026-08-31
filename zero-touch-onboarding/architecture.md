---
layout: page
title: "Zero-Touch Onboarding Architecture"
permalink: /zero-touch-onboarding/architecture/
---

# Zero-Touch Onboarding Architecture

## Purpose

This reference architecture describes a generalized approach for securely
preparing Windows and macOS devices with minimal manual IT intervention.

## Objectives

- Improve employee Day 1 readiness
- Reduce manual device configuration
- Apply consistent security controls
- Automate application deployment
- Provide role-based access
- Verify compliance before granting access
- Create measurable and auditable processes

## Reference Workflow

1. An authorized onboarding request is submitted.
2. The employee’s identity and required access are approved.
3. The user account and role-based groups are created.
4. A managed Windows or macOS device is assigned.
5. The device starts automated enrollment.
6. Required applications and security policies are deployed.
7. Encryption and endpoint protection are validated.
8. Device compliance is evaluated.
9. Corporate access is granted.
10. IT confirms that the device is ready.

## Platform Components

| Function | Windows | macOS |
|---|---|---|
| Identity | Microsoft Entra ID | Approved identity provider |
| Enrollment | Windows Autopilot | Apple Automated Device Enrollment |
| Management | Microsoft Intune | Jamf Pro |
| Encryption | BitLocker | FileVault |
| Application delivery | Intune | Jamf Pro |
| Compliance | Intune compliance | Jamf inventory and compliance integration |
| Access control | Conditional Access | Conditional Access or approved access platform |

## Design Principles

### Identity-driven deployment

Application and access assignments should be based on approved roles and groups.

### Security by default

Encryption, endpoint protection, firewall, operating-system updates and
compliance policies should be automatically applied.

### Minimum required applications

Only essential applications should block initial provisioning. Other
applications can be installed after the user reaches the desktop.

### Controlled exceptions

Exceptions should be documented, approved, time-bound and periodically reviewed.

## Success Measurements

- Provisioning success rate
- Time to employee productivity
- Number of manual IT touchpoints
- Application installation failure rate
- Device compliance rate
- Onboarding-related support requests

## Related Pages

- [Windows Autopilot](/zero-touch-onboarding/windows-autopilot/)
- [macOS and Jamf](/zero-touch-onboarding/macos-jamf/)
- [Security Controls](/zero-touch-onboarding/security-controls/)
- [Troubleshooting](/zero-touch-onboarding/troubleshooting/)
