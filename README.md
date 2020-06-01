# ansible-freeton

Roles of Ansible for install and monitor FreeTon node.

## Roles:

- **common** - preparing system and install dependencies
- **freeton** - build and setup FreeTon node
- **netdata** - real-time monitoring
- **prometheus-node-exporter** - exporter for hardware and OS metrics exposed, also this gives opportunity get _balance_ and _diff_ in freeton network

## Functional

- Freeton Install

  - Creating user and group
  - Cronjob for validator script
  - All logs in one folder /var/log/...
  - Systemd for control status of node and restart in fail case
  - Logrotate for archive logs

- Node Monitoring
  - Install netdata for realtime status <host>/netdata
  - install prometheus-node-exporter for collect metrics
    - collecting data about node status(node diff, wallet balance,)
- Install nginx for close entry poins of monitoring systems
- Install and sync ntp server for avoid time shift

* System upgrade

## Installation

- Pull repository
- Add your host to freeton file
- Change role for installation (common should be always)
- Run ansible: `ansible-playbook freeton.yaml -i freeton --ask-sudo-pass`
- Ansible Build and setup node and save seed phrase `{{ install_path }}/ton-keys/seed_phrase.secret`
- Deploy wallet [instruction](https://docs.ton.dev/86757ecb2/v/0/p/94921e-multisignature-wallet-management-in-tonos-cli)

## Example Dashboard based on prometheus-node-exporter

![Alt text](FreeTon.png?raw=true "Title")

## todo:

- Improve describe of the repository
- Create rules for Alertmanager (Prometheus)
- Grafana template
- Install and configure Loki for log monitoring and alerting
