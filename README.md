# Ansible Module Winetricks

The Winetricks module for Ansible is used to manage Windows libraries in Wine via the use of [Winericks](https://wiki.winehq.org/Winetricks).


## Installation

Installation is optional. The only requirement is that Wine is installed onto the managed system.

Copy over the library into the default directory for Ansible's library.

```
$ sudo cp -r -v ansible-module-winetricks/library/ /usr/share/ansible/
```

The "library" directory can be included in the top-level directory of a Playbook to be bundled with it. Note that this software is distributed under the strict GPLv3 license to ensure that it always stays free and open source.

Alternatively, a Playbook can be executed to use this Git repository as an additional module library path.

```
$ ansible-playbook --module-path=/path/to/ansible-module-winetricks site.yml
```


## Usage

Module arguments:

| Name | Required | Default | Description
| --- | --- | --- | --- |
| args | Yes | | The arguments to use with Winetricks. |
| binary | No | | Specify a different Winetricks binary to use. This is useful for when multiple versions of Winetricks are installed on a system. |


## Testing

A simple Playbook is provided to test that the `winetest` binary will return the version information. The results from the module will also be displayed.

```
$ ansible-playbook test.yml
PLAY [localhost] **************************************************************************

TASK [Gathering Facts] ********************************************************************
ok: [localhost]

TASK [Make sure that Winericks does not fail with any special checks first] ***************
ok: [localhost]

TASK [Test the "winetricks" Ansible module by verifying the Winetricks version] ***********
skipping: [localhost]

TASK [View the Winetricks module output] **************************************************
ok: [localhost] => {
    "winetricks_module_output": {
        "changed": false, 
        "cmd": [
            "/usr/bin/winetricks", 
            "--unattended", 
            "--version"
        ], 
        "failed": false, 
        "rc": 0, 
        "stderr": "", 
        "stderr_lines": [], 
        "stdout": "20180217 - sha256sum: 5ae9eb539ad58eb7437c00ef4bdaa0efd63e6be474c6c8957316f6a54f0911cd\n", 
        "stdout_lines": [
            "20180217 - sha256sum: 5ae9eb539ad58eb7437c00ef4bdaa0efd63e6be474c6c8957316f6a54f0911cd"
        ]
    }
}

PLAY RECAP ********************************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0
```


## License

GPLv3
