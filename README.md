License
==========
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE. 


snap-utils
==========

Linux LVM Snapshot utils

This very simple set of scripts can be used as base scripts for your backup strategy.

What we learned is that for consistent LVM snapshots you need to:

      *   If it's a mysql server, FLUSH ALL TABLES WITH READ LOCK
      *   Sync disk
      *   FSFREEZE all filesystems
      *   Take snapshot of entire VM disk (can be done at some RAID controllers also)
      *   UNFREEZE all filesystems

This script take of the steps above with a predefined timeout, avoiding whole system locks. 

FSFREEZE command is very dangerous, because it put on hold all processes that try to hit disk. It's why we included a timeout for the unlock operation. If the pos_snapshot command is not called after a predefined timeout, it's called automatically by system.

usage
=====

The proposed usage is running a backup tool of your choice on DOM0 of virtual machines.

This backup tool must call:

      /APP/scripts/pre_snap_command
      #If above command outputs "@@@SNAP_GO@@@", take a snapshot
      /APP/scripts/pos_snap_command

Enjoy it.
