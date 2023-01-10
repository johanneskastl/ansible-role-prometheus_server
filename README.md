![Ansible Lint](https://github.com/johanneskastl/ansible-role-prometheus_server/workflows/Ansible%20Lint/badge.svg)

prometheus_server
=========

Install, configure and start the Prometheus server

Requirements
------------

None.

Role Variables
--------------

**Default values**
- `systemd_unit_name`: name of the systemd unit for the prometheus server, defaults to `prometheus.service`
- `scrape_interval`: global scrape interval, defaults to `15s`
- `evaluation_interval`: global evaluation interval, defaults to `15s`
- `scrape_timeout`: global scrape timeout, defaults to `10s`
- `prometheus_scrape_interval`: scrape interval for the prometheus job, defaults to `5s`
- `prometheus_scrape_timeout`: scrape timeout for the prometheus job, defaults to `5s`

**Handling the behaviour of the role**
- `scrape_local_node_exporter`: enable scraping the node-exporter metrics on the prometheus server itself (enabled by default)

**Settings for the node-exporter job**

Both of these are only set if defined by the user. Otherwise they will be omitted and the global defaults are used for the node-exporter job.

- `node_exporter_scrape_interval`: scrape interval for the node-exporter job
- `node_exporter_scrape_timeout`: scrape timeout for the node-exporter job

**Adding additional nodes**

- `additional_nodes`: list of IP addresses or hostnames of additional nodes, that should be added to the existing `node` job, aka scraping their node-exporter metrics on port 9100

Dependencies
------------

None

Example Playbook for only setting up the server itself without any other nodes
----------------

    - hosts: servers
      roles:
        - role: 'johanneskastl.prometheus_server'

Example Playbook with two additional nodes to be scraped
----------------

    - hosts: servers
      roles:
        - role: 'johanneskastl.prometheus_server'
          additional_nodes:
            - 192.168.1.100
            - 10.11.12.100

License
-------

BSD-3-Clause

Author Information
------------------

I am Johannes Kastl, reachable via kastl@b1-systems.de.
