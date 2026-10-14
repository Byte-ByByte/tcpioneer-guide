# Capabilities

## Introduction

Capabilities define what interactions a client can operate onto a host.
Capabilities are defined in the server's `capabilities.json`. Capabilities include:

* Mouse control
* Keypress and type control
* On-demand screenshot access
* Terminal access

## Usage

To use these capabilities, use the API endpoint `/capability`. More information is found at [Run Capability (/capability)](/guide/endpoints/capability).

To input parameters, use the `params` field of the JSON you POST to `/capability`. More information on specific params are in the docs listed in [Capabilities Table](#capabilities-table), and more information about the endpoint is at [Run Capability (/capability)](/guide/endpoints/capability).

## Tasks

A task in a capability is essentially a sub-capability. They can be enabled or disabled similar to capabilities themselves.

More specifically, a task is an integer that tells the capability which of its supported features the client wants to run. Clients can only run one task per request because return values may differ between tasks.

To choose a task, use the `task` field of the JSON you POST to `/capability`. More information on specific params are in the docs listed in [Capabilities Table](#capabilities-table).

## Capabilities Table

Below is an **exhaustive table** of *capabilities*, *IDs*, and *links to docs* that can be done on a host if allowed:

| Name | ID | Documentation |
|------|----|---------------|
|Keyboard|keyboard|[Keyboard (capability)](/guide/capabilities/keyboard)
|Mouse|mouse|[Mouse (capability)](/guide/capabilities/mouse)
|Screenshot|screenshot|[Screenshot (capability)](/guide/capabilities/screenshot)
|Terminal|terminal|[Terminal (capability)](/guide/capabilities/terminal)