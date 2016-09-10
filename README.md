# hooky
Hooky: a python tool to perform a bunch of actions dictated by a json configuration file  

Design notes:  

Primary use case:  
as a Customizer hook script. One file, self contained.  
"An outside tool will drop it into the filesystem and execute it without any parameters"  

Primary use distro:  
Ubuntu. Maybe it'll work on debian too.  
Python3 will be required; restricting this to 15.04 and above.  

Primary package manager:  
apt with ubuntu flavor PPA support.  

Things we need to be able to do:  
Bootstrap from a packageless shell prompt as root inside of a chroot that has been set up for us.  
Provide the same things kamikazi-core's bash scripts do.  

Things we have to do to reach the end:  
* Define packagesets as a named packagegroup, eg 'kamikazi-webserver' might contain ['nginx-extra', 'rethinkdb']
* Basic control over package manager: update lists, install packages, purge packages, remove packages, read synaptic flavor package files.
* Advanced control over package manager: use basic controls to install wajig; shell out to wajig.
* Basic control over git: installation, default configuration, depth 1 clones.
* Basic control over templating: jinja2, autoescape off by default.
* Basic control over files and directories: rename files, move files, recursive copy files, link files, delete files.
* Creating a unix socket within the chroot
* Reading json input from a unix socket (on-build settings?)
* Printing json status messages to a socket (return status to user)
* Reading json input from a file (I don't like yaml or I'd use ansible playbooks)
* Printing json/plaintext status messages to a file descriptor (just in case there's no unix sockets, LXSS!)
* Run a shell script with bash (should probably always work)
* Run a shell script with dash/sh (on debian and ubuntu, sh is dash.)
* Run a shell script with xonsh / install xonsh (python3 bash replacement)
* Run wget safely (or download a file over http/https and write it to disk)
* Run dpkg -i on a downloaded .deb package (name this something with 'unsafe')
* Install/uninstall a pip2/pip3 package (or invoke both with one call)
* Run arbitrary systemctl commands (systemctl enable, creating symlinks)
* Run arbitrary sed commands (damn netdata install script)
* Unzip files (serf lives in a zip under the C:\, CLUSTERFARM SQUARECLIENTS)
