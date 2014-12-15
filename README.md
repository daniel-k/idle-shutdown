idle-shutdown
=============

This bunch of scripts serves to shutdown a machine when certain requirements 
are met. Customization can easily ba done by adding your own bash scripts.

I created them with my NAS in mind to save electricity when my server is not
accessed anymore, but as the action as well as the conditions are customizable
it might be used for other tasks, too.

These scripts are tested on Ubuntu 14.04 and some may require additional
packages, please refer to the descriptions inside every script.


## Installation

1. Copy the project folder to a place that only root has access to, `/root`
   might be a good start.

2. It's important that only root can alter files in that directory, otherwise
   this creates a big security hole. So change permissions:
   `$ chmod -R go-rwx /root/idle-shutdown`

3. Setup a cronjob that executes [idle-shutdown](idle-shutdown) periodically.
   Example:
   `*/1 * * * * /root/idle-shutdown/idle-shutdown &> /dev/null`

4. Have a look at the existing scripts in [conf.d](conf.d) as they already
   provide some useful checks, but some need configuration.


## How to extent

The scripts are organized inside the folder [conf.d](conf.d) and executed in
lexicographical order. As soon as **every** script terminates successfully, i.e.
return the exit code 0, the action specified in [idle-shutdown](idle-shutdown)
will be perfomed (shutdown by default).

All you need to do is to add your own scripts to that directory and make them
executable, refer [to this example](conf.d/10_example).