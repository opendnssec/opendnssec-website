---
hide:
  - navigation
  - toc
---

## The OpenDNSSEC project

OpenDNSSEC is a policy-based zone signer that automates the process of keeping track of DNSSEC keys and the signing of zones. The goal of the project is to make DNSSEC easy to deploy. The project is Open Source and intends to drive adoption of Domain Name System Security Extensions (DNSSEC) to further enhance Internet security.

## End-of-Life Roadmap for OpenDNSSEC

From October 2027, OpenDNSSEC reaches its official End-of-Life and no further updates or support will be provided. From October 2025, no new features will be developed, only critical bug fixes and security updates will be released. More information is available as part of [the end-of-life roadmap for OpenDNSSEC](https://www.nlnetlabs.nl/news/2025/Oct/03/opendnssec-eol-announcement/), that was announced on October 3, 2025. Users are encouraged to begin evaluating [Cascade](https://blog.nlnetlabs.nl/cascade/) as the successor DNSSEC signing solution to OpenDNSSEC and plan for a migration.

## OpenDNSSEC 2.1.14

Version 2.1.14 of OpenDNSSEC has been released on 2024-08-22.

**News**

This is a mainenance release that fixes some bugs and adds robustness for HSM outages.  Apart from a minor fix to the backup keys command and export keys, it solved an issue where keys were not published soon enough in special cases in combination with <SharedKeys> directive.  In case you use shared keys, you must update.  But this is a good idea anyway.

**Download**

- [https://github.com/opendnssec/opendnssec/releases/download/2.1.14/opendnssec-2.1.14.tar.gz](https://github.com/opendnssec/opendnssec/releases/download/2.1.14/opendnssec-2.1.14.tar.gz)
- [https://github.com/opendnssec/opendnssec/releases/download/2.1.14/opendnssec-2.1.14.tar.gz.sig](https://github.com/opendnssec/opendnssec/releases/download/2.1.14/opendnssec-2.1.14.tar.gz.sig)
- Checksum SHA256: 5a68d62ea0ea3a6c61e9f4946f462c7b907fbe6bccc9e8a721b7fe0f906f95d0

## OpenDNSSEC 2.1.13

Version 2.1.13 of OpenDNSSEC has been released on 2023-06-26.

**News**

This release fixes a bug that affects both signer and enforcer command
line handling. Under heavy usage of the command line there was a small
change for a crash.
Furthermore there is a small behavioural change for users of the “keep”
policy. The back-off for retrying a sign task change is now equal to
the resign period in case the input file isn’t available or updated.
This because users nearly always will emit an external sign command for
this period. This will reduce logging errors.

**Download**

- [https://github.com/opendnssec/opendnssec/releases/download/2.1.13/opendnssec-2.1.13.tar.gz](https://github.com/opendnssec/opendnssec/releases/download/2.1.13/opendnssec-2.1.13.tar.gz)
- [https://github.com/opendnssec/opendnssec/releases/download/2.1.13/opendnssec-2.1.13.tar.gz.sig](https://github.com/opendnssec/opendnssec/releases/download/2.1.13/opendnssec-2.1.13.tar.gz.sig)
- Checksum SHA256: 50d7b9b0ccfc6a502784606ca4e5c03680fcf6425fb3947f45d8809ea8503e59

## OpenDNSSEC 2.1.12

Version 2.1.12 of OpenDNSSEC has been released on 2022-11-08.

**News**

This is a maintenance release of OpenDNSSEC addressing additional issues relating to the previous bug-fix release. Both installations that use shared keys or want to use salt lengths of zero must use this release. Other installations will benefit to from better reporting in case of issues.

**Issues**

- Ensure debug symbols on RPM-style builds;
- Bug fix that prevented restoring state from when salt length was zero;
- Bug fix for enforcer daemon crash after deleting key on some systems.

**Download**

- [https://github.com/opendnssec/opendnssec/releases/download/2.1.12/opendnssec-2.1.12.tar.gz](https://github.com/opendnssec/opendnssec/releases/download/2.1.12/opendnssec-2.1.12.tar.gz)
- [https://github.com/opendnssec/opendnssec/releases/download/2.1.12/opendnssec-2.1.12.tar.gz.sig](https://github.com/opendnssec/opendnssec/releases/download/2.1.12/opendnssec-2.1.12.tar.gz.sig)
- Checksum SHA256: 50d7b9b0ccfc6a502784606ca4e5c03680fcf6425fb3947f45d8809ea8503e59
