---
title: "Configuration Options"
weight: 20
---

## Setup
TelemetryJet has several global configuration settings. Configuration can be set via a `.telemetryjet` file containing JSON key/values, or via environment variables.

When the server starts, configuration loads in the following priority (Lower numbers override higher numbers):

1. Environment Variables
2. A `.telemetryjet` file in the working directory
3. A `.telemetryjet` file in the user's home directory
4. Program defaults

The `.telemetryjet` file must contain JSON with a flat structure. If the file is invalid, it will be ignored.

### Example of a .telemetryjet config file:

{{< highlight json >}}
{
    "data_dir" : "~/telemetryjet"
}
{{< / highlight >}}

### Example of Environment Variables

Environment Variables override the JSON configuration. All options are set using variables prefixed with `TELEMETRYJET_`. For example, to set the data directory before running the server:

{{< highlight bash >}}
export TELEMETRYJET_DATA_DIR=../data
{{< / highlight >}}

## List of Options

<table class="bp3-html-table bp3-html-table-bordered bp3-small">
  <thead>
    <tr>
      <th>JSON Key</th>
      <th>Environment Variable</th>
      <th>Type</th>
      <th>Default</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>data_dir</td>
      <td>DATA_DIR</td>
      <td>String</td>
      <td>"~/telemetryjet"</td>
      <td>Path to the "data directory", a folder which holds all the files TelemetryJet exports, such as the SQLite database.</td>
    </tr>
  </tbody>
  <tbody>
    <tr>
      <td>logging</td>
      <td>LOGGING</td>
      <td>Boolean</td>
      <td>true</td>
      <td>Turns all logging on and off. Note: This will only affect initialization log messages if set via environment variable.</td>
    </tr>
  </tbody>
</table>


...