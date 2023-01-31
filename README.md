# Ansible Role: Dragonflydb

An Ansible Role that installs [Dragonflydb](https://dragonflydb.io/) on Linux (Debian/Ubuntu).

## Requirements

Only installs on Debian/Ubuntu.
Tested with Ubuntu 22.04 only.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    dragonflydb_version: 0.14.0

Install a specific version of Dragonflydb by setting it here. See [available Dragonfly versions](https://github.com/dragonflydb/dragonfly/releases) for a release that has a pre build .deb package. The 1st Dragonflydb version to provide a deb package was 0.14.0

    dragonfly_port: 6379
    dragonflydb_bind_interface: 127.0.0.1

The Dragonfly bindport and IP address. use localhost or 127.0.0.1 to only allow locahost connections, Public IP ADDRESS , to allow connections to that ip address (aka from outside too)

    dragonflydb_requirepass: ""

Password for AUTH authentication, default: ""

    dragonflydb_databases: 16

Maximum number of supported databases for select.

    dragonflydb_maxmemory: "0"

Limit on maximum-memory (in human-readble bytes) that is used by the database. 0 - means the program will automatically determine its maximum memory usage. default: 0

    dragonflydb_cache_mode: "false"

Dragonfly has a single unified adaptive caching algorithm that is very simple and memory efficient. You can enable caching mode by passing --cache_mode=true flag. Once this mode is on, Dragonfly will evict items least likely to be stumbled upon in the future but only when it is near maxmemory limit.

    dragonflydb_dbdir: /var/lib/dragonflydb

by default, dragonfly docker uses /data folder for snapshotting. the CLI uses: "" You can use -v docker option to map it to your host folder. This roles uses /var/lib/dragonflydb to be more analog to Redis.

    dragonflydb_dbfilename: dump

The filename to save/load the DB. default: "dump";

    dragonflydb_memcache_port.

To enable memcached compatible API on this port. Disabled (undefined) by default.
    dragonflydb_keys_output_limit: 8192

Maximum number of returned keys in keys command. Default is 8192. keys is a dangerous command. We truncate its result to avoid blowup in memory when fetching too many keys.

    dragonflydb_hz: 100

Key expiry evaluation frequency. Default is 100. Lower frequency uses less cpu when idle at the expense of slower eviction rate.

    dragonflydb_primary_port_http_enabled: "true"

If true allows accessing http console on main TCP port, default: true

    dragonflydb_admin_port

If set, would enable admin access to console on the assigned port. This supports both HTTP and RESP protocols. default disabled/undefined

    dragonflydb_admin_bind

If set, the admin consol TCP connection would be bind the given address. This supports both HTTP and RESP protocols. default any

## Dependencies

None.

## Example Playbook

    - hosts: servers_dragonflydb
      roles:
        - nicovs.dragonflydb

## License

MIT / BSD

## Author Information

This role was created in 2023 by [Nicovs](https://github.com/nicovs)
