# Samba helping tools

The project provides tools that help made Samba (MS Windows network file
sharing) tasks a bit handy.

## smb-mount
One bash script that automates mounting of a samba share. It uses `sudo` to 
get rights for mounting. `smb-mount` also creates a shortcut script.


`smb-mount` uses current user name got using `whoami`, for authentication.
A domain name may also be provided as `:`-separated suffix of remote name.


Script maintains directory `/mnt/smb`. A share is mounted into subdirectory
of that one. Its name is composed of remote and share names. The script makes
no name manipulation during this. It only cuts out domain name.


The shortcut for given pair of remote (including domain) and user name is
created in the directory of script. Its name will be composed of:
* prefix `smbm-`;
* name of share equal to 2-nd script argument;
* infix `-on-`;
* remote name (without domain suffix).


Neither `smb-mount` nor a shortcut must not be called using `sudo` or with
other explicit rights assignment. It will call `sudo` itself when it is
actually needed.

### Synopsis
`smb-mount remote[:domain] share`


### Example 1
Assume the script is placed in `/usr/bin`. Given remote `MyNAS` with share
`Films` one can use command `smb-mount mynas films`.

Remote: `mynas`
Share: `films`
Mount point: `/mnt/smb/mynas/films`
Shortcut: `/usr/bin/smbm-films-on-mynas`

Note that using lowercase name equivalents is allowed by Samba while
`smb-mount` accounts the names as given in its arguments.

### Example 2
Given remote `MyOrgServer` with share `Documetns` one assigned domain `staff`,
may use command `smb-mount MyOrgServer:staff Documetns`.

Mount point: `/mnt/smb/MyOrgServer/Documetns`
Shortcut: `/usr/bin/smbm-Documetns-on-MyOrgServer`

