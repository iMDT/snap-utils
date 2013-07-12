Read-FIRST
==========
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE. 

snap-utils
==========

Linux LVM Snapshot utils

This very simple set of scripts can be used as base scripts for your backup strategy.

For consistent LVM snapshots you need to:
    * If it's a mysql server, FLUSH ALL TABLES WITH READ LOCK
    * Sync disk
    * FSFREEZE all filesystems
    * Take snapshot of disk (in our case it's done on DOM0 of Xen)
    * UNFREEZE all filesystems

This script take care of doing all of these operations in a predefined amount of maximum time.

It means that your backup script will not put the database on "a waiting forever" state.

Also, the FSFREEZE is very dangerous, as it freezes all the systems, for that, a timeout is used. 

If the main backup process doesn't call the pos_snap_command, it will unfreeze after specified time.

usage
=====

The proposed usage is running a backup tool of your choice on DOM0 of virtual machines.

This backup tool must call:

      /APP/scripts/pre_snap_command
      #Take snapshot here
      /APP/scripts/pos_snap_command

Enjoy it.
