# Role Name

Loki role for Ubuntu

## Requirements

## Role Variables

    loki_version: 2.7.1

    loki_additional_pkg:
      - unzip

    loki_temp_dir: /home/vagrant/lokiDir
    loki_etc_dir: /etc/loki

    loki_bin:
      url: "https://github.com/grafana/loki/releases/download/v{{ loki_version}}/loki-linux-amd64.zip"
      file: loki-linux-amd64
      dir: /usr/local/bin

    loki_config:
      url: "https://raw.githubusercontent.com/grafana/loki/v{{ loki_version}}/cmd/loki/loki-local-config.yaml"
      file: loki-local-config.yaml

    loki_group: loki
    loki_user:
      name: loki
      shell: /bin/false

    loki_service:
      name: loki.service
      template_path: templates/loki.service.j2
      enabled: true
      daemon_reload: true

## Dependencies

## Example Playbook

    - name: Setup Loki
      hosts: loki

      roles:
        - loki

## License

BSD

## Author Information

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
