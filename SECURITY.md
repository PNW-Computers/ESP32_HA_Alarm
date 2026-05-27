# Security Policy

Thank you for helping keep **ESP32_HA_Alarm** safe, reliable, and responsible.

This repository contains configuration, documentation, wiring references, ESPHome/Home Assistant automation examples, and related materials for an ESP32-based alarm and notification system. Because this project may control physical hardware such as relays, sirens, sensors, batteries, cameras, and Home Assistant automations, security and safety concerns are taken seriously.

Please do **not** report security vulnerabilities through public GitHub issues, discussions, or pull requests if the report includes sensitive details, bypass techniques, private infrastructure information, credentials, Home Assistant access details, camera details, physical security weaknesses, or exploitable configuration problems.

---

## Supported Versions

The current `main` branch is considered the actively maintained version of this repository.

| Version / Branch | Security Support |
| --- | --- |
| `main` / current repository content | Supported |
| Older commits | Not officially supported |
| Forks or modified copies | Not officially supported |
| Personal deployments based on modified YAML or hardware | Not officially supported |

If formal versioned releases are added later, this section will be updated to identify which versions are actively supported.

---

## Reporting a Security Issue

To report a security issue, please email:

**support@pnwcomputers.com**

Use a subject line similar to:

**Security Report: ESP32_HA_Alarm Vulnerability**

Please include as much detail as safely possible, including:

- A clear description of the issue.
- The affected file, YAML configuration, automation, wiring reference, script, or documentation section.
- Why the issue may create a security or safety risk.
- Steps to reproduce the issue in a safe lab environment, if applicable.
- The potential impact.
- Suggested remediation, if you have one.
- Your Home Assistant, ESPHome, ESP32 board, sensor, relay, or firmware version, if relevant.
- Whether the issue involves exposed credentials, unsafe defaults, alarm bypass, relay behavior, unsafe siren activation, camera privacy, wireless access, or physical tampering.

Please do **not** include real passwords, API keys, Home Assistant tokens, Wi-Fi credentials, client data, private network details, camera URLs, public IP addresses, GPS coordinates, home addresses, or sensitive alarm deployment details in your report.

---

## Examples of Security Issues to Report

Please report issues such as:

- Exposed Wi-Fi credentials, Home Assistant tokens, API keys, encryption keys, or secrets.
- Unsafe ESPHome API, OTA, captive portal, fallback hotspot, or web server defaults.
- Configuration that could allow unauthorized control of the siren, relay, sensors, or automations.
- Alarm bypass methods caused by insecure defaults or unsafe logic.
- Automations that could trigger false alarms, fail to stop the siren, or ignore safety timeouts.
- Unsafe relay behavior that could energize hardware unexpectedly.
- Documentation that recommends exposing Home Assistant, ESPHome, Frigate, or camera feeds insecurely.
- Camera, notification, or Frigate examples that could leak private footage or personal information.
- Unsafe handling of MQTT credentials, webhook URLs, notification tokens, or mobile app identifiers.
- Insecure dashboard controls that allow unauthorized alarm arming, disarming, or silencing.
- Hardware wiring guidance that could create fire, battery, relay, or electrical safety risks.
- Instructions that could accidentally encourage switching mains AC with relay modules intended only for low-voltage DC.
- Logic flaws that could prevent the alarm from timing out, silencing, or entering a safe state.
- Security-sensitive information accidentally committed to the repository.

---

## Issues That Are Not Security Vulnerabilities

The following should normally be opened as regular GitHub issues instead of private security reports:

- Typos or formatting issues.
- Broken links.
- General documentation improvements.
- Feature requests.
- Non-sensitive YAML bugs.
- Questions about Home Assistant setup.
- Questions about ESPHome flashing.
- General wiring clarification.
- Parts availability or shopping link issues.
- Non-security dashboard layout improvements.

If you are unsure whether something is a security issue, please report it privately first.

---

## Sensitive Information Policy

Do not commit sensitive information to this repository.

This includes, but is not limited to:

- Wi-Fi SSIDs and passwords.
- Home Assistant long-lived access tokens.
- ESPHome API encryption keys.
- OTA passwords.
- MQTT usernames and passwords.
- Webhook URLs.
- Notification service tokens.
- Frigate camera URLs.
- RTSP usernames and passwords.
- NVR credentials.
- Public IP addresses tied to a real deployment.
- VPN details.
- Router, firewall, or port-forwarding details.
- Home addresses or GPS coordinates.
- Photos or screenshots showing private property layouts.
- Camera screenshots showing identifiable people, vehicles, license plates, or private areas.
- Alarm arming/disarming codes.
- Physical bypass details for a real deployment.
- Private Home Assistant dashboard URLs.

If sensitive information is accidentally committed, it should be treated as exposed. Remove it from the repository, rotate the affected credential or key, and review the commit history as needed.

---

## Responsible Disclosure

We ask that all reporters follow responsible disclosure practices:

1. Report security concerns privately.
2. Allow reasonable time for review and remediation.
3. Do not publicly disclose the issue before a fix or mitigation is available.
4. Do not exploit the issue beyond what is necessary to confirm it.
5. Do not access, modify, delete, trigger, silence, or interfere with any alarm system that does not belong to you.
6. Do not test against another person’s Home Assistant, ESPHome device, camera system, network, vehicle, or property without explicit authorization.
7. Do not publish bypass instructions for real-world alarm deployments.

Reports involving unauthorized access, credential theft, alarm bypass abuse, harassment, stalking, doxxing, surveillance misuse, or physical tampering will not be supported.

---

## Hardware and Physical Safety

This project may involve low-voltage wiring, relays, batteries, sirens, sensors, and microcontrollers. Physical safety matters.

Follow these safety rules:

