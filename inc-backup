#!/bin/bash
set -o pipefail

# add below the directories you want to backup
INCLUDE=(/home/*/) 
# the above directory gets all subdirectories (i.e. user dirs) inside the "home" directory
INCLUDE+=(/etc/)
INCLUDE+=(/...some other directory.../)

# add below the directories or the file types you want to exclude
EXCLUDE=(cache/)
EXCLUDE+=(*.tmp)
EXCLUDE+=(/..some other directory../)

#add below the path to your backup directory
BACKUP_DIR_PATH="/mnt/backup/"

DATETIME="$(date '+%Y-%m-%d_%H-%M')"

echo ${INCLUDE[@]}

for SOURCE_DIR in ${INCLUDE[@]}; do
echo Source Dir: $SOURCE_DIR
readarray -d '/' -t name <<< ${SOURCE_DIR}
tarname=${name[-2]}

echo Compressing: $tarname
mkdir -p $BACKUP_DIR_PATH$tarname

# next line is where the magic is happening
tar --verbose --create --gzip --exclude=$EXCLUDE --listed-incremental=$BACKUP_DIR_PATH$tarname/$tarname.sngz --file=$BACKUP_DIR_PATH$tarname/$tarname-$DATETIME.tgz $SOURCE_DIR/

done

exit
