# Git projects and application examples

Updated 2026-10-30. The following seven original repositories were read or checked through their metadata. Commit identifiers are recorded in [repositories.json](../sources/repositories.json). A link does not establish compatibility or qualification.

| Project / reviewed commit | Purpose | Limit |
| --- | --- | --- |
| [waveshareteam/ESP32-P4-Platform](https://github.com/waveshareteam/ESP32-P4-Platform/tree/6f78fa810ec505048c1941e3d09cefc9f29129bd) · `6f78fa81` | Manufacturer examples and board/revision configuration: baseline checks, Ethernet, SD, audio, MIPI and UI. | Use a matching configuration; some examples default to 16-MB flash. |
| [espressif/esp-idf](https://github.com/espressif/esp-idf/tree/735507283d5b2f9fb363a1901172dbd9e847945d) · `73550728` | SDK used in the existing test setup; Ethernet, memory and device drivers. | v5.5.4 is the documented test version, not a claim about the latest release. |
| [espressif/esp-hosted](https://github.com/espressif/esp-hosted/tree/a0422923d01fa5cd5f4987885fe743656398b7c5) · `a0422923` | Overview repository for the Hosted family. | Active MCU implementation is now in esp-hosted-mcu; check license files for the parts used. |
| [espressif/esp-hosted-mcu](https://github.com/espressif/esp-hosted-mcu/tree/78b1c1c43c02b0c4e898cf87f94679278b1ddaff) · `78b1c1c4` | Wireless connectivity for an MCU host through an Espressif coprocessor. | Host and C6 firmware must match; owner wireless testing remains open. Check component licenses. |
| [espkvm/espkvm](https://github.com/espkvm/espkvm/tree/39273c3db6fc2d02dacf596d635938c666af836c) · `39273c3d` | IP-KVM example linked by the manufacturer for this board. | Requires extra HDMI-to-CSI hardware, a revision-appropriate build and electrical review. Not installed here. |
| [jrowny/p4kvm](https://github.com/jrowny/p4kvm/tree/18e0b85735d9569d4264fe4d5b58f6659c148680) · `18e0b857` | Early Ethernet KVM proof of concept with TC358743 for pre-revision-3 P4 chips. | README identifies missing security and proof-of-concept status; no operating qualification here. Check licenses before reuse. |
| [Mcgee1704/esp32-p4-llm-cluster-research](https://github.com/Mcgee1704/esp32-p4-llm-cluster-research/tree/0675f8687b9459fafa4545587ef14aedd118187d) · `0675f868` | Published owner experiments on P4 memory, Ethernet and distributed text inference. | Evidence for the documented setup, not complete board qualification. Mixed provenance: consult LICENSE and THIRD_PARTY. |

## Choosing a starting point

Manufacturer examples provide starting points for peripheral checks after the board profile and silicon revision are known. Existing owner tests establish IDF 5.5.4, 32 MiB flash, 32 MiB PSRAM and an operational IP101 Ethernet path. Wireless work needs matching C6 firmware. KVM, camera, display and audio each need their own verification.

Waveshare groups examples by baseline checks, interface and application. This repository does not copy third-party examples or binary images. Start with the official [resources](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH/Resources-And-Documents) and [ESP-IDF guidance](https://docs.waveshare.com/ESP32-P4-WIFI6-POE-ETH/ESP-IDF).

## Licenses and evidence limits

GitHub's `NOASSERTION` license identifier means the API does not provide one unambiguous SPDX repository-wide license. It implies neither public domain nor necessarily absent licensing. Review specific LICENSE files, file headers, subcomponents and third-party notices before reusing code. The research repository contains multiple provenance/license areas.

None of these projects was installed, built, flashed or served on a network as part of this catalog task or English translation. Historical owner findings are described in [Owner boards](05-own-boards.md).
