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
#### Upload
Upload a single file into a "folder"
```
# coldstore --put backup.tgz /stuff
```
This will result in the file backup.tgz being at **/stuff/backup.tgz**

Upload a directory into a "folder"
```
# coldstore --put /home/photos/2015/08 /pictures/2015
```
This will create an encrypted tgz of the folder 2015/08/ and put it in **/pictures/2015/08/**

Coldstore uses a similar trailing slash concept as rsync. A trailing slash on
destination path (/some/folder/) will be treated as a directory combined with the source
filename. Inversely, a destination path without a trailing slash
(/some/destination) will be treated as an absolute path for the folder or file.

#### Listing
```
# coldstore --list /
Listing /
- /stuff/backup.tgz
- /pictures/2015/08/
```

Above we can see that we have one file and one folder

#### Inspecting
```
# coldstore --inspect /testFile
Inspecting /testFile
{u'glacier_id': u'd14d2754-4165-11e5-a4f5-bc5ff4e7a098',
 u'glacier_vault': u'jl-archive001',
 u'host': u'scarto',
 u'metadata_version': u'v1',
 u'sha1': u'2bceab392b525c6dc881db5f1f5efa065dd3bc2f',
 u'size': 11697736,
 u'skipped_encryption': u'false',
 u'source_path': u'/home/jlester/portable.tgz',
 u'timestamp': 1439434125.813473,
 u'type': u'file',
 u'upload_date': u'August 12, 2015 21:48:45'}
 ```

#### Delete
```
# coldstore --delete /testFile
Delete /testFile
Deleting d14d2754-4165-11e5-a4f5-bc5ff4e7a098 from jl-archive001
```
