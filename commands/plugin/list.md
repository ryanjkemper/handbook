# wp plugin list

Gets a list of plugins.

Displays a list of the plugins installed on the site with activation status, whether or not there's an update available, etc.

Use `--status=dropin` to list installed dropins (e.g. `object-cache.php`).

### OPTIONS

[\--&lt;field&gt;=&lt;value&gt;]
: Filter results based on the value of a field.

[\--field=&lt;field&gt;]
: Prints the value of a single field for each plugin.

[\--fields=&lt;fields&gt;]
: Limit the output to specific object fields.

[\--format=&lt;format&gt;]
: Render output in a particular format.
\---
default: table
options:
  - table
  - csv
  - count
  - json
  - yaml
\---

[\--status=&lt;status&gt;]
: Filter the output by plugin status.
\---
options:
  - active
  - active-network
  - dropin
  - inactive
  - must-use
\---

[\--skip-update-check]
: If set, the plugin update check will be skipped.

### AVAILABLE FIELDS

These fields will be displayed by default for each plugin:

* name
* status
* update
* version

These fields are optionally available:

* update_version
* update_package
* update_id
* title
* description
* file

### EXAMPLES

    # List active plugins on the site.
    $ wp plugin list --status=active --format=json
    [{"name":"dynamic-hostname","status":"active","update":"none","version":"0.4.2"},{"name":"tinymce-templates","status":"active","update":"none","version":"4.4.3"},{"name":"wp-multibyte-patch","status":"active","update":"none","version":"2.4"},{"name":"wp-total-hacks","status":"active","update":"none","version":"2.0.1"}]

    # List plugins on each site in a network.
    $ wp site list --field=url | xargs -I % wp plugin list --url=%
    +---------+----------------+--------+---------+
    | name    | status         | update | version |
    +---------+----------------+--------+---------+
    | akismet | active-network | none   | 3.1.11  |
    | hello   | inactive       | none   | 1.6     |
    +---------+----------------+--------+---------+
    +---------+----------------+--------+---------+
    | name    | status         | update | version |
    +---------+----------------+--------+---------+
    | akismet | active-network | none   | 3.1.11  |
    | hello   | inactive       | none   | 1.6     |
    +---------+----------------+--------+---------+

### GLOBAL PARAMETERS

These [global parameters](https://make.wordpress.org/cli/handbook/config/) have the same behavior across all commands and affect how WP-CLI interacts with WordPress.

| **Argument**    | **Description**              |
|:----------------|:-----------------------------|
| `--path=<path>` | Path to the WordPress files. |
| `--url=<url>` | Pretend request came from given URL. In multisite, this argument is how the target site is specified. |
| `--ssh=[<scheme>:][<user>@]<host\|container>[:<port>][<path>]` | Perform operation against a remote server over SSH (or a container using scheme of "docker", "docker-compose", "docker-compose-run", "vagrant"). |
| `--http=<http>` | Perform operation against a remote WordPress installation over HTTP. |
| `--user=<id\|login\|email>` | Set the WordPress user. |
| `--skip-plugins[=<plugins>]` | Skip loading all plugins, or a comma-separated list of plugins. Note: mu-plugins are still loaded. |
| `--skip-themes[=<themes>]` | Skip loading all themes, or a comma-separated list of themes. |
| `--skip-packages` | Skip loading all installed packages. |
| `--require=<path>` | Load PHP file before running the command (may be used more than once). |
| `--exec=<php-code>` | Execute PHP code before running the command (may be used more than once). |
| `--context=<context>` | Load WordPress in a given context. |
| `--[no-]color` | Whether to colorize the output. |
| `--debug[=<group>]` | Show all PHP errors and add verbosity to WP-CLI output. Built-in groups include: bootstrap, commandfactory, and help. |
| `--prompt[=<assoc>]` | Prompt the user to enter values for all command arguments, or a subset specified as comma-separated values. |
| `--quiet` | Suppress informational messages. |
