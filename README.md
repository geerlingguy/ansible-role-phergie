# Ansible Role: Phergie PHP IRC Bot

Installs Phergie, a PHP IRC bot on RHEL/CentOS and Debian/Ubuntu Linux systems.

To use Phergie, you can run `php phergie.php` from the directory in which Phergie is installed (set this with the `phergie_install_path` variable). You might want to run phergie in the background, and log output so you can check for any problems and store chat history with a command like:

    $ nohup php /path/to/phergie.php > /path/to/log 2>&1&

## Requirements

PHP should be installed on your system if you want to run Phergie. At least `php`, `php-pdo` and `php-sqlite`. Git is also required, as listed in the dependencies below.

## Role Variables

Available variables are listed below, along with default values (see `vars/main.yml`):

    phergie_install_path: /home/geerlingguy/phergie
    phergie_user: geerlingguy

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

  - geerlingguy.git (Installs Git).

## Example Playbook

    - hosts: servers
      vars_files:
        - vars/main.yml
      roles:
        - { role: geerlingguy.phergie }

*Inside `vars/main.yml`*:

    TODO

## License

MIT / BSD

## Author Information

This role was created in 2014 by Jeff Geerling (@geerlingguy), author of Ansible for DevOps. You can find out more about the book at http://ansiblefordevops.com/, and learn about the author at http://jeffgeerling.com/.
