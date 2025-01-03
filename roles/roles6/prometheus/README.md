# Role Name

Prometheus role for Ubuntu

## Requirements

## Role Variables

    prometheus_version: 2.41.0

    prometheus_url: "https://github.com/prometheus/prometheus/releases/download/v{{ prometheus_version }}/prometheus-{{ prometheus_version }}.linux-amd64.tar.gz"
    prometheus_pkg_path: "/home/{{ ansible_user_id }}/"
    prometheus_pkg_path_with_pkg_name: "{{ prometheus_pkg_path }}/prometheus-{{ prometheus_version }}.linux-amd64"

    prometheus_config_dir: /etc/prometheus
    prometheus_lib_dir: /var/lib/prometheus
    prometheus_bin_dir: /usr/local/bin/

    prometheus_dirs:
      - "{{ prometheus_config_dir }}"
      - "{{ prometheus_lib_dir }}"

    prometheus_files_to_move:
      - { src: "{{ prometheus_pkg_path_with_pkg_name }}/prometheus", dest: "{{ prometheus_bin_dir }}" }
      - { src: "{{ prometheus_pkg_path_with_pkg_name }}/promtool", dest: "{{ prometheus_bin_dir }}"}
      - { src: "{{ prometheus_pkg_path_with_pkg_name }}/consoles/", dest: "{{ prometheus_config_dir }}/" }
      - { src: "{{ prometheus_pkg_path_with_pkg_name }}/console_libraries/", dest: "{{ prometheus_config_dir }}/" }

    prometheus_config:
      template: templates/prometheus.yml.j2
      path: "{{ prometheus_config_dir }}/prometheus.yml"

    prometheus_group: prometheus
    prometheus_user:
      name: prometheus
      shell: /sbin/nologin

    prometheus_systemd:
      template: templates/prometheus.service.j2
      name: prometheus.service
      path: /etc/systemd/system/prometheus.service
      enabled: yes
      listen_address: 0.0.0.0:9090

    prometheus_static_configs:
      targets: ["localhost:9090"]

    # prometheus_scrape_configs: |2
    #     - job_name: "application"
    #       static_configs:
    #         - targets: ["192.168.56.201:8080"]

## Dependencies

## Example Playbook

    - name: Setup Prometheus
      hosts: prometheus

      roles:
        - prometheus

## License

BSD

## Author Information

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
