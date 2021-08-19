#### View the backup subdirectories

<span class="version-tag">New in v21.1:</span> `BACKUP ... INTO` adds a backup to a collection within the backup destination. The path to the backup is created using a date-based naming scheme. To view the backup paths in a given destination, use [`SHOW BACKUPS`](../{{site.versions["stable"]}}/restore.html#view-the-backup-subdirectories):

{% include_cached copy-clipboard.html %}
~~~ sql
> SHOW BACKUPS IN 's3://{BUCKET NAME}?AWS_ACCESS_KEY_ID={KEY ID}&AWS_SECRET_ACCESS_KEY={SECRET ACCESS KEY}';
~~~

~~~
        path
------------------------
2021/03/23-213101.37
2021/03/24-172553.85
2021/03/24-210532.53
(3 rows)
~~~

When you restore a backup, add the backup's subdirectory path (e.g., `2021/03/23-213101.37`) to the storage URL.

#### Restore a cluster

To restore a full cluster:

{% include_cached copy-clipboard.html %}
~~~ sql
> RESTORE FROM 's3://{BUCKET NAME}/{path/to/backup/subdirectory}?AWS_ACCESS_KEY_ID={KEY ID}&AWS_SECRET_ACCESS_KEY={SECRET ACCESS KEY}';
~~~

To view the available subdirectories, use [`SHOW BACKUPS`](../{{site.versions["stable"]}}/restore.html#view-the-backup-subdirectories).

#### Restore a database

To restore a database:

{% include_cached copy-clipboard.html %}
~~~ sql
> RESTORE DATABASE bank FROM 's3://{BUCKET NAME}/{path/to/backup/subdirectory}?AWS_ACCESS_KEY_ID={KEY ID}&AWS_SECRET_ACCESS_KEY={SECRET ACCESS KEY}';
~~~

To view the available subdirectories, use [`SHOW BACKUPS`](../{{site.versions["stable"]}}/restore.html#view-the-backup-subdirectories).

{{site.data.alerts.callout_info}}
`RESTORE DATABASE` can only be used if the entire database was backed up.
{{site.data.alerts.end}}

#### Restore a table

To restore a single table:

{% include_cached copy-clipboard.html %}
~~~ sql
> RESTORE TABLE bank.customers FROM 's3://{BUCKET NAME}/{path/to/backup/subdirectory}?AWS_ACCESS_KEY_ID={KEY ID}&AWS_SECRET_ACCESS_KEY={SECRET ACCESS KEY}';
~~~

To restore multiple tables:

{% include_cached copy-clipboard.html %}
~~~ sql
> RESTORE TABLE bank.customers, bank.accounts FROM 's3://{BUCKET NAME}/{path/to/backup/subdirectory}?AWS_ACCESS_KEY_ID={KEY ID}&AWS_SECRET_ACCESS_KEY={SECRET ACCESS KEY}';
~~~

To view the available subdirectories, use [`SHOW BACKUPS`](../{{site.versions["stable"]}}/restore.html#view-the-backup-subdirectories).
