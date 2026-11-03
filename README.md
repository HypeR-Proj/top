<!--
SPDX-FileCopyrightText: 2026 roolrz
SPDX-License-Identifier: Apache-2.0
-->

# top

Interactive and batch monitor for Native process, CPU and memory observations.

Samples task, CPU and memory inspectors; `lib-text-ui` owns fullscreen rendering support
and `lib-tool-args` shares filters and interval parsing. The first frame is rendered
immediately, before the refresh interval elapses.

See the [implementation entry](src/main.rs) and [component declaration](component.json)
for the public interfaces, build dependencies and delivered artifacts.

## Usage

In a Native session with the required capabilities:

```sh
top --help
top -b -n 2 -d 1
```

## Boundaries

CPU rates require successive samples. The initial frame therefore has no previous
interval from which to calculate a rate. Observation and control are separate: the
monitor does not acquire process-management authority.

## Build and test

Use this checkout inside the [repo-managed workspace](https://github.com/HypeR-Proj/HypeR).
From this repository directory:

```sh
make
make test
```

An absolute `OUT=/path/to/out` selects a shared output directory. The module
entry delegates to build/system, which prepares the installed SDK and declared
dependencies. Native binaries require HypeR; host module checks cover the tests
selected by component.json. A standalone clone does not contain the workspace’s
other source repositories or Native SDK.
