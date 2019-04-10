Role Name
=========

Install MariaDB Server Master and Slave on Redhat/CentOS.

Requirements
------------

No special requirements; note that this role requires root access, so either run it in a playbook with a global `become: yes`, or invoke the role in your playbook like:

    - hosts: database
      roles:
        - role: diegorodrigues87.mariadb
          become: yes

Role Variables
--------------

	mariadb_databases: []
	mariadb_users: []
	mariadb_user_name: root
	mariadb_root_username: root
	mariadb_user_home: /root
	mariadb_root_password: ''

	mariadb_mirror: yum.mariadb.org
	mariadb_version: '10.3'

	mariadb_configure_swappiness: true
	mariadb_swappiness: 0

	mariadb_character_set_server: utf8
	mariadb_collation_server: utf8_general_ci

# Network configuration (network.cnf)

	mariadb_service: mariadb
	mariadb_bind_address: '127.0.0.1'
	mariadb_port: 3306

# Service configuration

	mariadb_max_connect_errors: 10
	mariadb_max_connections: 505
	mariadb_max_user_connections: 500
	mariadb_skip_name_resolve: 1
	mariadb_wait_timeout: 60

# Logging

	mariadb_log_warnings: '1'
	mariadb_slow_query_log: '0'
	mariadb_long_query_time: '10'
	mariadb_sysdate_is_now: 1
	mariadb_logs_days: 10
	mariadb_expire_logs_days: 10
	mariadb_sync_binlog: 1

# Query cache

	mariadb_query_cache_size: 0
	mariadb_query_cache_type: 0

# Replication settings (replication is only enabled if master/user have values).
	mariadb_server_id: "1"
	mariadb_max_binlog_size: "100M"
	mariadb_replication_role: ''
	mariadb_replication_master: ''
	mariadb_replication_user: []

# System resources

	mariadb_join_buffer_size: '128k'
	mariadb_max_allowed_packet: '16M'
	mariadb_max_heap_table_size: '16M'
	mariadb_open_files_limit: '65353'
	mariadb_read_buffer_size: '128k'
	mariadb_read_rnd_buffer_size: '256k'
	mariadb_sort_buffer_size: '2M'
	mariadb_table_definition_cache: '1400'
	mariadb_table_open_cache: '2000'
	mariadb_table_open_cache_instances: '8'
	mariadb_thread_cache_size: 50
	mariadb_tmp_table_size: '16M'

# InnoDB

	mariadb_innodb_buffer_pool_instances: 8
	mariadb_innodb_buffer_pool_load_at_startup: 'ON'
	mariadb_innodb_buffer_pool_size: '384M'
	mariadb_innodb_file_per_table: 'ON'
	mariadb_innodb_flush_log_at_trx_commit: 1
	mariadb_innodb_flush_method: 'O_DIRECT'
	mariadb_innodb_log_buffer_size: '16M'
	mariadb_innodb_log_file_size: '48M'
	mariadb_innodb_log_files_in_group: 2
	mariadb_innodb_strict_mode: 'ON'

# Custom settings

	mariadb_custom_cnf: {}


Dependencies
------------

None.

Example Playbook
----------------

    - hosts: db-servers
      become: yes
      vars_files:
        - vars/main.yml
      roles:
        - { role: diegorodrigues87.mariadb }

*Inside `vars/main.yml`*:

    mariadb_root_password: super-secure-password
    mysql_databases:
      - name: example_db
        encoding: utf8
        collation: utf8_general_ci
    mysql_users:
      - name: example_user
        host: "%"
        password: similarly-secure-password
        priv: "example_db.*:ALL"


License
-------

BSD

Author Information
------------------

Roles is created by Diego Rodrigues.
