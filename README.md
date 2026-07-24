<!-- markdownlint-disable MD007 -- Unordered list indentation -->
<!-- markdownlint-disable MD010 -- No hard tabs -->
<!-- markdownlint-disable MD033 -- No inline html -->
<!-- markdownlint-disable MD055 -- Table pipe style [Expected: leading_and_trailing; Actual: leading_only; Missing trailing pipe] -->
<!-- markdownlint-disable MD041 -- First line in a file should be a top-level heading -->
<div align="center">

[![made-with-rust](https://img.shields.io/badge/Made%20with-Rust-1f425f.svg)](https://www.rust-lang.org/)
[![License: GPL v2+](https://img.shields.io/badge/License-GPLv2%2B-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html)
![Lifecycle: Alpha](https://img.shields.io/badge/Lifecycle-Alpha-orange)
![Support](https://img.shields.io/badge/Support-Maintained-brightgreen)

</div>
<!--
[![!#/bin/bash](https://img.shields.io/badge/-%23!%2Fbin%2Fbash-1f425f.svg?logo=gnu-bash)](https://www.gnu.org/software/bash/)
[![made-with-python](https://img.shields.io/badge/Made%20with-Python-1f425f.svg)](https://www.python.org/)
[![made-with-rust](https://img.shields.io/badge/Made%20with-Rust-1f425f.svg)](https://www.rust-lang.org/)
![Go](https://img.shields.io/badge/Go-00ADD8?logo=go&logoColor=white)
![Made with](https://img.shields.io/badge/Made%20with-C%2B%2B-brightgreen?style=plastic)
![Made with](https://img.shields.io/badge/Made%20with-Unreal%20Engine-critical?style=plastic)
[![made-with-javascript](https://img.shields.io/badge/Made%20with-JavaScript-1f425f.svg)](https://www.javascript.com)
![License: GPL v2](https://img.shields.io/badge/License-GPLv2-blue.svg)
[![License: GPL v2+](https://img.shields.io/badge/License-GPLv2%2B-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.html)
![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![License: MPL 2.0](https://img.shields.io/badge/License-MPL_2.0-brightgreen.svg)](https://opensource.org/licenses/MPL-2.0)
![Lifecycle: Alpha](https://img.shields.io/badge/Lifecycle-Alpha-orange)
![Lifecycle: Beta](https://img.shields.io/badge/Lifecycle-Beta-yellow)
![Lifecycle: RC](https://img.shields.io/badge/Lifecycle-RC-blue)
![Lifecycle: Stable](https://img.shields.io/badge/Lifecycle-Stable-brightgreen)
![Lifecycle: Deprecated](https://img.shields.io/badge/Lifecycle-Deprecated-red)
![Status: Deprecated](https://img.shields.io/badge/Status-Deprecated-orange)
![Status: Archived](https://img.shields.io/badge/Status-Archived-lightgrey)
![Lifecycle: EOL](https://img.shields.io/badge/Lifecycle-EOL-lightgrey)
![Coverage](https://img.shields.io/badge/Coverage-25%25-red)
![Coverage](https://img.shields.io/badge/Coverage-50%25-orange)
![Coverage](https://img.shields.io/badge/Coverage-75%25-yellow)
![Coverage](https://img.shields.io/badge/Coverage-90%25-brightgreen)
![Status: Passing](https://img.shields.io/badge/Status-Passing-brightgreen)
![Status: Failing](https://img.shields.io/badge/Status-Failing-red)
[![GitHub Sponsors](https://img.shields.io/github/sponsors/jim-collier?logo=GitHub%20Sponsors&style=social)](https://github.com/sponsors/jim-collier)
-->

<!-- TOC ignore:true -->
# Captain Nemo

Captain Nemo is a next-generation port of [Nemo Anywhere](https://github.com/t00mietum/nemo-anywhere).

This is placeholder project for now. Real coding work won't begin until [Nemo Anywhere](https://github.com/t00mietum/nemo-anywhere) has it's first stable release.

(Nemo Anywhere is itself a hard fork of the OG Linux Mint [Nemo](https://github.com/linuxmint/nemo) file manager, which in turn was a hard fork of Gnome [Nautilus](https://github.com/GNOME/nautilus) file manager.)

<!-- TOC ignore:true -->
## Table of contents

<!-- TOC -->

- [Why](#why)
- [Features](#features)
- [Installing](#installing)
- [Building from source](#building-from-source)
- [Contributing](#contributing)
- [Copyright and license](#copyright-and-license)

<!-- /TOC -->

## Why

The sister project [Nemo Anywhere](https://github.com/t00mietum/nemo-anywhere) was the first step in:

- Removing Cinnamon Desktop dependencies from Nemo, so that it can install cleanly on non-Cinnamon desktop environments.

- Removing desktop management functionality. (While that was arguably fine for the Cinnamon Desktop, conceptually Nemo is a file manager first and foremost - it shouldn't also be a desktop manager. Arguably, the "Desktop" should in general be a separate program, independent of a separate file manager.)

- Porting to fully-functional, first-class Windows and macOS applications.

- Adding a few "quality of life" features and default settings.

But for truly maximum cross-platform portability, Nemo Anywhere needs to eventually move off of not just GTK+ v3, but GTK+ period. While it works, GTK+3 is no longer actively developed, is basically stuck with C, and is comparatively weak and fragile on Windows and macOS. (GTK+ was never originally designed to run on Windows or macOS, and they remain sort of "second-class citizens".)

There were originally two main options being considered for Captain Nemo (once Nemo Anywhere reaches v1.0.0 stable):

- Rust and QML. (QML is the next evolution of Qt widgets.) This is the most viable language option for moving away from C and for long-term maintenance. But the only viable QML bindings for Rust is `cxx-qt`. While it seems fine for now, it also carries a non-trivial vendor dependency and risk.

	- Mitigation strategy: Use `cxx-qt`, but also maintain a hard-forked subset of only the parts needed, and keep it up-to-date as we go. If and when the time comes that `cxx-qt` is ever abandoned, falls behind QML, and/or pursues different goals: Our minimal hard fork is ready to go.

- Idiomatic/RAII C++ v23, combined with native QML bindings. Harder to port the code (ironically in spite of both having the same ancestry), but less risk with QML.

Rust and QML seems the obvious choice going forward.

## Features

## Installing

## Building from source

## Contributing

See [contributing.md](contributing.md) for process, and [style-guide.md](style-guide.md) for code and doc style.

## Copyright and license

This is an all-new work, with so far a singular copyright holder. But obviously with an existing open-source project to base logic and look-and-feel on.

So it's well-worth acknowledging the great effort and years of development by the [many contributors](https://github.com/linuxmint/nemo/graphs/contributors) of the Linux Mint project (and original Nemo).

Without the [original Nemo](https://github.com/linuxmint/nemo), there would not have ever been [Nemo Anywhere](https://github.com/t00mietum/nemo-anywhere). And without that, no Captain Nemo.

The [original Nemo](https://github.com/linuxmint/nemo) is the work of the Linux Mint project, and is itself a hard fork from 2012 of [GNOME Files aka Nautilus](https://github.com/GNOME/nautilus).


> Copyright © 2026 Jim Collier (ID: 1cv◂‡Vᛦ)<br />
> Licensed under [GNU GPL v2 Or Later License](https://spdx.org/licenses/GPL-2.0-or-later.html) license. No warranty.
<!--
> Licensed under the [MIT License](https://mit-license.org/). No warranty.
> Licensed under the [GNU General Public License v2.0](https://www.gnu.org/licenses/gpl-2.0.html). No warranty.
> Licensed under the [GNU General Public License v2.0 or later](https://spdx.org/licenses/GPL-2.0-or-later.html). No warranty.
> Licensed under the [GNU General Public License v3](https://www.gnu.org/licenses/gpl-3.0.en.html) license. No warranty.
> Licensed under the [Mozilla Public License 2.0](https://mozilla.org/MPL/2.0/). No warranty.
-->