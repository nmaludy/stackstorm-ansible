# Changelog

## v0.5.2

* Added pywinrm to requirements so connection to windows hosts is possible.
  Contributed by Nick Maludy (Encore Technologies)

## v0.5.0

* Added ability to use yaml structures to pass arbitrarily complex values through extra_vars. key=value and @file syntax is still supported. Example usage:
```yaml
sample_task:
  action: ansible.playbook
  input:
    playbook: playbook.yml
    extra_vars:
      - key1=value1
      -
        key2: value2
        key3: [ value3a, value3b ]
        key4:
          - value4a
          - { value4bkey: value4bvalue }
        key5:
          key6: value6
          key7: value7
      - @path/to/file.yml
        ...
```

## v0.4

* Breaking Change: Added ability to pass in multiple extra_vars. The extra_vars parameter is now a list. Example usage:
```yaml
sample_task:
  action: ansible.playbook
  input:
    playbook: playbook.yml
    extra_vars: 
      - "@path/to/file.yml"
      - "@path/to/file.json"
      - key1=value1
      - key2={{ _.value2 }}
        ...
```

## v0.3

* Removed immutable flag for `sudo:` parameters for all actions. Default is `true`, which means that ansible commands are run with sudo (as root). Good thing is you can change it to `false` when required.

## v0.2

* Breaking Change: Replaced all dashes in parameter names with underscores (adhere to the spec of Jinja/Python variables)

## v0.1.1

* Prepend sandboxed path with ansible binaries to PATH env variable, allowing ansible binary discovery to follow PATH order

## v0.1.0

* Initial release with actions included:
 * `ansible.playbook`
 * `ansible.command`
 * `ansible.command_local`
 * `ansible.galaxy.install`
 * `ansible.galaxy.list`
 * `ansible.galaxy.remove`
 * `ansible.vault.encrypt`
 * `ansible.vault.decrypt`