- Use this project only with low-voltage DC circuits unless you are properly qualified and using equipment specifically rated for mains voltage.
- Do not switch 120V/240V AC directly with relay modules intended for low-voltage DC hobby electronics.
- Fuse power lines appropriately.
- Use properly rated wire, connectors, power supplies, and enclosures.
- Keep LiPo batteries protected from puncture, heat, overcharging, short circuits, and physical damage.
- Mount hardware securely to avoid vibration damage, shorts, or loose wiring.
- Use a siren timeout or fail-safe to prevent continuous activation.
- Test the system in a controlled environment before relying on it.
- Verify that a physical kill switch or other safe silencing method works.
- Avoid placing exposed electronics where moisture, heat, vibration, or tampering could create hazards.

This repository is not a substitute for professional electrical, automotive, security, or life-safety system design.

---

## Home Assistant and ESPHome Security Recommendations

Deployments based on this repository should follow secure Home Assistant and ESPHome practices.

Recommended safeguards include:

- Use strong, unique Home Assistant credentials.
- Enable multi-factor authentication for Home Assistant.
- Avoid exposing Home Assistant directly to the internet.
- Use a trusted VPN or secure remote access method when possible.
- Protect ESPHome API access with encryption keys.
- Protect OTA updates with strong passwords.
- Avoid leaving fallback hotspots enabled unnecessarily.
- Avoid publishing dashboards that expose alarm controls.
- Limit who can arm, disarm, silence, or modify alarm automations.
- Use secrets files for sensitive values.
- Keep Home Assistant, ESPHome, ESP32 firmware, Frigate, and related integrations updated.
- Review automation logic after updates.
- Keep backups of working configurations.
- Test fail-safe behavior after configuration changes.

---

## Privacy and Surveillance Considerations

This project may integrate with cameras, Frigate NVR, mobile notifications, and video clips. Users are responsible for complying with applicable privacy laws, recording laws, notification rules, and local regulations.

Do not use this project to:

- Record people illegally.
- Track people without authorization.
- Harass, stalk, or intimidate others.
- Publish private camera footage.
- Capture or distribute license plates, faces, addresses, or private activity without a lawful reason.
- Monitor property, vehicles, or devices that you do not own or have authorization to protect.

When sharing examples, screenshots, videos, or logs, remove identifying information first.

---

## Configuration Safety Standards

Configuration files, documentation, and examples in this repository should follow these standards whenever possible:

- Prefer secure defaults.
- Use placeholders instead of real credentials.
- Use Home Assistant `secrets.yaml` for sensitive values.
- Include warnings before destructive or high-risk changes.
- Clearly identify optional features that may increase risk.
- Include safe timeout behavior for sirens and alerts.
- Avoid recommending direct internet exposure.
- Avoid hardcoding private IP addresses tied to real deployments.
- Avoid including personal camera names, vehicle names, addresses, or device identifiers.
- Clearly separate lab examples from production deployment examples.
- Warn users when automations may trigger audible alarms, notifications, cameras, or relays.
- Include manual override or kill-switch considerations where practical.

---

## Scripts, YAML, and Automation Logic

Any YAML, scripts, or automation logic included in this repository should be reviewed carefully before use.

Automation should avoid:

- Hardcoded credentials.
- Unprotected alarm control services.
- Unrestricted dashboard controls.
- Unlimited siren runtime.
- Silent failure when sensors are unavailable.
- Trigger loops that repeatedly activate alarms.
- Unsafe relay defaults.
- Automatically trusting unverified sensors.
- Uploading logs, images, clips, or notifications to third-party services without clear notice.
- Exposing private camera feeds or alarm controls through public URLs.

Where practical, automations should include safe defaults, clear comments, fail-safe behavior, and manual override options.

---

## Response Timeline

Pacific Northwest Computers will make a best effort to follow this timeline:

| Stage | Target Timeline |
| --- | --- |
| Initial acknowledgment | Within 3 business days |
| Initial review | Within 7 business days |
| Fix, mitigation, or status update | As soon as reasonably practical |
| Public disclosure, if appropriate | After a fix or mitigation is available |

Response times may vary depending on workload, report complexity, hardware testing requirements, and whether additional review is required.

---

## Security Fix Process

When a valid issue is confirmed, maintainers may take one or more of the following actions:

- Remove exposed sensitive information.
- Rewrite unsafe documentation.
- Update affected YAML, examples, scripts, or wiring notes.
- Add warnings, safer defaults, or validation.
- Improve timeout, fail-safe, or manual override behavior.
- Recommend credential rotation if exposure is suspected.
- Add `.gitignore` rules or example configuration files.
- Add sanitization guidance for screenshots, logs, and examples.
- Open a private or public advisory when appropriate.
- Credit the reporter if requested and appropriate.

---

## Legal and Ethical Use

This project is intended for lawful, defensive, personal, educational, and authorized security use only.

Users are responsible for:

- Complying with all applicable laws and regulations.
- Obtaining authorization before monitoring, recording, or protecting property that is not theirs.
- Respecting privacy and data protection requirements.
- Using alarms, sirens, cameras, and notifications responsibly.
- Following local rules related to audible alarms, vehicle electronics, cameras, and surveillance.
- Ensuring hardware is installed safely.

Do not use this project for unauthorized surveillance, stalking, harassment, physical tampering, alarm bypass, credential theft, or illegal activity.

---

## No Warranty

This repository is provided for educational, experimental, and reference purposes.

Security reports and fixes are handled on a best-effort basis. This policy does not create a warranty, service-level agreement, support contract, or legal obligation.

Use this project at your own risk. Test thoroughly before relying on it for property protection.

---

## Contact

For security reports:

**support@pnwcomputers.com**

For general documentation feedback, non-sensitive bugs, or feature requests, please use the normal GitHub issue process.
