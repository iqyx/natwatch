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

## Acknowledgements

## Contributing
