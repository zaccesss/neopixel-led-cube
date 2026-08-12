# Security Policy

## Scope

This repository is an Arduino sketch and hardware build guide for a NeoPixel LED cube. It contains no service, no network component and no user data, so the attack surface is narrow. In scope:

- A vulnerability in the firmware that could damage connected hardware (for example an unbounded PWM or current-drive value)
- Insecure or unsafe wiring guidance in [hardware/README.md](hardware/README.md) that could create a fire or shock risk if followed as written

## Out of scope

- General code quality or style issues, use a regular issue instead
- Third-party library vulnerabilities in the Adafruit NeoPixel dependency, report those upstream

## Reporting a vulnerability

> [!IMPORTANT]
> Report privately, not in a public issue. Email [eng@isaacadjei.me](mailto:eng@isaacadjei.me) with details and reproduction steps. Expect an acknowledgement within a few days.

## The shared policy

> [!NOTE]
> The full policy, covering scope, the disclosure process and expected response times, is in [zaccesss/security-policy](https://github.com/zaccesss/security-policy) and on [isaacadjei.me/security-policy](https://isaacadjei.me/security-policy). This file takes precedence where the two differ.
