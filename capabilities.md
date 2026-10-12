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

To input parameters, use the `params` field of the JSON you POST to `/capability`. More information on specific params are in the docs listed in [Capabilities Table](#capabilities-table).

## Capabilities Table

Below is an **exhaustive table** of *capabilities*, *IDs*, and *links to docs* that can be done on a host if allowed:

<!-- what capabilities? -->