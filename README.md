Ansible Role: Kubernetes Kube-Prometheus
=========

Installs the [kube-prometheus](https://github.com/prometheus-operator/kube-prometheus) project on a Kubernetes cluster.

Requirements
------------

Fully functional existing K8s cluster running K8s 1.22+. Older versions may work, but are untested.

Role Variables
--------------

The GoLang install version:. Requires golang 1.17.13 or later.

    go_version: 1.20.1

The kube-promethus role defines the following variables:

    # Directory to install kube-prometheus. Default is /opt/kube-prometheus
    prometheus_bin: "/opt/kube-prometheus"

    # Configure nginx ingress controller
    config_ingress: "yes"

    # Release of kube-prometheus to install
    release_tag: v0.12.0

    # Release of jb to install
    jb_release: release-0.7

    # Kubernetes namespace to use for installation of kube-prometheus
    kube_namespace: monitoring


Dependencies
------------

This playbook depends on the `ansible-role-golang-install` role and that an existing Kubernetes cluster is available.

Example Playbook
----------------

    # ===========================================================================
    # Install Kube-Prometheus
    # ===========================================================================
    - name: Install the Kube-Prometheus project
    hosts: k8s_master
    gather_facts: true
    become: false
    tags: play_prometheus

    roles:
        - { role: ansible-role-golang-install, go_version: 1.20.1 }
        - { role: ansible-role-kubernetes-kube-prometheus,
            storage_class: "vmw-block-sc"
        }

License
-------

MIT

Author Information
------------------

Aaron Patten
aaronpatten@gmail.com
