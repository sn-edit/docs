# Commands

Below, you will find a list of commands currently supported by sn-edit and a brief explanation to each of them.
You will find out, how you can use them and what they do.

First things first, running sn-edit without parameters results in you seeing the list of available commands and then
a usage information on how to use commands.

Every command has a separate `--help` parameter. While using this with a command, you will get information about all the
available flags for the command. 

```
Usage:
  sn-edit [command]

Available Commands:
  download    Download one entry from servicenow
  help        Help about any command
  updateset   Manage update sets for the app
  upload      Upload one entry from servicenow
  version     Print the version number of sn-edit

Flags:
      --config string   config file (default is $HOME/.sn-edit.yaml)
  -h, --help            help for sn-edit

Use "sn-edit [command] --help" for more information about a command.

```

## List of Commands
Below you find a list of all the flags and explanation to their usage.

### download
With the download command you can download an entry from your Servicenow instance. While downloading, sn-edit will determine
the scope of the entry.

For this to work, you need to set up your tables and fields first in the `.sn-edit.yaml` file. 
See [tables configuration](configuration/README.md?id=app.tables) fore more details.  

For this command to work properly, you need to provide the flags `--sys_id` and `--table`.
Otherwise, sn-edit will not be able to properly determine the entry and download it.

```
Usage:
  sn-edit download [flags]

Flags:
  -h, --help            help for download
      --sys_id string   the sys_id of the entry which you would like to get
  -t, --table string    the table from where sn-edit should get the entry from

Global Flags:
      --config string   config file (default is $HOME/.sn-edit.yaml)

```

#### Example usages

```bash
sn-edit --table sys_script_include --sys_id f1b8d304db2010108a1758b3ca961967
```

### upload
With the upload command you can upload an entry to the instance. With this command you are able to upload your entries
to the instance. This command accepts multiple parameters.

The `--table`, `--sys_id` and `--fields` flags are all required to be provided. The flag `--update_set` is optional.
If you provide an `--update_set` flag, then sn-edit will use the sys_id provided (if found in the local db) to use
while updating the entry.

It is important, to first list the update sets on the instance using the `sn-edit updateset --list --scope global` command.
(Replace the scope with the one you want to use)

Using the list command is due to the fact, that sn-edit needs to have the update sets listed locally in the database to use them
in the cli app.

If you do not provide an `--update_set` flag, then sn-edit will fall back to the session default. If you want to change
the default update set, then use the `sn-edit updateset` command to update the default update set.
See [updateset](commands/README.md?id=updateset) command for more reference.

#### Example usages

Upload the fields script and name to the instance to the table sys_script_include
```bash
sn-edit upload --table sys_script_include --sys_id f1b8d304db2010108a1758b3cg96196x --fields script,name
```

Upload the fields script and name to the instance to the table sys_script_include with a custom update set.
(You can get the sys_id from the updateset --list command)
```bash
sn-edit upload --table sys_script_include --sys_id f1b8d304db2010108a1758b3cg96196x --fields script,name --update_set fgbjd304db2010108a1758b3cg96196x
```

```
Usage:
  sn-edit upload [flags]

Flags:
  -f, --fields string       provide one or more fields, comma separated (example: "name,script,active")
  -h, --help                help for upload
      --sys_id string       the sys_id of the entry which you would like to get
  -t, --table string        the table from where sn-edit should get the entry from
      --update_set string   the sys_id of an update set, you need to list the update sets before using this (example: "<sys_id>")

Global Flags:
      --config string   config file (default is $HOME/.sn-edit.yaml)

```

### updateset
With the updateset command you are able to manage update sets. I recommend always running list for every scope before setting anything.
The app needs to know about the update sets (name, sys_id) so it is able to change the current default update set.

This command allows you to set a default update set for a scope. Every scope can have 1..n update sets. Using the `--list` flag
without a `--scope` specified, defaults to global. You can provide a scope flag, if you do please provide a scope name.

There is also a `--set` flag, which requires that you provide an `--update_set` and a `--scope` (if not provided, defaults to global).
While you can provide a scope name for the `--scope` flag, the `--update_set` flag requires that you provide a sys_id,
this can be retrieved using the `--list` flag.

Do not use `--list` and `--set` at once, it can lead to unexpected results.

#### Example usages

List update sets for global scope.
```bash
sn-edit updateset --list
```

List update set for x_1122323_scope
```bash
sn-edit updateset --list --scope x_1122323_scope
```

Set update set with sys_id for the scope x_1122323_scope
```bash
sn-edit updateset --set --scope x_1122323_scope --update_set f1b8d304db2010108a1758b3cg96196x
```

Truncate update set data
```bash
sn-edit updateset --truncate
```

```
Usage:
  sn-edit updateset [flags]

Flags:
  -h, --help                help for updateset
      --list                use this to list update sets for the scope provided
      --scope string        the name of the scope (example: "global") (default "global")
      --set                 use this to set update sets for the scope provided
      --update_set string   the sys_id of the update_set (example: "<sys_id>") (default "global")

Global Flags:
      --config string   config file (default is $HOME/.sn-edit.yaml)

```

### version
Version just prints the current version of sn-edit. It does not accept any other parameters.

Example usage:
````bash
sn-edit --version
````