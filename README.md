temp
====
# !/bin/sh -e
# Numlock control reset tool
# 15-5-2013

#set variables
UNSET="unset"
RESTORE="restore"

if [ "$1" = $UNSET ]
then
  #preparing directories
	rm -rf /wintmp
	mkdir /wintmp
	#mounting filesystems
	mount /dev/sda2 /wintmp
	#finding and removing auto-set file
	cd "/wintmp/ProgramData/Microsoft/Windows/Start Menu/Programs/Startup/"
	cp ./numlock.vbs ../numlock.bkp
	cp ./numlock.vbs /wintmp/Windows/numlock.bkp
	rm -rf ./numlock.vbs
	#safely unmounting
	umount /wintmp
	echo "Complete."

fi
	
if [ "$1" = $RESTORE ]
then
	#preparing directories
	rm -rf /wintmp
	mkdir /wintmp
	#mounting filesystems
	mount /dev/sda2 /wintmp
	cd "/wintmp/ProgramData/Microsoft/Windows/Start Menu/Programs/Startup/"
	#looking for backups
	if [ -f "/wintmp/ProgramData/Microsoft/Windows/Start Menu/Programs/numlock.bkp" ];
		then
			cp ../numlock.bkp ./numlock.vbs
			echo "Restored from /userdata/ backup."
		else
			echo "userdata level backup not present, using system based"
			cp /wintmp/windows/numlock.bkp ./numlock.vbs
			echo "Restored from system-level backup"
	echo "Complete"
	
fi
fi
