## OVAL Discovery

* Many times only a targeted scan is required
* No obvious list of what scan targets are availble
* Extracts the common name of plugins from the system

```shell
$ mco oscap oval_checks
```

```shell
master
   OVAL Checks: ["partition_for_tmp => oval:ssg:def:272",
                 "partition_for_var => oval:ssg:def:151",
                 "partition_for_var_log => oval:ssg:def:334",
# Lots more...
                 "snmpd_not_default_password => oval:ssg:def:164"]

Finished processing 1 / 1 hosts in 204.91 ms
```

<!-- .element: class="fragment" -->
