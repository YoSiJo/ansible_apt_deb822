# apt_deb822

Add or remove an APT repository in Ubuntu and [Debian](https://www.debian.org/),
as a sources file in [DEB822](https://manpages.debian.org/bullseye/dpkg-dev/deb822.5.en.html) format.

The orignial repository is hostet on [codeberg.org](https://codeberg.org/) and not an github. Only Ansible Galaxy don't support codeberg.

## Requirements

Nothing.
The role is intended as an alternative to the
[ansible.builtin.apt_repository](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/apt_repository_module.html) module.
In the long run, it should take over as much as possible from this and extend the capabilities with the deb822 possibilities.

## Role Variables

| Variables                                 | Choices/Defaults                  | Comments                                                                |
|---                                        |---                                |---                                                                      |
| apt_deb822_filename (string)              |                                   | Define the filename . The suffix `.sources` is appended automatically.  |
| apt_deb822_mode (raw)                     | Default: `0644`                   | The permissions the resulting file.                                     |
| apt_deb822_state (string)                 | Choices: `absent` or (`present`)  | A source string state.                                                  |
| apt_deb822_options (dictionary/required\]  |                                   | Defines the repository settings.                                        |

## apt_deb822_options

| Options           | Type    | Comments                                |
|---                |---      |---                                      |
| Types             | list    | `deb` and/or `deb-src`                  |
| URIs              | list    | The repository urls                     |
| Suites            | list    | `stable`, `bullseye`, …                 |
| Components        | list    | `main`, `contrib`, `non-free`, …        |
| Architectures     | list    | `amd64`, `armel`, …                     |
| Languages         | list    | Defining languages information          |
| Targets           | list    | Defining Acquire::IndexTargets          |
| PDiffs            | boolean | Enable or disable PDiffs                |
| By-Hash           | boolean | Enable or disable By-Hash               |
| Allow-Insecure    | boolean | Enable or disable parts of apt-secure   |
| Trusted           | boolean | Enable or disable trusted state         |
| Signed-By         | string  | Defining the path to gpg file           |
| Check-Valid-Until | boolean | Enable or disable Valid-Until Check     |
| Valid-Until-Min   | intager | Defined the Min-ValidTime in second     |
| Check-Date        | boolean | Check system time                       |
| Date-Max-Future   | intager | Defined the Max-FutureTime in second    |
| InRelease-Path    | string  | Set the relativ path to InRelease-file  |

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: servers
  tasks:
    - name: Include apt_deb822 role
      ansible.builtin.include_role:
        name: apt_deb822
      vars:
        apt_deb822_options:
          Description: Debian default repository
          Types:
            - deb
          URIs:
            - http://ftp.debian.org/debian
          Suites:
            - stable
            - stable-updates
          Components:
            - main
            - contrib
          PDiffs: true
```

## License

AGPL v3 or later
