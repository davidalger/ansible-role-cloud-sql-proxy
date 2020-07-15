# Ansible Role: Cloud SQL Proxy

[![Build Status](https://travis-ci.com/davidalger/ansible-role-cloud-sql-proxy.svg?branch=master)](https://travis-ci.com/davidalger/ansible-role-cloud-sql-proxy)


Installs [Cloud SQL Proxy](https://cloud.google.com/sql/docs/mysql/sql-proxy) on RHEL / CentOS 7 complete with unit scripts to keep `cloud-sql-proxy.service` running.

## Requirements

Just a [Cloud SQL](https://cloud.google.com/sql/docs/) instance for the proxy to connect to.

## Role Variables

    cloud_sql_proxy_connection_name: <project_id>:<region>:<instance_name>

The connection name for the Cloud SQL instance. See [this page](https://cloud.google.com/sql/docs/mysql/sql-proxy#tips) for more info. An appropriate value for this can be found on the Cloud SQL instance in the Cloud Console.

This string is also used by the proxy to determine the socket path. Example: When `tf-project-298d32a1:us-central1:tf-master-db1` is used as the connection name, the resulting unix socket will be `/var/run/cloud-sql-proxy/tf-project-298d32a1:us-central1:tf-master-db1`

    cloud_sql_proxy_tcp_port: <tcp_port>

Setting this will cause the Cloud SQL Proxy service to listen on a local TCP port rather than a unix socket.

## Dependencies

None.

## Example Playbook

    - hosts: web-servers
      vars:
        cloud_sql_proxy_connection_name: tf-project-298d32a1:us-central1:tf-master-db1
    
      roles:
        - { role: davidalger.cloud_sql_proxy, tags: database }

## License

This work is licensed under the MIT license. See LICENSE file for details.

## Author Information

This role was created in 2018 by [David Alger](http://davidalger.com/).
