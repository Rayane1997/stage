Create-lvm
===========

Before installing docker on the target hosts we are going to set a dedicated volume. The lvm created will be used to contain the docker data in the docker machines and the images, necessary to run containers, for the registry.

|  Variable | Default  |  Comments |  
|----------------------|----------------|-----------------------------------------------------------------|
| mount_point  |  /data-docker |   directory where the docker data or the images will be held  |
| physical_device | /dev/sdb |  free disk used to contained the data   |
|volumegroup_name| docker00 | name of the volume group|
|lv_name| test | logical volume name|

 
requierement
------------

1 free disk 


Source
-------
https://github.com/zaxos/lvm-ansible-role

