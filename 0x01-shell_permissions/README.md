0x01. Shell, permissions
useradd is a low level utility for adding users. On Debian, administrators should usually use adduser(8)
       instead.

       When invoked without the -D option, the useradd command creates a new user account using the values specified
       on the command line plus the default values from the system. Depending on command line options, the useradd
       command will update system files and may also create the new user's home directory and copy initial files.

Add a normal user
       If called with one non-option argument and without the --system or --group options, adduser will add a normal
       user.

       adduser  will  choose  the first available UID from the range specified for normal users in the configuration
       file.  The UID can be overridden with the --uid option.

       The range specified in the configuration file may be overridden with the --firstuid and --lastuid options.

       By default, each user in Debian GNU/Linux is given a corresponding group with the same name.  Usergroups  al‐
       low  group  writable  directories  to be easily maintained by placing the appropriate users in the new group,
       setting the set-group-ID bit in the directory, and ensuring that all users use a umask of 002.  If  this  op‐
       tion  is turned off by setting USERGROUPS to no, all users' GIDs are set to USERS_GID.  Users' primary groups
 Manual page addgroup(8) line 17 (press h for help or q to quit)

adduser will create a home directory subject to DHOME, GROUPHOMES, and LETTERHOMES.  The home  directory  can
       be  overridden  from the command line with the --home option, and the shell with the --shell option. The home
       directory's set-group-ID bit is set if USERGROUPS is yes so that any files created in the user's home  direc‐
       tory will have the correct group.

       adduser  will  copy  files  from SKEL into the home directory and prompt for finger (gecos) information and a
       password.  The gecos may also be set with the --gecos option.  With the --disabled-login option, the  account
       will  be  created but will be disabled until a password is set. The --disabled-password option will not set a
       password, but login is still possible (for example with SSH RSA keys).  To set up an encrypted home directory
       for  the  new user, add the --encrypt-home option.  For more information, refer to the -b option of ecryptfs-
       setup-private(1).

       If the file /usr/local/sbin/adduser.local exists, it will be executed after the user account has been set  up
       in order to do any local setup.  The arguments passed to adduser.local are:
       username uid gid home-directory
       The environment variable VERBOSE is set according to the following rule:

       0 if   --quiet is specified

       1 if neither
              --quiet nor --debug is specified
2 if   --debug is specified

              (The  same  applies to the variable DEBUG, but DEBUG is deprecated and will be removed in a later ver‐
              sion of adduser.)

   Add a system user
       If called with one non-option argument and the --system option, adduser will add a system  user.  If  a  user
       with  the  same name already exists in the system uid range (or, if the uid is specified, if a user with that
       uid already exists), adduser will exit with a warning. This warning can be suppressed by adding --quiet.

       adduser will choose the first available UID from the range specified for system users  in  the  configuration
       file (FIRST_SYSTEM_UID and LAST_SYSTEM_UID). If you want to have a specific UID, you can specify it using the
       --uid option.

       By default, system users are placed in the nogroup group.  To place the new system user in an already  exist‐
       ing group, use the --gid or --ingroup options.  To place the new system user in a new group with the same ID,
       use the --group option.

       A home directory is created by the same rules as for normal users.  The new system user will have  the  shell
       /usr/sbin/nologin (unless overridden with the --shell option), and have logins disabled.  Skeletal configura‐
       tion files are not copied.

       
By default, a group will also be created for the new user (see -g, -N, -U, and USERGROUPS_ENAB).
adduser:-adduser  and  addgroup  add  users  and  groups  to the system according to command line options and configuration information in /etc/ad‐
       duser.conf.  They are friendlier front ends to the low level tools like useradd, groupadd and usermod programs, by default choosing Debian
       policy  conformant UID and GID values, creating a home directory with skeletal configuration, running a custom script, and other features.
       adduser and addgroup can be run in one of five modes:

   Add a normal user
       If called with one non-option argument and without the --system or --group options, adduser will add a normal user.

       adduser will choose the first available UID from the range specified for normal users in the configuration file.  The UID can be  overrid‐
       den with the --uid option.

       The range specified in the configuration file may be overridden with the --firstuid and --lastuid options.

       By  default, each user in Debian GNU/Linux is given a corresponding group with the same name.  Usergroups allow group writable directories
       to be easily maintained by placing the appropriate users in the new group, setting the set-group-ID bit in  the  directory,  and  ensuring
       that  all  users  use  a  umask  of  002.  If this option is turned off by setting USERGROUPS to no, all users' GIDs are set to USERS_GID.
       Users' primary groups can also be overridden from the command line with the --gid or --ingroup options to set the group by id or name, re‐
       spectively.   Also,  users  can  be  added  to  one  or more groups defined in adduser.conf either by setting ADD_EXTRA_GROUPS to 1 in ad‐
       duser.conf, or by passing --add_extra_groups on the commandline.

       adduser will create a home directory subject to DHOME, GROUPHOMES, and LETTERHOMES.  The home directory can be overridden from the command
       line  with  the --home option, and the shell with the --shell option. The home directory's set-group-ID bit is set if USERGROUPS is yes so
       that any files created in the user's home directory will have the correct group.
