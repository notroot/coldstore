# Coldstore

Coldstore is a simple tool for backing up data to Amazon Glacier. Coldstore can
push either individual files or whole directories to Glacier. All data is
encrypted before being uploaded and the necessary metadata is all stored in S3.
This gives the advantage that in the event of complete system failure, the only
thing necessary to retreive data is a copy of Coldstore, your AWS credentials
and of course your encryption key. 

Coldstore is still under active development on the dev branch. Please check
back later to check on development progress.  
