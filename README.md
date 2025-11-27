[//]: # (STANDARD README)
[//]: # (https://github.com/RichardLitt/standard-readme)
[//]: # (----------------------------------------------)
[//]: # (Uncomment optional sections as required)
[//]: # (----------------------------------------------)

[//]: # (Title)
[//]: # (Match repository name)
[//]: # (REQUIRED)

# sunshineos

[//]: # (Banner)
[//]: # (OPTIONAL)
[//]: # (Must not have its own title)
[//]: # (Must link to local image in current repository)

> [!IMPORTANT]
> **Pre-pre-alpha**
>
> SunshineOS is currently in active design and initial prototyping. Some sections of this README describe intended
> behaviour before implementation.
> 
> SunshineOS is not production ready yet!

[//]: # (Badges)
[//]: # (OPTIONAL)
[//]: # (Must not have its own title)



[//]: # (Short description)
[//]: # (REQUIRED)
[//]: # (An overview of the intentions of this repo)
[//]: # (Must not have its own title)
[//]: # (Must be less than 120 characters)
[//]: # (Must match GitHub's description)

The little tug that guides your servers safely into Drydock

[//]: # (Long Description)
[//]: # (OPTIONAL)
[//]: # (Must not have its own title)
[//]: # (A detailed description of the repo)

SunshineOS is a tiny discovery operating system that reports hardware data to his Harbourmaster, such as a metrics or
inventory system. Though originally built to be used with *[Learn more...](http://github.com/evoteum/drydock)*,
SunshineOS can report to any Harbourmaster.


## Table of Contents

[//]: # (REQUIRED)
[//]: # (Managed automatically)
[//]: # (Changes between the TABLE_OF_CONTENTS_START and TABLE_OF_CONTENTS_END markers will be overritten)

[//]: # (TOCGEN_TABLE_OF_CONTENTS_START)

- [Install](#install)
- [Usage](#usage)
- [Documentation](#documentation)
- [Repository Configuration](#repository-configuration)
- [Contributing](#contributing)
- [License](#license)
    - [Code](#code)
    - [Non-code content](#non-code-content)

[//]: # (TOCGEN_TABLE_OF_CONTENTS_END)

## Security
[//]: # (OPTIONAL)
[//]: # (May go here if it is important to highlight security concerns.)

SunshineOS will be a minimal operating system, minimising its attack surface. Nonetheless, it should not be used beyond
periodic metrics gathering.

## Background
[//]: # (OPTIONAL)
[//]: # (Explain the motivation and abstract dependencies for this repo)

[Drydock](http://github.com/evoteum/drydock) needs a way to automatically gather key information about a physical server
so that it can build a [Tinkerbell hardware manifest](https://tinkerbell.org/docs/concepts/hardware/). At minimum,
Tinkerbell requires MAC addresses, so while we are there, we also gather as much useful info as possible. This
will make SunshineOS useful not only to Drydock but also to any metrics system that wants,
- more info than a "normal" operating system can provide
- a single API to gather information, regardless of the regular operating system.

## Install

[//]: # (Explain how to install the thing.)
[//]: # (OPTIONAL IF documentation repo)
[//]: # (ELSE REQUIRED)

SunshineOS is designed to PXE boot onto a machine in memory. It never installs itself to disk.

If you already have PXE infrastructure, you can make it available as a bootable machine image. If you do not already
have PXE infrastructure, and want to get Kubernetes up and running, take a look at
[Drydock](http://github.com/evoteum/drydock).

## Usage
[//]: # (REQUIRED)
[//]: # (Explain what the thing does. Use screenshots and/or videos.)

SunshineOS provides machine hardware data to its Harbourmaster. That's it.

Drydock uses this data to emit a [Tinkerbell hardware manifest](https://tinkerbell.org/docs/concepts/hardware/) for each
machine, that Tinkerbell then uses to take over operating system provisioning.

[//]: # (Extra sections)
[//]: # (OPTIONAL)
[//]: # (This should not be called "Extra Sections".)
[//]: # (This is a space for ≥0 sections to be included,)
[//]: # (each of which must have their own titles.)

## Beyond the Drydock

While SunshineOS was primarily designed for Drydock, it can be useful around your "Harbour" too. For example,

1. Hull Blueprint (True Hardware Identity)<br/>
SunshineOS can surface immutable identifiers like serials, baseboard IDs and exact manufacturer details that other OSes hide behind drivers or vendor agents.
2. Engine Room Hours (Total Power-On and Boot Cycles)<br/>
Reads raw firmware counters without relying on OS-level logging, giving a trustworthy view of component age and wear.
3. Cargo Hold Map (Accurate Storage Layout)<br/>
Reports the real disk map, partitions, hidden vendor regions, wear-level stats and SMART data—untainted by OS abstractions or storage drivers.
4. Propeller Health (Thermal & Fan Telemetry)<br/>
Retrieves sensor data directly from hardware buses, unaffected by vendor daemons that often under-report or round values.
5. Fuel Lines & Consumption (Power Delivery + PSU Status)<br/>
Exposes PSU metadata, voltages and fault indicators that Windows/Linux typically cannot standardise across hardware vendors.
6. Anchor Chains (Accurate NIC + Firmware Metadata)<br/>
Enumerates physical network interfaces, link training, offload capabilities and firmware versions—unconfused by OS bonding, VLANs or virtual NIC overlays.
7. Harbour Registry (Firmware & BMC Versions)<br/>
Reports BIOS/UEFI, BMC/IPMI, ME/PSP versions consistently, which normal OSes often hide behind vendor-specific tooling.
8. Structural Integrity (Memory Topology & Health)<br/>
DIMM slot mapping, ECC status, bank population and error counters pulled from SMBIOS and memory controllers rather than OS layers.
9. Ballast & Trim (Chassis Sensors & Form-Factor Detection)<br/>
Reports chassis intrusion status, physical form factor, rack/slot identity and other hardware metadata normally absent from general OSes.
10. Weather Deck Conditions (Boot Device & PXE Capabilities)<br/>
Provides exact boot order, PXE support level, boot ROM versions and network boot readiness—critical for provisioning flows but fragile under a normal OS.

Perhaps the best bit is that SunshineOS will be able to report all this on a single, easy to use API, no matter what
operating system normally runs on that box. This could, for example, be particularly useful to your favourite asset
management system!

## FAQ
### Why not just use Linux?
SunshineOS is designed to allow you to get to the stage where you can automatically install a full operating system, including but not
limited to Linux, without having to manually inventory your hardware. Manually installing operating systems on to
dozens, hundreds, or perhaps even thousands, of physical servers is
*[not fun](https://en.wikipedia.org/wiki/English_understatement)*, so SunshineOS is part of the puzzle necessary to
automate that from end to end.

### Where did the name "SunshineOS" come from?

SunshineOS is named after the small but capable tug boat, [Sunshine](https://tugs.fandom.com/wiki/Sunshine), from the
80's TV show "[TUGS](https://en.wikipedia.org/wiki/Tugs_(TV_series))". This is because we love,
- obscure pop culture references.
- furthering the maritime theme of Kubernetes.

### How big will it be?

As small as possible, because the smaller he is, the faster he gets running, does his job, and then gets out of the way.
We are currently targeting 20MB.

For perspective, Candy Crush is approximately [326.2MB](https://apps.apple.com/cd/app/candy-crush-saga/id553834731). Not
really a fair "like for like" comparison, but you get the point!

## Documentation

Further documentation is in the [`docs`](docs/) directory.

## Repository Configuration

> [!WARNING]
> This repo is controlled by OpenTofu in the [estate-repos](https://github.com/evoteum/estate-repos) repository.
>
> Manual configuration changes will be overwritten the next time OpenTofu runs.


[//]: # (## API)
[//]: # (OPTIONAL)
[//]: # (Describe exported functions and objects)



[//]: # (## Maintainers)
[//]: # (OPTIONAL)
[//]: # (List maintainers for this repository)
[//]: # (along with one way of contacting them - GitHub link or email.)



[//]: # (## Thanks)
[//]: # (OPTIONAL)
[//]: # (State anyone or anything that significantly)
[//]: # (helped with the development of this project)



## Contributing
[//]: # (REQUIRED)
If you need any help, please log an issue and one of our team will get back to you.

PRs are welcome.


## License
[//]: # (REQUIRED)

### Code

All source code in this repository is licenced under the [GNU Affero General Public License v3.0 (AGPL-3.0)](https://www.gnu.org/licenses/agpl-3.0.en.html). A
copy of this is provided in the [LICENSE](LICENSE).

### Non-code content

All non-code content in this repository, including but not limited to images, diagrams or prose documentation, is
licenced under the
[Creative Commons Attribution-ShareAlike 4.0 International](https://creativecommons.org/licenses/by-sa/4.0/) licence.
