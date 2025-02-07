### What and Where

{{< truetable >}}
| Name | Description |
|------|------|
| **Load Previous Replication Task** | Use settings from a saved replication. |
| **Source Location** | Storage location for the original snapshots that are replicated. |
| **Destination Location** | Storage location for the replicated snapshots. |
| **Task Name** | Name of this replication configuration. |
{{< /truetable >}}

**Source Location: On this System**

{{< truetable >}}
| Name | Description |
|------|------|
| **Source** | Define the path to a system location that has snapshots to replicate. Click the folder to see all locations on the source system or click in the field to manually type a location (Example: *pool1/dataset1*). Multiple source locations can be selected or manually defined with a comma (,) separator.  Selecting a location displays the number of existing snapshots that can be replicated. Selecting a location that has no snapshots configures the replication task to take a manual snapshot of that location and replicate it to the destination. |
| **Recursive** | Select to also replicate all snapshots contained within the selected source dataset snapshots. Clear to only replicate the selected dataset snapshots. |
| **Replicate Custom Snapshots** | Replicate snapshots that are not created by an automated snapshot task. Requires setting a naming schema for the custom snapshots. |
| **Naming Schema** | Pattern of naming custom snapshots replicated. Enter the name and [strftime(3)](https://www.freebsd.org/cgi/man.cgi?query=strftime) {0}, {1}, {2}, {3}, and {4} strings that match the snapshots to include in the replication. Separate entries by pressing <kbd>Enter</kbd>. The number of snapshots matching the patterns display. |
{{< /truetable >}}

**Source Location: On a Different System**

{{< truetable >}}
| Name | Description |
|------|------|
| **SSH Connections** | Select an existing SSH connection to a remote system or choose **Create New** to create a new SSH connection. |
| **Source** | Define the path to a system location that has snapshots to replicate. Click the folder to see all locations on the source system or click in the field to manually type a location (Example: *pool1/dataset1*). Multiple source locations can be selected or manually defined with a comma (,) separator.  Selecting a location displays the number of existing snapshots that can be replicated. Selecting a location that has no snapshots configures the replication task to take a manual snapshot of that location and replicate it to the destination. |
| **Recursive** | Select to also replicate all snapshots contained within the selected source dataset snapshots. Clear to only replicate the selected dataset snapshots. |
| **Naming Schema** | Pattern of naming custom snapshots to be replicated. Enter the name and [strftime(3)](https://www.freebsd.org/cgi/man.cgi?query=strftime) {0}, {1}, {2}, {3}, and {4} strings that match the snapshots to include in the replication. Separate entries by pressing <kbd>Enter</kbd>. The number of snapshots matching the patterns are shown. |
| **SSH Transfer Security** | Data transfer security. The connection is authenticated with SSH. Data can be encrypted during transfer for security or left unencrypted to maximize transfer speed. Encryption is recommended, but can be disabled for increased speed on secure networks. |
{{< /truetable >}}

**Destination Location: On this System**

{{< truetable >}}
| Name | Description |
|------|------|
| **Destination** | Define the path to a system location that stores replicated snapshots. Click the folder to see all locations on the destination system or click in the field to manually type a location path (Example: *pool1/dataset1*). Selecting a location defines the full path to that location as the destination. Appending a name to the path creates a new zvol at that location. For example, selecting pool1/dataset1 stores snapshots in dataset1, but clicking the path and typing */zvol1* after dataset1 creates zvol1 for snapshot storage. |
| **Encryption** | Select to use encryption when replicating data. Additional encryption options appear. |
{{< /truetable >}}

**Destination Location: On a Different System**

{{< truetable >}}
| Name | Description |
|------|------|
| **SSH Connections** | Select a saved remote system SSH connection or choose **Create New** to create a new SSH connection. |
| **Destination** | Define the path to a system location that stores replicated snapshots. Click the folder to see all locations on the destination system or click in the field to manually type a location path (Example: *pool1/dataset1*). Selecting a location defines the full path to that location as the destination. Appending a name to the path creates a new zvol at that location. For example, selecting pool1/dataset1 stores snapshots in dataset1, but clicking the path and typing */zvol1* after dataset1 creates zvol1 for snapshot storage. |
| **Encryption** | Select to use encryption when replicating data. Additional encryption options appear. |
{{< /truetable >}}

### When

{{< truetable >}}
| Name | Description |
|------|------|
| **Replication Schedule** | Text |
| **Destination Snapshot Lifetime** | When replicated snapshots are deleted from the destination system. **Same as Source** uses the configured snapshot lifetime value from the source dataset periodic snapshot task. **Never Delete** never deletes snapshots from the destination system. **Custom** sets a how long a snapshot remains on the destination system. Enter a number and choose a measure of time from the dropdown list. |
| **Schedule** | Select specific times to snapshot what you specified in **Source Datasets** and replicate the snapshots to the location in **Destination Dataset**. Select a preset schedule or choose **Custom** to use the advanced scheduler. |
| **Text** | Text |
{{< /truetable >}}
