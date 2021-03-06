---
layout: "yandex"
page_title: "Yandex: yandex_mdb_mysql_cluster"
sidebar_current: "docs-yandex-datasource-mdb-mysql-cluster"
description: |-
  Get information about a Yandex Managed MySQL cluster.
---

# yandex\_mdb\_mysql\_cluster

Get information about a Yandex Managed MySQL cluster. For more information, see
[the official documentation](https://cloud.yandex.com/docs/managed-mysql/).

## Example Usage

```hcl
data "yandex_mdb_mysql_cluster" "foo" {
  name = "test"
}

output "network_id" {
  value = "${data.yandex_mdb_mysql_cluster.foo.network_id}"
}
```

## Argument Reference

The following arguments are supported:

* `cluster_id` - (Optional) The ID of the MySQL cluster.

* `name` - (Optional) The name of the MySQL cluster.

~> **NOTE:** Either `cluster_id` or `name` should be specified.

* `folder_id` - (Optional) The ID of the folder that the resource belongs to. If it is not provided, the default provider folder is used.

## Attributes Reference

In addition to the arguments listed above, the following computed attributes are
exported:

* `network_id` - ID of the network, to which the MySQL cluster belongs.
* `created_at` - Creation timestamp of the key.
* `description` - Description of the MySQL cluster.
* `labels` - A set of key/value label pairs to assign to the MySQL cluster.
* `environment` - Deployment environment of the MySQL cluster.
* `version` - Version of the MySQL cluster.
* `health` - Aggregated health of the cluster.
* `status` - Status of the cluster.
* `resources` - Resources allocated to hosts of the MySQL cluster. The structure is documented below.
* `user` - A user of the MySQL cluster. The structure is documented below.
* `database` - A database of the MySQL cluster. The structure is documented below.
* `host` - A host of the MySQL cluster. The structure is documented below.

The `resources` block supports:

* `resources_preset_id` - The ID of the preset for computational resources available to a MySQL host (CPU, memory etc.).
  For more information, see [the official documentation](https://cloud.yandex.com/docs/managed-mysql/concepts/instance-types).
* `disk_size` - Volume of the storage available to a MySQL host, in gigabytes.
* `disk_type_id` - Type of the storage for MySQL hosts.

The `backup_window_start` block supports:

* `hours` - The hour at which backup will be started.
* `minutes` - The minute at which backup will be started.

The `access` block supports:

* `data_lens` - Allow access for Web SQL.

The `user` block supports:

* `name` - The name of the user.
* `password` - The password of the user.
* `permission` - Set of permissions granted to the user. The structure is documented below.

The `permission` block supports:

* `database_name` - The name of the database that the permission grants access to.
* `roles` - List user's roles in the database.
            Allowed roles: `ALL`,`ALTER`,`ALTER_ROUTINE`,`CREATE`,`CREATE_ROUTINE`,`CREATE_TEMPORARY_TABLES`,
            `CREATE_VIEW`,`DELETE`,`DROP`,`EVENT`,`EXECUTE`,`INDEX`,`INSERT`,`LOCK_TABLES`,`SELECT`,`SHOW_VIEW`,`TRIGGER`,`UPDATE`.

The `database` block supports:

* `name` - The name of the database.

The `host` block supports:

* `fqdn` - The fully qualified domain name of the host.
* `zone` - The availability zone where the MySQL host will be created.
* `subnet_id` - The ID of the subnet, to which the host belongs. The subnet must be a part of the network to which the cluster belongs.
* `assign_public_ip` - Sets whether the host should get a public IP address on creation.