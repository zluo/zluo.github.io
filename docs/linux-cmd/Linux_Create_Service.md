---
layout: default
title: Create a service script
nav_order: 3 
parent: Linux Command
---
## Create an Service script

### Build an initscript

    /etc/init.d or 
    /etc/rc/init.d 

and place a script named test in that.

this is an example initscript:
```bash
#!/bin/sh
### BEGIN INIT INFO
# Provides:          testone
# Required-Start:    $local_fs
# Required-Stop:     $local_fs
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# X-Interactive:     false
# Short-Description: Example init script
# Description:       Start/stop an example script
### END INIT INFO

DESC="test script"
NAME=testone
#DAEMON=

do_start()
{
   echo "starting!";
}

do_stop()
{
   echo "stopping!"
}

case "$1" in
   start)
     do_start
     ;;
   stop)
     do_stop
     ;;
esac

exit 0
```

### Create an user for the desired service.

Ensure the created user has full access to the binary you want to set up:

    /usr/bin/python.

### Adjust the variables: 

    sudo vi /etc/init.d/example.

### Make sure the script is executable: 

    chmod +x /etc/init.d/example.

**Enable the daemon with**
   
    update-rc.d example defaults.

**Start the service**

    service example start
    
**Uninstall service**

### Run a script at start up

#### Method 1: Add commands to /etc/rc.local

    vi /etc/rc.local

with content like the following:
```bash
    /path/to/my/script.sh || exit 1   # Added by me
    exit 0
```

#### Method 2: Add an Upstart job (for systems older than 15.04)

1.  Create file /etc/init/myjob.conf

```bash
    description     "my job"
    start on startup
    task
    exec /path/to/my/script.sh
```

### Method 3: Add an init script (obsolete)
1.  Create a new script in /etc/init.d/myscript.

    vi /etc/init.d/myscript

```bash
    #!/bin/sh
    /path/to/my/script.sh
```

2.  Make it executable.

```bash
    chmod ugo+x /etc/init.d/myscript
```

3.  Configure the init system to run this script at startup.
```bash
    update-rc.d myscript defaults
```