# Configuration instructions

We are using yaml for configuration files. It is easy to read, configure and maintain.
It contains less bloat in comparison with a json file.

## sn-edit.sample.yaml
This is a sample file, please fill in your details to use it.

```yaml
app:
  core:
    db:
    initialised: false
    path: /path/to/a/db/file/sn-edit.db
    log_level: info
    rest:
      masked: false
      password: password
      url: https://dev11112.service-now.com
      user: username
      xor_key: maskingkey
    root_directory: /path/to/the/working/folder
    tables:
    - name: sys_script
    fields:
      - extension: txt
        field: sys_id
      - extension: js
        field: script
      - extension: txt
        field: sys_name
    - name: sys_script_include
    fields:
      - extension: txt
        field: sys_id
      - extension: js
        field: script
      - extension: txt
        field: sys_name
```

## Config parameters
The above config file is for inspiration, it needs to be present in any of the locations mentioned in the 
[Getting started](getting-started/README.md "configuration") guide.
Please save the config file to one of the locations, do not save it twice. The current folder is taking preference
over the config file in your `$HOME`.

I will annotate the properties with `.` for reference. So you can easily see the path of the properties. 

### app.db
This block contains the database details. We use an internal sqlite database to store some meta-data. This database
is never transferred outside of your filesystem. We need this data for using the app. 

#### app.db.initialised
Set this to false, this will right now run the table and field creation seed for the database. After a successful run
sn-edit sets this property to `true` and the creation will not run again. Be aware, that the initial seed is not deleting
any tables. For a reset, remove the `db` file set the property to `false`, this will re-create the database.

#### app.db.path
You need to set this to a full path, no symlinks supported officially. It is recommended to set the full path, this way,
we ensure that sn-edit finds the database file correctly. See a sample below.


```yaml
app:
  core:
    db:
    initialised: false
    path: /Users/username/sn-edit/sn-edit.db
```

### app.log_level
The log level defines the depth of the output that the app gives you. For generic usage, `info` should be enough.
For reporting an issue, it is recommended that you use the app with `debug` and provide as much details as possible.

Possible values:
* info
* warn
* error
* panic
* fatal
* debug


```yaml
app:
  core:
    log_level: info
```

### app.rest
This block contains the rest credentials. Right now we are supporting basic authentication only. But there are plans
to support at least some oauth flows.

#### app.rest.masked
This property has to be set to `false` per default. Since a lot of users are not comfortable saving their instance
credentials locally in plaintext, we are doing some masking.

Masking includes "obfuscating" the password that you've provided. For your first setup you set the username and password
in plaintext. If you run the app with masked=false, the app will take the plaintext password and mask it, setting the masked
property to true and overwriting your plaintext password with the masked one.

#### app.rest.xor_key
The xor key has to be set to something random. This key will be used to mask your password.

#### app.rest.url
The url to your instance, full url with the the leading protocol, but it is important that you do not set a trailing slash
at the end. The slash will be automatically appended if needed by sn-edit. The config file should contain an url without
a slash.


```yaml
rest:
  core:
    masked: false
    password: password
    url: https://dev11112.service-now.com
    user: username
    xor_key: maskingkey
```

### app.root_directory
The root directory must be a directory writable by sn-edit. We require full path, instead of relative path.
All the downloaded entries will be saved here and this will be the working directory for the app. Do not add
a slash at the end please. This will be handled by the app. We use os specific path separators, so it is important
it you do not add any additional slashes at the end. Sn-edit will handle that for you.

```yaml
app:
  core:
    root_directory: /path/to/the/working/folder
```

### app.tables
This is the most important part of the app. The tables block describes all the tables you would like to use with sn-edit.

You need to specify the table name first. You also need to define all the fields you want sn-edit to download. See more 
at the download command.

If you specify a field, please also specify an extension. This is required and sn-edit will be downloading the contents
of the field to a file of specified extension and field name.

So based on the sample below, if you would download an entry from the table `sys_script` (Business rules), then sn-edit
will be downloading the contents of sys_id, script and sys_name fields. The fields sys_id and unique key are required.
From these details sn-edit will determine the correct table and fields to download.

The sys_scope field is also something that we add in the background. This is to determine the scope of the entry. The
scope will be not downloaded as a file.

You can specify any amount of tables, sn-edit is not generating this for now. You need to manually fill the details you
would like to download and then run the download command.


```yaml
app:
  core:
    tables:
    - name: sys_script
      fields:
        - extension: txt
          field: sys_id
        - extension: js
          field: script
        - extension: txt
          field: sys_name
    - name: sys_script_include
      fields:
        - extension: txt
          field: sys_id
        - extension: js
          field: script
        - extension: txt
          field: sys_name
```
