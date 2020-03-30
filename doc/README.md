# Documentation

Bulding a sinhika makes a few assumptions. One of them is the Debian'ness of /etc/staff-group-for-usr-local existing, /usr/local set to g+s and the user you are operating under belongs to the group staff.

This is usually done behind the curtains for you, however, if in doubt:

```sudo touch /etc/staff-group-for-usr-local
sudo chmod -R g+s /usr/local
sudo chgrp -R staff /usr/local
```

Given the fact that you are not likely to run this on a shared server, this is not considered a security hole.

On a standard sinhika installation, everything happens in /usr/local the way described above. Also, the daemon processes run as a plain mortal user, which you have to pick by yourself.
