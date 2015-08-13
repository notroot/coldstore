# Coldstore

Coldstore is a simple tool for backing up data to Amazon Glacier. Coldstore can
push either individual files or whole directories to Glacier. All data is
encrypted before being uploaded and the necessary metadata is all stored in S3.
This gives the advantage that in the event of complete system failure, the only
thing necessary to retreive data is a copy of Coldstore, your AWS credentials
and of course your encryption key.

Coldstore is still under active development on the dev branch. Please check
back later to check on development progress.

## Example Usage

Upload a single file into a "folder"
```
# coldstore --put backup.tgz /stuff
```
This will result in the file backup.tgz being at **/stuff/backup.tgz**

Upload a directory into a "folder"
```
# coldstore --put 2015/08/ /pictures/2015/08
```
This will create an encrypted tgz of the folder 2015/08/ and put it in **/pictures/2015/08/**

Coldstore uses a similar trailing slash concept as rsync. A trailing slash on
destination path (/some/folder/) will be treated as a directory combined with the source
filename. Inversely, a destination path without a trailing slash
(/some/destination) will be treated as an absolute path for the folder or file.

Listing the archives
```
# coldstore --list /
Listing /
- /stuff/backup.tgz
- /pictures/2015/08/
```

Above we can see that we have one file and one folder
