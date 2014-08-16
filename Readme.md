#Config-Loader

### A simple SLAX script that allows for easily loading a config onto a a Junos device

## Loading the script

1. Place the script file "config-loader.slax" into the directory /var/db/scripts/op/ on the device
2. Enable the script for usage in the configuration
..1 `set system scripts op file config-loader.slax`
3. Commit the configuration
..1 If there is an error in the script or if the script is missing then Junos will throw an error

## Usage

The tool can remotely load a configuration file via a file, FTP, or HTTP URL.

The script requires three arguments to load the configuration
1. source: The URL source for the config
..* FTP, HTTP, or a file path
..* Example ftp://foo:bar@1.2.3.4:/config.text
..* Example http://1.2.3.4:8080/config.text
..* Example /var/tmp/config.text
2. action: The action to take with the config
..* replace: Replaces the existing configuration with the newly loaded configuration file
..* merge: Merges the newly loaded configuration with the existing config
..* override: Discards all other candidate configurations and replaces it with the loaded config (not needed for this use case)
..* set: Set is specified when the text file you are loaded uses configuration CLI commands
3. format: The format of the loaded configuration
..* xml: specifies 

## Examples
```

Successfully loaded config:

root@device> op config-loader action set format text source http://172.16.237.1:8080/testconfig.set
Opening candidate configuration
Loading new configuration
Commiting candidate configuration

Error fetching config:
rroot@device> op config-loader action set format text source http://172.16.237.1:8080/testconfig.bad                      
Opening candidate configuration
Loading new configuration
Error fetching config

fetch: http://172.16.237.1:*: Not Found

```
