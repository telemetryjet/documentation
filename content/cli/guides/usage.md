---
title: "Usage"
weight: 2
menu:
  cli:
    parent: "cli_guides"
    identifier: "cli_usage"
    title: "Usage"
---

## Overview
Jet allows you to easily stream data between a number of data sources, including serial devices, files, and the TelemetryJet server. 

Jet uses declarative configuration: You specify the data source settings in a JSON file, and jet builds a network that connects all data sources in a file together.

## Basic Usage

To stream data, use the `jet stream` command. The command takes one or more JSON files as inputs:
<pre>
jet stream device.json # One configuration

jet stream device1.json device2.json # Multiple configurations

jet stream devices/*.json # All JSON files in a folder
</pre>

You can specify JSON files with relative paths, absolute paths, or [Glob syntax](https://en.wikipedia.org/wiki/Glob_(programming)) to select files using a pattern. 

Jet is completely stateless -- All the configuration is set using the files and parameters you pass to the program. This means you can put your configuration in a git repository, flash drive, or other sharing mechanism.

## Configuration Files

A configuration file defines a network of multiple data sources. All the data sources in a file can communicate with each other bidirectionally. 

**Note: Data sources defined in separate JSON files don't communicate with each other.**

Some data sources only transmit data, others only receive data, and many do both. For more details about which data sources transmit and receive data, see the [Data Source Types.](/cli/guides/data_sources/)

A configuration file contains an array of data source definitions:

<pre>
[
  {
    "id": "arduino1",
    "type": "&lt;data source type&gt;",
    "options": {
      &lt;options for the data source&gt;
    }
  },
  {
    "id": "arduino2",
    "prefix": "arduino2",
    "type": "&lt;data source type&gt;",
    "options": {
      &lt;options for the data source&gt;
    }
  }
]
</pre>


## Data Source Definitions
Each data source definition in the configuration file has a number of fields which define its properties:



<table class="bp3-html-table bp3-html-table-bordered bp3-html-table-condensed bp3-html-table-striped" style="width: 100%">
  <thead>
    <tr>
      <th style="width: 100px;">Field</th>
      <th style="width: 100px;">Type</th>
      <th style="width: 100px;">Required?</th>
      <th style="width: 200px;">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>id</code></td>
      <td>String</td>
      <td>Yes</td>
      <td>A display name for this data source, used to print debug information and errors.</td>
    </tr>
    <tr>
      <td><code>type</code></td>
      <td>String</td>
      <td>Yes</td>
      <td>Defines the type of data source. This must be a value from the list of <a href="/cli/guides/data_sources/">Data Source Types.</a></td>
    </tr>
    <tr>
      <td><code>prefix</code></td>
      <td>String</td>
      <td>No</td>
      <td>If provided, the prefix is inserted in front of any keys sent by this data source.</td>
    </tr>
    <tr>
      <td><code>options</code></td>
      <td>Object</td>
      <td>No*</td>
      <td>An object with any options specific to the data source.<br/> Some <a href="/cli/guides/data_sources/">Data Source Types</a> have required options. This field can be omitted for data sources with no required options.</td>
    </tr>
  </tbody>
</table>

## Advanced Usage
### Disconnect/Reconnect Behavior
Jet will continue running until you exit it with an interrupt signal (Ctrl-C on most platforms.) If any hardware data sources disconnect, jet will periodically poll and reconnect to the data source when it is available.

If you would like to exit as soon as an input or output data source is unavailable, specify the `--exit` flag. This will cause jet to throw an error and exit if any devices disconnect, or if no more data is available from a data source.