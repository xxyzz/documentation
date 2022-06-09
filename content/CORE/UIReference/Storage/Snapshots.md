---
title: "Snapshots"
weight: 20
---

{{< toc >}}

{{< include file="/_includes/SnapshotsIntroSnippet.md" type="page" >}}

Taking snapshots requires the system have all [pools]({{< relref "/CORE/CORETutorials/Storage/Pools/_index.md" >}}), [datasets]({{< relref "/CORE/CORETutorials/Storage/Pools/Datasets.md" >}}), and [zvols]({{< relref "/CORE/CORETutorials/Storage/Pools/Zvols.md" >}}) already configured.

## Creating a Single Snapshot

{{< hint ok >}}
Consider making a [Periodic Snapshot Task]({{< relref "CreatingPeriodicSnapshotTasks.md" >}}) to save time and create regular, fresh snapshots.
{{< /hint >}}

To quickly snapshot existing storage, go to **Storage > Snapshots** and click **ADD**.

![StorageSnapshotsAdd](/images/CORE/12.0/StorageSnapshotsAdd.png "Create a New Snapshot")

Use the **Dataset** drop-down list to select an existing ZFS pool, dataset, or zvol to snapshot.

The TrueNAS software displays a suggested name that you can override with any custom string.
To include the snapshot in [local]({{< relref "LocalReplication.md" >}}) or [remote]({{< relref "RemoteReplication.md" >}}) replication tasks  choose a proper naming schema. The **Naming Schema** drop-down list populates with schemas already created from periodic snapshot tasks.

To include child datasets with the snapshot, set **Recursive**.

## Managing Snapshots

Go to **Storage > Snapshots** to manage created snapshots.

![StorageSnapshots](/images/CORE/12.0/StorageSnapshots.png "List of Created Snapshots")

Each entry in the list includes the dataset and snapshot names.
Click <i class="material-icons" aria-hidden="true" title="Expand">chevron_right</i> to view options for a snapshot:

{{< tabs "Snapshot Options" >}}
{{< tab "DATE CREATED" >}}
The exact time and date of the snapshot creation.
{{< /tab >}}
{{< tab "USED" >}}
The amount of space consumed by this dataset and all of its descendants.
This value, checked against the dataset quota and reservation, shows the space used but does not include the dataset reservation. It takes into account the reservations of any descendant datasets.
The amount of space that a dataset consumes from its parent, and the amount of space freed if this dataset is recursively deleted, is the greater of its space used and its reservation.

At creation, a snapshot shares space between the snapshot, file system, and even with previous snapshots.
File system changes reduce the shared space and count toward a snapshot's used space.
Deleting a snapshot often increases the space that is unique and used in other snapshots.

Another method to view the space used by an individual snapshot is to go to the **Shell** and enter `zfs list -t snapshot`.

The space used, available, or referenced does not account for pending changes.
Pending changes generally update within a few seconds, but larger disk changes slow usage updates.
{{< /tab >}}
{{< tab "REFERENCED" >}}
The amount of data accessible by this dataset.
This could be shared with other datasets in the pool.
New snapshots or clones reference the same amount of space as the file system or snapshot it was created from, as the contents are identical.
{{< /tab >}}
{{< tab "DELETE" >}}

{{< include file="/_includes/DeletingSnapshots.md" type="page" >}}

{{< /tab >}}
{{< tab "CLONE TO NEW DATASET" >}}
Creates a new snapshot *clone* (dataset) from the snapshot contents.
{{< expand "What is a clone?" "v" >}}
A **clone** is a writable copy of the snapshot.
Because a clone is actually a mountable dataset, it appears in the **Pools** screen rather than the **Snapshots** screen.
Creating a new snapshot adds **-clone** to the name by default.
{{< /expand >}}
A dialog prompts for the new dataset name.
The suggested name derives from the snapshot name.
{{< /tab >}}
{{< tab "ROLLBACK" >}}
Revert the **Dataset** back to the point in time saved by the snapshot.

{{< hint warning >}}
Rollback is a dangerous operation that causes any configured replication tasks to fail.
Replications use the existing snapshot when doing an incremental backup, and rolling back can put the snapshots 'out of order'.
To restore the data within a snapshot, the recommended steps are:

1.  Clone the desired snapshot.
2.  Share the clone with the share type or service running on the TrueNAS system.
3.  Allow users to recover their needed data.
4.  Delete the clone from **Storage > Pools**.

This approach does not destroy any on-disk data and has no impact on replication.
{{< /hint >}}

TrueNAS asks for confirmation before rolling back to the chosen snapshot state.
Clicking **Yes** reverts all dataset files to the state they were in at the time of snapshot creation.
{{< /tab >}}
{{< /tabs >}}

### Bulk Operations

{{< include file="/_includes/SnapshotsBulkOperations.md" type="page" >}}

## Browsing a Snapshot Collection

{{< include file="/_includes/BrowsingSnapshotCollections1.md" type="page" >}}

A user with permission to access the hidden file can view and explore all snapshots for a dataset from the **Shell** or the **Sharing** screen using services like **SMB**, **NFS**, and **SFTP**.

{{< include file="/_includes/BrowsingSnapshotCollections2.md" type="page" >}}