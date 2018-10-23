# DEPRECATED - Ansible Role: Phergie PHP IRC Bot

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-phergie.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-phergie)

> **DEPRECATED**: This role has been deprecated, as geerlingguy no longer uses Phergie and will not continue maintaining the role.

Installs Phergie, a PHP IRC bot on RHEL/CentOS and Debian/Ubuntu Linux systems.

To use Phergie, you can run `php phergie.php` from the directory in which Phergie is installed (set this with the `phergie_install_path` variable). You might want to run phergie in the background, and log output so you can check for any problems and store chat history with a command like:

    $ nohup php /path/to/phergie.php > /path/to/log 2>&1&

## Requirements

  - Git (recommended role: `geerlingguy.git`).
  - PHP (recommended role: `geerlingguy.php`) - `php`, `php-pdo`, and `php-sqlite` are recommended.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    phergie_install_path: "/home/{{ ansible_ssh_user }}/phergie"
    phergie_user: "{{ ansible_ssh_user }}"

The location where Phergie will be installed, and the user with which Phergie will be installed and most likely run.

    phergie_timezone: America/Chicago

The timezone Phergie will use when performing date-based actions.

    phergie_connections:
      - {
        host: 'irc.freenode.net',
        port: '6667',
        username: 'PhergieExample',
        realname: 'Phergie Example Bot',
        nick: 'PhergieExample'
      }

A list of connection objects; Phergie can connect to multiple IRC hosts, but typically one connection will suffice.

    phergie_autojoin_channels:
      - '#example'

A list of channels which Phergie will join after successfully connecting to the IRC server.

    phergie_command_prefix: ''

If you would like Phergie to only respond to commands with a prefix (like `!karma [keyword]` instead of `karma [keyword]`), set a prefix here.

    phergie_ui_enabled: 'true'

Whether to output Phergie bot events in the console when phergie is running (useful for debugging or checking on Bot activity in logs).

    phergie_plugins:
      - AltNick
      - AutoJoin
      - Beer
      - Help
      - Karma
      - Lart
      - Php
      - Ping
      - PingPong
      - Pong
      - Prioritize
      - Quit
      - Remind
      - Serve

A list of Phergie plugins to load. See the complete list here: https://github.com/phergie/phergie/tree/master/Phergie/Plugin.

    phergie_altnicks: []

A list of alternative nicks Phergie will use if the primary nick is taken (requires `AltNick` in `phergie_plugins`).

    phergie_wunderground_api_key: ''

The Weather Underground API key to use (requires `Wunderground` in `phergie_plugins`).

    phergie_karma_db_location: ''

A path to an SQLite database which Phergie will use if `Karma` is in `phergie_plugins`. It's useful to use a db outside of the phergie installation folder so the database won't be wiped out if you update phergie via `git pull`.

## Dependencies

  - `geerlingguy.git`

## Example Playbook

    - hosts: ircbot
      vars_files:
        - vars/main.yml
      roles:
        - geerlingguy.phergie

*Inside `vars/main.yml`*:

    phergie_connections:
      - {
        host: 'irc.freenode.net',
        port: '6667',
        username: 'PhergieExample',
        realname: 'Phergie Example Bot',
        nick: 'PhergieExample'
      }

## License

MIT / BSD

## Author Information

This role was created in 2014 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
