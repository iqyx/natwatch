# The NW-R platform specification

> Abstract goes here


> Copyright notice goes here

## Introduction

### Motivation

Over the time it became clear that the original NatWatch platform is not well suited for many
intended applications and there are reasons to make some improvements. Some of the discovered
problems can be solved with updates to the original NatWatch specification still
preserving a degree of compatibility with older designs. However, from the long term point of
view, it may be favorable to step forward and create a brand new (albeit incompatible) platform
resolving all issues known so far.

The new NW-R specification tries to resolve the same as the original one. It helps if there is
a need for a platform:

- that is easily extendable with the possiblity to make your own compatible hardware
- used mainly for research, data acquisition, communication or similar purposes (disaster recovery)
- having professional look and feel
- usually working unattended in rough environments
- made of current hardware and using current technologies
- without IoT and make:r hype
- which does not cost you an arm and leg

### Maintaining the specs

In order to track changes, allow contributions and keep all old versions accessible, text of
the specification is kept in a Git repository.

The used workflow is based on GitFlow. Contributions are made to separate *feature* branches.
Feature branches are reviewed and merged to the *develop* branch. If a release is to be made,
it is tagged with a version and merged to the *master* branch. If a hotfix is to be made, a hotfix
branch is created from the release. Hotfix contributions are then merged directly to the *master*
branch and tagged with appropriate version.

The specification uses [Semantic Versioning](https://semver.org/spec/v2.0.0.html). All versions
created before a first hardware is validated in the field are 0.y.z. The first stable version
of the specification will be 1.0.0. All subsequent versions making compatible changes (ie. extending
the previous version) will increase the minor number (1.x.y). Hotfix releases will increase the
hotfix number. If there is a requirement to make an incompatible change to the specification,
the major version number is increased (resetting minor and hotfix to zero).

### Conventions used in the document

The document roughly follows [RFC Style Guide](https://tools.ietf.org/html/rfc7322). Language specfied
in [RFC 2119](https://tools.ietf.org/html/rfc2119) is used to indicate requirement levels. Motivation
for the section in question or general contributor thoughs can be found in notes:
> This is a note.

The specification does not contain appendices. All related information should be contained within
the section itself.


## Resolving compatibility of the hardware

A device (eg. a board) MUST indicate compatibility with this specification using a major.minor.hotfix
identifier. Major is a single number or a range of numbers with a format %u or %u-%u respectively. Minor
MUST be a single number. Hotfix should be 0 or "x".

A device is compatible with the specification if:
- major numbers are equivalent or the specification's major number is in the range indicated by the device
  compatibility identifier
- minor number of the device compatibility identifier is equal or greater than the one of the specification
- hotfix number doesn't care

Example: a device specifies it is compatible with *1.4.x* version of this specification. It means:
- it may or may not be compatible with any development version (*0.y.z*)
- it is compatible with any versions with minor numbers lower or equal than required, eg. *1.2.3*, because
  it implements all requirements of the *1.0.0* version together with changes added in *1.1.0* and *1.2.0*
	versions. *1.2.3* hotfix release just fixes some errors in non-normative text.
- it is incompatible with *1.6.0* because it may lack some features required by *1.5.0* and *1.6.0* changes.
- it is incompatible with any *2.y.z* version because it may require some features not included anymore.

In practice resolving compatibility between devices may be more complicated. An example is a backplane
accepting boards compatible with more than one version of the specification. Or it may provide all features
required by the current version of the specification but it may still accept devices (boards) compatible
with older versions of the specification.

## Board size and outline

## Backplane-to-board electrical interface

### Connector type and position

### Connector signals

#### Low-power power rail (VBUS-LP)

1. The low-power rail is on the top side of the board on pins B1, B2, B3 and B4. If the low-power
   rail is used, the board SHOULD contain an ESD protection/transient suppression.

2. Nominal voltage of the low-power rail is 5V. The voltage MAY deviate depending on the circumstances.
   
3. A board MAY sink power from the low-power rail. The input range of the board MUST be 4.5V to 5.5V.
   4.5V is considered an undervoltage and the board sinking power from such low-power rail SHOULD be held
   in a brown-out reset state. 5.5V is considered an overvoltage. In this case the board MAY cut the power
   to protect itself in a suitable way. The board SHOULD clamp the low-power rail voltage at 6V or more.
   The board MUST contain a hotplug controller/e-fuse with a suitable current limiting including
   inrush current limiting.

4. A board MAY supply power to the low power rail. If so:
- it MUST provide a power-or capability (a diode, ideal-diode controller with a transistor, etc.)
- the supplied power MUST be limited to a 4A corrent draw at 5V
- the supplied voltage must be in the range 4.8V to 5.2V

#### Signal ground (GND)

Signal ground is connected to the chassis at multiple points where connectors protrude the chassis. If a ground
loops are to be avoided on a board, isolated front panel connectors MUST be used.

Signal ground is available on pins A1, A2, A3, A4, A5 and B5.

> Chassis, front panel, front panel connectors, etc. should be defined first.

#### I2C signals (SCL, SDA)

An I2C bus is available for low-speed (100kbit/s) communication over the backplane. It contains SCL (B6), SDA (B7) and
an accompanying GND (B8).

#### CAN 2.0b/CAN FD signals

A CAN/CAN-FD bus is available for medium-speed (1mbit/s) communication over the backplane. It contains
CANH (B10), CANL (B11) and GND (B9).

#### Unused connections

All connections not listed in the previous sections MUST NOT be connected (ie. they MUST be left floating).
They are reseved for future use.


## Acknowledgements

## Contributing
