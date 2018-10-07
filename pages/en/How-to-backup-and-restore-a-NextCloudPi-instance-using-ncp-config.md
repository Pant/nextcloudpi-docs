How to backup and restore a NextCloudPi installation
====================================================

You may want to move your NCP instance to a larger drive or restore it after a hardware failure.

## Making backup excluding your data

You can visit https://nextcloudpi.local:4443 for NCP's web interface or start nextcloudpi-config from your NCP terminal by typing:

`sudo nextcloudpi-config`

![ ](https://user-images.githubusercontent.com/8775469/34511790-5bedb6f4-f05e-11e7-9d60-bba86e2c2166.png)

Move up and down with arrow-keys, use tab+enter to select(execute) or finish(cancel)

We are going to use nc-backup to back-up our NC instance to a file.

![](https://user-images.githubusercontent.com/8775469/34511800-664637ac-f05e-11e7-995c-f23e05d143ed.png)

The output will confirm if operation was successful and where the backup file is stored.

You may run backups automatically using nc-backup-auto
![](https://user-images.githubusercontent.com/8775469/34511804-692730ac-f05e-11e7-9ab0-f0ad3500d4df.png)
To enable/disable, type yes/no in the 'active' field, and adjust other settings to your needs 

We now have backups of our NC installation directory and database, no actual data included yet. Unless you choose to do so and typed 'yes' in the IncludeData field above (Make sure you have enough space before doing this). Next is a backup of the configuration files.
![](https://user-images.githubusercontent.com/8775469/34511805-6b475358-f05e-11e7-84a8-bb9b48995efd.png) 
Select destination for backup of configuration:
![](https://user-images.githubusercontent.com/8775469/34511811-72e6c85a-f05e-11e7-803f-bf306a539cf6.png)
![](https://user-images.githubusercontent.com/8775469/34511813-74e6f3aa-f05e-11e7-9b41-40f9535606a9.png)

We now have backups of our NC installation directory, database and the configuration files. 
Still no actual data included yet (unless you included it in the step before). Next is a backup or rather BTRFS snapshot of our ncdata-directory.
Note: This will only work if you used BTRFS instead of ext4 when formating your NC data partition.
![](https://user-images.githubusercontent.com/8775469/34511814-776e2dfa-f05e-11e7-8b42-fc4ed7a777df.png) 
![](https://user-images.githubusercontent.com/8775469/34511817-7a0bae8e-f05e-11e7-86fa-9866889b36c4.png)
![](https://user-images.githubusercontent.com/8775469/34511818-7c1d397c-f05e-11e7-86bc-88d5e3f4fc3c.png)
It will confirm the name and location of the snapshot taken upon completion.
You may want to enable nc-snapshot-auto to have regular snapshots taken automatically.

### Making backup including your data

Below you will find some of the same steps as above, difference being that ncdata (your files) will be included here, so this may take a long time to execute depending how much data you have stored. My Pi3 took about 20-30minutes to write 15Gb to an external usb drive.

Again, You can visit https://nextcloudpi.local:4443 for NCP's web interface or start nextcloudpi-config from your NCP terminal by typing:

`sudo nextcloudpi-config`

![20-nc-backup-select-in-ncp-config](https://user-images.githubusercontent.com/8775469/34664327-9c050340-f45b-11e7-82ec-fe4beab8017b.png)
Move up and down with arrow-keys, use tab+enter to select(execute) or finish(cancel)
Select destination location by typing the path: /media/btrfs is mine. Yours may be different. Type yes in include data field and hit enter to start the backup process.
![21-nc-backup-set-destination-and-include-data](https://user-images.githubusercontent.com/8775469/34664336-a17b62ec-f45b-11e7-9d1d-a31f2dccc90b.png)
Wait, go make coffee or tea or both, this may take while and depends on how much data you are backing up.
![22-nc-backup-launch-backup-nc-bkp_date-tar-created](https://user-images.githubusercontent.com/8775469/34664359-c022104c-f45b-11e7-9acd-a333c3363ffd.png)
Note the name and location of the backup created. Hit enter to exit.

[View video](https://youtu.be/FV80ZE9t6cE) showing how to backup an NCP instance through NextCloudPi web interface.

### Restoring a backup including your data

Restoring a NCP instance and using nc-restore looks almost the same as creating the backup.
You can visit https://your-local-IP:4443 for NCP's web interface or start nextcloudpi-config from your NCP terminal by typing:

`sudo nextcloudpi-config`

Move up and down with arrow-keys, use tab+enter to select(execute) or finish(cancel)
Select nc-restore hit enter
![30-nc-restore-select-in-ncp-config](https://user-images.githubusercontent.com/8775469/34664376-e0e1036a-f45b-11e7-850e-7a1ed4cd6d89.png)
Make sure you adjust the name and location to reflect yours. In example below, it failed, because I chose the wrong file. It worked after correcting it to reflect the backup created in previous step./media/btrfs/nextcloud-bkp_20180107.tar
![31-nc-restore-configure-location](https://user-images.githubusercontent.com/8775469/34664380-e942ef78-f45b-11e7-80ce-b7201909e7e9.png)
Time for some patience again ;-) It might take some time depending size.
![32-nc-restore-overwrite-old-instance-terminal-output](https://user-images.githubusercontent.com/8775469/34664383-ed643652-f45b-11e7-9a43-1f36790b5336.png)

[Video demonstration how to restore your ncp instance with ncp-web](https://youtu.be/YdXVIJPZWvw)
..............
This a a work in progress, thank you for your patience ;-)
Please comment or ask for help [HERE](https://github.com/nextcloud/nextcloudpi/issues/269)