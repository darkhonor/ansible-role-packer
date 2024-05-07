# Ansible Role: Packer

Installs the Packer application and (if required) the modules and plugins
required to operate the application in an airgap environment.

## Requirements

None

## Role Variables

You can modify any of the following variables as you wish in the role's `defaults/main.yml`:

* `airgap`: Boolean if the target is in an airgap'd environment (Default: `false`)
* `hashicorp_rpm_repo_url`: Full URL to the Hashicorp RPM repository (Default: <https://rpm.releases.hashicorp.com/RHEL/$releasever/$basearch/stable>)
* `hashicorp_gpg_key_url`: Full URL to the Hashicorp RPM GPG Key (Default: <https://rpm.releases.hashicorp.com/gpg>)
* `trust_repository_certs`: Boolean if the source repository's certificate is trusted by the target (Default: `true`)
* `plugin_archive_url`: Full URL to an archive of the Packer Plugins (airgap only)
* `plugin_archive_path`: Path on the target to create and store the provider archive (airgap only; Default: `/opt/packer`)

The following role variables are *safe* defaults and should not need to be modified:

* `plugin_archive_owner`: File owner for the Provider archive (airgap only; Default: `root`)
* `plugin_archive_group`: Group owner for the provider files (airgap only; Default: `root`)
* `plugin_archive_mode`: Directory Mode for the provider files (airgap only; Default: `0755`)
* `plugin_archive_setype`: SELinux Type for provider files (airgap only; Default: `usr_t`)
* `plugin_archive_keep_newer`: Boolean if you want to preserve files locally that are newer than the files in the archive (airgap only; Default: `false`)

## Dependencies

None

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- name: Configure workstations
  become: true
  become_method: sudo
  gather_facts: true
  hosts: all
  roles:
    - role: packer
      airgap: true
      hashicorp_rpm_repo_url: "{{ repo_server }}/{{ hashicorp_repo_path }}"
      hashicorp_gpg_key_url: "{{ repo_server }}/{{ hashicorp_cert_path }}"
      trust_repository_certs: false
      plugin_archive_url: "{{ repo_server }}/{{ packer_plugin_archive }}"
      plugin_archive_path: /opt/packer
```


## License

MIT

## Author Information

Alex Ackerman, GitHub @darkhonor

