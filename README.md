## DavOps Tooling Website Solution 

-  **Step1** 

   **Preparing NFS Server**

   I spined up 3 RHEL-8.6.0_HVM-20220503-x86_64-2-Hourly2-GP2 in AWS called 1. NFS server, WEB1 and WEB2



  ![Alt text](images/spined.jpg)


   -  Configuring LVM on the NFS server

      I created 3 volumes of 10gb each on the same availability zone with my NFS server and attached them to my NFS server 
 
 ![Alt text](images/createdVolumes.jpg)

 - I inspected my server to confirm that the 3 disk added was sussessful 

 - Using Gdisk, I created single partition on the 3 disks

 ![Alt text](images/Gdisk.jpg)


 Using Lsblk to varify the newly created partitions 
  ![Alt text](image.png)


  - I installed LVM2 

  I used Pvcreate to mark each of the 3 disk as physical volume to use used by the LVM

![Alt text](image-1.png)

  - I used sudo pvs to varify 

    ![Alt text](image-2.png)


    - I used vgcreate the create volume group called webdata.vg and varified with **sudo vgs**

    ![Alt text](image-3.png)

    - I used lvcreate to create 3 logical volumes from the VG group. lv-opt,lv-apps and lv-logs.

    ![Alt text](image-4.png)

    ![Alt text](image-5.png)

    - I formated the volumes with xfs extension 

    ![Alt text](image-6.png)




-  I created 3 mount points called mnt/opt to mount lv-opt, mnt/logs to mount lv-logs and mnt/apps to mount lv-apps
mnt/apps to be used by webserver, mnt/logs to be used by webserver logs and mnt/opt to be used by jenkins server in next project

![Alt text](image-7.png)

