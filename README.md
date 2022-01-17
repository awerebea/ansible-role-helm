# Ansible Role: Helm, the Kubernetes package manager

An Ansible Role that installs [Helm](https://helm.sh/) on Linux.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

If no version is specified, the latest version for the `linux-amd64` platform will be installed. Available [Helm releases](https://github.com/helm/helm/releases/).

    helm_version: 3.2.1
    helm_platform: linux
    helm_arch: amd64

If no custom path to the main Helm repo is specified, URL of the official Helm repo is used, `https://get.helm.sh`

    helm_repo_path: https://get.helm.sh

If no directory is specified for the `helm` binary placing, `/usr/local/bin` is used.

    helm_bin_dir: $HOME/.local/bin

If the directory for downloading and extracting the release archive is not specified, `/tmp` is used.

    helm_download_dir: $HOME/Downloads

List of user environment files to add conditional export to the system PATH of a directory with the app binary.
<br />Only existing files with write access for the current ansible_user will be processed.
<br />If not specified, empty list is used.

    helm_env_files_to_modify:
      - $HOME/.profile
      - $HOME/.bashrc
      - $HOME/.zshenv

**NOTE:** By default, the base tasks of a role are skipped if the application is already installed in the desired
<br />bin directory and no version upgrade is required.
<br />&nbsp;&nbsp;&nbsp;&nbsp;If you want to add a conditional export to the system `PATH` of a directory with the app binary, after the Playbook
<br />has already been run once, you can force the launch base role tasks by defining the `update_apps` variable
<br />and adding `helm` to the list. For example:
``` bash
$ ansible-playbook main.yaml -e "update_apps=[helm]"
```
This approach is also used to force an update to the latest available release.

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  roles:
    - role: ansible-role-helm
      helm_bin_dir: $HOME/.local/bin
```

## License

MIT
